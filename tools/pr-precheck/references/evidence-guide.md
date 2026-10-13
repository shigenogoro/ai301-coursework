# Evidence guide: where evidence lives in a PR package

Live mode files: `plan.md` (with `## Deviations`), the branch diff from `git diff main...HEAD` and commits from `git log --oneline main..HEAD`, `pr_draft.md` (title on line 1, filled PR template below), `test_evidence.md`, the issue via `gh issue view <n> --comments`, and the repo's `.github/PULL_REQUEST_TEMPLATE.md` and `docs/CONTRIBUTING.md`.

## Plan fidelity (harness category: silent-drift)

Where it lives (eval): the Plan context block's "Plan:" paragraph (scope, "Not in scope", Files, any deferral or known-limit note), read against the Candidate PR's Diff (every `---`/`+++` file header and hunk) and the Description's claims.
Where it lives (live): `plan.md`'s Scope, Files I will touch, and Deviations sections, read against `git diff main...HEAD`; the claims in `pr_draft.md`'s Summary and Changes.
Good looks like: every changed file appears in the plan's Files list or a deviation note, every hunk is the planned change or its test, and every promised deliverable is in the diff or explicitly deferred. Every description claim ("implements the plan", "docs updated", "no other changes") can be pointed at in the diff.
Bad: an extra hunk (a rewrite, a new flag or config option, a renaming pass, an unrelated file) that the plan does not name or scopes out; a promised part missing with no note; a description claiming more than the diff, or "exactly the plan" over a diff that differs.

## Test evidence (harness category: not-tested)

Where it lives (eval): the Candidate PR's Test evidence section, read against the plan's "Test plan:" and the "Repro evidence" line (trigger and observed before). The repo's checks are named in the Repo facts block.
Where it lives (live): `test_evidence.md` (before on main or from the unit 2 repro, after on the branch, and `make test-unit`, `make test-integration`, `make lint`, `make typecheck` output), read against `plan.md`'s Test plan; the Testing section of `pr_draft.md`.
Good looks like: the repro's own trigger re-run with before and after output that differ observably (text, exit code, status, value); every scenario the test plan names is shown; the repo's suite or check commands are named with their outcome. An honestly reported failing check, with a reason not caused by the diff, still counts.
Bad: "tested locally", "works now", "tests pass" with no output; only the control or a different input exercised; a named scenario silently missing.

## Diff quality (harness category: unreviewable)

Where it lives (eval): the Candidate PR's Diff and Commits list.
Where it lives (live): `git diff main...HEAD` and `git log --oneline main..HEAD`; also `git diff main...HEAD --stat`, which should list only the fix and its tests, never `plan.md`, `comment.md`, `pr_draft.md`, or `test_evidence.md`.
Good looks like: the fix is visible on first read and every changed line is needed for it or its test; comments explaining the fix are fine.
Bad (any one fails): debug prints, eprintln, or console.log; commented-out code or earlier attempts; dead or `_unused` functions, `allow(dead_code)`; TODOs on touched lines; re-indent, format, or import churn; re-printed duplicate lines; drive-by edits. Commits like "wip" or "cleanups while debugging" corroborate.

## Standards and comms (harness category: standards-wall)

Where it lives (eval): the Repo facts block's "pull requests:" line (template sections, checklist, issue-link, changelog or whatsnew asks) and "contribution policy:" line (AI-use policy), read against the Description and the Diff (for required files such as a changelog entry).
Where it lives (live): `.github/PULL_REQUEST_TEMPLATE.md` (Summary, Issue `Closes #`, Changes, Testing checklist, Screenshots / Demo, Notes for Reviewers) and `docs/CONTRIBUTING.md` (branch naming, conventional commits, removing a seeded bug's xfail marker and pyproject suppression), read against `pr_draft.md`, the commits, and the diff. The course requires an AI-use disclosure in Notes for Reviewers.
Good looks like: every required section filled with content specific to this PR, checklist boxes ticked only where true, the issue linked, any required entry present in the diff, and an AI disclosure naming the tool and the extent of help whenever the policy requires one.
Bad: a required checklist or section absent, no issue link where required, a stated changelog or whatsnew entry missing from the diff, or no AI disclosure where the policy demands it, even when the fix itself is excellent.
