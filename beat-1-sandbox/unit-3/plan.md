# Plan: issue #61, health check DB probe passes a raw SQL string

## Diagnosis

`api/routes/health.py:32` runs `await db.execute("SELECT 1")` with a bare string. SQLAlchemy 2.x only accepts textual SQL wrapped in `text()`, so the call raises `ArgumentError` and the route marks postgres `unhealthy`.

Evidence from my repro comment (issue #61, comment 5883974946, commit `2f4e82f`, SQLAlchemy 2.1.1, Postgres 16.15, Windows 11, uvicorn):

- `curl -i http://127.0.0.1:8000/health` returned `HTTP/1.1 503` with `"postgres":"unhealthy"`.
- The log line for the same `x-request-id`: `postgres_health_check_failed error="Textual SQL expression 'SELECT 1' should be explicitly declared as text('SELECT 1')"`.
- Control, same database and session: `[A] session.execute("SELECT 1")` raised `sqlalchemy.exc.ArgumentError`; `[B] session.execute(text("SELECT 1"))` returned `1`. `psql -c "SELECT 1"` also returned 1.

The database is healthy, and only the string form fails. That points at the call, not at connectivity or the engine, so wrapping in `text()` fixes the cause rather than hiding the error.

## Scope

In scope: wrap the probe's SQL in `text()` in `api/routes/health.py`, and add one unit test that fails without it.

Not in scope:
- The `redis` probe (`'Settings' object has no attribute 'redis_host'`). That is #62, and my repro made no claim about it.
- The vector-db probe, the `chromadb` container crash, and `scripts/seed_db.py` console encoding.
- Any other route, `core/database.py`, dependency versions, or `pyproject.toml`.

## Files I will touch

- `api/routes/health.py`: add `from sqlalchemy import text`; change line 32 to `await db.execute(text("SELECT 1"))`.
- `tests/unit/test_health.py` (new): call `health_check()` with an `AsyncMock` db and assert `execute` received a `TextClause`, not a `str`. The repo has no health tests today.

## Approach

1. Create branch `fix/61-health-check-text-sql` from `main`.
2. Write the unit test first and confirm it fails on current `main`.
3. Make the one-line change and confirm the test passes.
4. Run `make check` and `make test-unit`, as CONTRIBUTING requires.
5. Re-run my repro steps (below).

## Test plan

Re-run my unit 2 repro on the fixed branch: compose stack up, `alembic upgrade head`, uvicorn, then `curl -i http://127.0.0.1:8000/health`.

- Before (from my repro): body has `"postgres":"unhealthy"`, and the log has `postgres_health_check_failed ... ArgumentError`.
- After, expected: body has `"postgres":"healthy"`, and the log has `postgres_health_check_passed` and no `ArgumentError`.
- The overall response is still expected to be `503` with `"redis":"unhealthy"` because of #62. That is not a failure of this fix.
- Control script `repro_61_control.py` should still show `[A]` raising and `[B]` returning 1, since it exercises SQLAlchemy directly.
- The new unit test fails on `main` and passes on the branch.

## Risks and unknowns

- I only tested Windows with Docker Desktop, the Compose `db` service, and uvicorn without `--reload`. I have not tried `make run`, the Dockerfile image, or a hosted Postgres.
- I have not checked whether other code calls `execute()` with a string. A grep of `execute("` found only `health.py:32`, but I have not traced dynamic call sites.
- Because redis stays unhealthy until #62, I cannot show an end-to-end `200` from `/health`. I can only show the postgres field flipping.
- CONTRIBUTING mentions xfail markers for seeded bugs. I found no health tests and so no marker to remove, but I have not searched every test directory for one.

## Prior art on the thread

- PR #82 (open): wraps the same line in `text()` and also changes the redis probe (#62), with no test. I am keeping #62 out of my change.
- PR #96 (open): same `text()` change plus `tests/unit/test_health_route.py`. My plan overlaps it. I have read its description, not its diff.
- Before opening a PR in unit 4 I will diff my branch against both and note any overlap.

## Deviations

The fix and the files match the plan: `api/routes/health.py` got `from sqlalchemy import text` and `text("SELECT 1")`, plus the new `tests/unit/test_health.py`. Differences from what I wrote:

- The unit test needed `@pytest.mark.unit`, because `make test-unit` runs `-m unit` and would otherwise skip it. ruff also rejected a bare `try/except/pass`, so I used `contextlib.suppress(Exception)`.
- `make typecheck` fails with `numpy/__init__.pyi:737: Type statement is only supported in Python 3.12 and greater`. It fails the same way on `main` without my change, so it is the environment (pyproject pins `python_version = "3.11"`), not this diff. `make lint`, `make format` and `make test-unit` (376 passed, 53 xfailed) pass.
- After the fix, `curl -i /health` shows `"postgres":"healthy"` and the log shows `postgres_health_check_passed`. The response is still `503` because of redis (#62), as I expected.
- I did not diff against #82 and #96 during the build. I will do that before opening the PR in unit 4.
- I did not change `pyproject.toml`. mypy cannot run to completion here, so I did not check which suppressions are now unnecessary.
