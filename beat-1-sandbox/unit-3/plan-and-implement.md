# Unit 3 — Plan and Build

Path: `beat-1-sandbox/unit-3/plan-and-implement.md`

Record of your plan, the branch you built it on, and the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in the
repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Posted upstream

**GitHub username**

shigenogoro

**Plan comment**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/61#issuecomment-6006584251

> My plan for #61, built from the reproduction I posted above (comment 5883974946).
>
> Cause. api/routes/health.py:32 passes the bare string "SELECT 1" to db.execute(). My control run on the same Postgres session shows the string form raising ArgumentError while text("SELECT 1") returns 1, and psql answers 1 directly. So the database is fine and the call is what fails.
>
> Change. Import text from sqlalchemy and change line 32 to await db.execute(text("SELECT 1")). I'll also add tests/unit/test_health.py, which calls health_check() with a mocked session and asserts execute gets a TextClause. It should fail on main and pass on the fix.
>
> Not touching. The redis probe (redis_host, that's #62), the vector-db probe, and core/database.py.
>
> Test plan. Re-run my repro: curl -i http://127.0.0.1:8000/health against the Compose Postgres. Before, the body had "postgres":"unhealthy" and the log had the ArgumentError. After, I expect "postgres":"healthy" with no ArgumentError. The overall response will probably still be 503 because of #62, so I won't be able to show a 200.
>
> Unknowns. I only ran Windows with Docker Desktop and uvicorn without --reload. I haven't tried make run, the Dockerfile image, or a hosted Postgres, and I haven't traced other callers beyond a grep for execute(".
>
> Open PRs on this line. #82 wraps the same SELECT 1 in text() but also changes the redis probe to fix #62, in one PR with no test. #96 makes the same text() change and adds tests/unit/test_health_route.py. I read both descriptions, not their diffs. My plan overlaps both on the text() line. It differs from #82 by keeping #62 out of this change, and from #96 only in being built on my own repro and test. I'll build it on a branch in my fork, and I'll compare it against #82 and #96 before opening any PR so I don't duplicate them blindly.

---

## Your branch

**Branch**

`fix/61-health-check-text-sql`

**Evidence**

Issue #61, repro from my unit 2 comment (commit `2f4e82f`, Windows 11, Docker Desktop, Postgres 16 from the Compose `db` service, uvicorn without `--reload`). Same command before and after the fix. Before = `main`, after = branch `fix/61-health-check-text-sql`.

**Before (main)**

```
$ curl -i http://127.0.0.1:8000/health
HTTP/1.1 503 Service Unavailable
date: Tue, 06 Oct 2026 00:42:53 GMT
server: uvicorn
content-length: 184
content-type: application/json
vary: Origin
x-request-id: 19d4879e-e423-4903-a005-fbdb5ee95314

{"detail":{"status":"unhealthy","dependencies":{"postgres":"unhealthy","redis":"unhealthy","vector_db":"healthy"},"safety_events_last_hour":0,"timestamp":"2026-10-06T00:42:53.586899"}}
```

Server log lines for those requests:

```
2026-10-05 20:42:57 [error    ] postgres_health_check_failed   error="Textual SQL expression 'SELECT 1' should be explicitly declared as text('SELECT 1')" request_id=4618688b-1e3a-4d66-829a-b4604922730d
2026-10-05 20:42:57 [error    ] redis_health_check_failed      error="'Settings' object has no attribute 'redis_host'" request_id=4618688b-1e3a-4d66-829a-b4604922730d
2026-10-05 20:42:57 [debug    ] vector_db_health_check_passed  request_id=4618688b-1e3a-4d66-829a-b4604922730d
```

**After (fix applied)**

```
$ curl -i http://127.0.0.1:8000/health
HTTP/1.1 503 Service Unavailable
date: Tue, 06 Oct 2026 00:43:16 GMT
server: uvicorn
content-length: 182
content-type: application/json
vary: Origin
x-request-id: bdcb390a-f0f4-4009-8a3f-f2fb72133785

{"detail":{"status":"unhealthy","dependencies":{"postgres":"healthy","redis":"unhealthy","vector_db":"healthy"},"safety_events_last_hour":0,"timestamp":"2026-10-06T00:43:17.506894"}}
```

Server log lines for that request:

```
2026-10-05 20:43:17 [debug    ] postgres_health_check_passed   request_id=bdcb390a-f0f4-4009-8a3f-f2fb72133785
2026-10-05 20:43:17 [error    ] redis_health_check_failed      error="'Settings' object has no attribute 'redis_host'" request_id=bdcb390a-f0f4-4009-8a3f-f2fb72133785
2026-10-05 20:43:17 [debug    ] vector_db_health_check_passed  request_id=bdcb390a-f0f4-4009-8a3f-f2fb72133785
```

`postgres` goes from `unhealthy` to `healthy` and the `ArgumentError` is gone. The response is still `503` because `redis` is unhealthy (`'Settings' object has no attribute 'redis_host'`), which is #62 and outside this change.

Unit test, `tests/unit/test_health.py`, run with `.venv/Scripts/python -m pytest tests/unit/test_health.py -q`:

```
before: FAILED tests/unit/test_health.py::test_postgres_probe_uses_text_clause
        1 failed, 2 warnings in 5.07s
after:  1 passed, 2 warnings in 1.32s
```

`make test-unit` on the branch: `376 passed, 53 xfailed`.

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

1. Smoke run, `--limit 3`: `pkg-01` and `pkg-03` agreed; `pkg-02` errored on Windows text encoding. After I made `run_eval.py` pass UTF-8 to the subprocess and find `claude.cmd`, `pkg-02` agreed.
2. First full run: **17/20**. Misses: `pkg-05`, `pkg-09`, `pkg-14`, all gold accept that I rejected. `categories:` line was `clear-accept 4/7  scope-creep 4/4  thread-convention 2/2  unbuildable 3/3  wrong-cause 4/4`.
3. After loosening `honest-unknowns` and `executable`, a partial run of `pkg-05,09,14` plus canaries `pkg-04,07,10,12,17,18,20`: the five that completed agreed (`5/5`), and five errored with no message, so I re-ran those with `--workers 2`: `5/5`.
4. Second full run: **20/20**, with every category matched (`clear-accept 7/7  scope-creep 4/4  thread-convention 2/2  unbuildable 3/3  wrong-cause 4/4`). This is the run in `eval-run.txt`, whose line reads `agreement: 20/20 scored items  (bar: 18/20: PASS)`.

Scores in order: 17/20, 20/20.

**Package analysis**

**pkg-14** (zellij, color-query responses leaking into the pane on reattach). Category `clear-accept`, gold label **accept**.

My first rubric decided **reject**, so it disagreed. The note column said `failed: executable, honest-unknowns`. The graded reasons were:

- executable: the plan names "the client attach/reattach path in zellij-server" and "zellij-client terminal query issuance", but says "exact functions to be pinned in the PR after tracing". My first `executable` condition asked for "the specific files, functions, or locations", so naming an area without a function failed it.
- honest-unknowns: the grader read the diagnosis as asserted fact while tracing was still to do, and noted the plan lists only one risk (a lost keystroke) while the repro was WezTerm on macOS only.

The gold note is that the plan is grounded: fresh attach is clean, the leak starts at reattach, 0.44.1 is clean, and the cache control fits. The plan also bounds its scope and defers the Windows variant with a reason. The diagnosis is tied to repro artifacts, so it was never a guess. My rubric read it as a plan that "didn't know enough" when it was actually one that said where it was still tracing. I fixed that in the two checks (next field). `pkg-14` now agrees.

**Check rationale**

From `tools/plan-check/rubric.md`, exactly as it reads now:

| honest-unknowns | The plan's risks and unknowns and its certainty words, read against what the repro evidence did and did not cover. | The plan and comment do not claim more than the evidence shows: a diagnosis the plan presents as its working cause, or hedged where untraced, passes, and so does a short or "none beyond X" risk line when nothing in the evidence contradicts it. Fail only if the plan or comment gives a guarantee or a promised outcome ("guaranteed", "will definitely fix"), states a root cause as verified or confirmed when no shown artifact backs it, or asserts a fact the repro evidence contradicts or plainly never touched that the change depends on. Do not fail a plan merely for listing few unknowns. | required |

Why it reads this way: my first version failed a plan for having "no unknown where the evidence plainly leaves one". That made the grader reject `pkg-05` (it wrote "Risk: none identified" next to repro that only covered Ubuntu), `pkg-09` and `pkg-14`, which gold labels accept. Their problem was never a false claim, only a short risk line. I rejected the idea of counting unknowns. The check now fails only on three things a reader can point at: a guarantee or promised outcome, a root cause called verified with no artifact behind it, or a fact the change depends on that the repro contradicts or never touched. It also says outright "Do not fail a plan merely for listing few unknowns", because without that sentence the grader kept falling back to the old reading.

**Trade-offs**

`honest-unknowns` now gives up the ability to fail a plan that is merely thin on risks. A plan with "Risk: none" and a repro that covered one platform passes as long as it makes no guarantee and no false certainty claim. I accept that it will miss a plan that is overconfident only by omission.

I checked what the loosening cost with canaries, `--only pkg-04,pkg-07,pkg-10,pkg-12,pkg-17,pkg-18,pkg-20`, covering both `thread-convention` packages (`pkg-04`, `pkg-20`), `wrong-cause` (`pkg-07`), `unbuildable` (`pkg-10`, `pkg-17`, `pkg-18`) and `scope-creep` (`pkg-12`). None flipped, and the final full run kept all 16 reject packages rejected (20/20). The reject packages are caught by other checks (`cause-grounded`, `scope-bounded`, `executable`, `thread-and-convention`), so `honest-unknowns` was not carrying them.

The `executable` change has the same cost: a plan that names a component and a concrete change but defers the function name now passes, so it will miss a plan that hides behind "pinned later" with no real location.

---

Related paths: `plan.md` and `eval-run.txt` in this directory; your skill's files in
`tools/plan-check/`.
