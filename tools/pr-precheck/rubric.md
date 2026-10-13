# Rubric: is this pull request ready to submit?

Six required checks, one or two per way a bad PR gets submitted:
silent drift (the diff does more or less than the plan, or the
description claims fidelity the diff contradicts), not tested (no
observable before/after for the plan's repro, or the repo's checks
never shown), unreviewable (debris buries the change), and standards
wall (the repo's stated template or disclosure asks ignored). Every
pass condition judges the artifact against the plan, the issue, and
the stated standards, never the description's length or polish. A
shortfall the plan's deviation notes and the description both
disclose is honest scoped work, not a failure.

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| diff-matches-plan | Every file and hunk in the diff, read against the plan's Files list, its in-scope change, its "Not in scope" statements, and its deviation notes. Live: `git diff main...HEAD` against `plan.md`. | Every hunk is either the planned change, a test for it, or an explanatory comment on it, or is covered by a deviation note; and every change the plan promises is in the diff or disclosed as deferred. Fail if any hunk touches a file or behavior the plan does not name (a rewrite of a neighboring function, a new config option or flag, a renaming pass, a dependency bump, an edit in a file the plan never lists), especially anything the plan explicitly scopes out, or if a promised part (a docs update, a second fix, a test) is missing with no note. Adjacent or "small" extra work still fails if it is new behavior the plan did not include. | required |
| description-matches-diff | Each factual claim in the PR title and description (what changed, "implements the plan exactly", "no changes beyond", "docs now say", "no functional changes outside X"), read against the diff hunk by hunk. | Every claim about what the PR changes is visible in the diff, and every fidelity claim holds. Fail if the description claims something the diff does not contain (a docs change, a test, a fix), or claims fidelity or "nothing else changed" while the diff contains changes it does not mention. A description that discloses a deferral the plan also records passes. | required |
| test-decisive | The test-evidence section's before/after, read against the plan's test plan and the repro evidence's trigger and observed output. | The evidence re-runs the plan's repro trigger (the failing path, not a control or a different input) and shows an observable after-fix result (output text, exit code, status, value) that differs from the before (the before may be quoted from the repro). Every failure mode or bug scenario the plan's test plan names (each input that fails before the fix) is shown with output, or its omission is disclosed as deferred in both plan and description. Controls (inputs that already work before the fix and should stay unchanged) and the repo's suite may be reported in a sentence without output. Fail if the evidence is only "tested locally", "works now", "verified on my machine", or "tests pass" with no repro output; if it re-runs only a control or the unchanged path (e.g. the single-file case when the bug is multi-file, a different request than the issue's); or if it silently skips a failure mode the plan's test plan named. Do not fail only because a control is asserted without output. | required |
| repo-checks-run | The test evidence (and live: `test_evidence.md`) read against the repo's stated checks in the repo facts or contributing guide (test suite, lint, type check). | The evidence names the repo's suite or check command and shows its outcome (e.g. "`cargo test` passes (614 tests)", "`pytest` 1462 passed"). A check that fails passes this row if the failure is reported honestly with a reason that is not this diff (e.g. it fails identically on main). Fail if no repo check outcome is shown at all, or a stated required check is silently missing. | required |
| diff-clean | The unified diff, line by line, and the commit list. | The diff contains only the change and its tests: no debug output (prints, `eprintln!("DEBUG ...")`, `console.log`), no commented-out code or earlier attempts, no dead or unused functions (including ones behind `allow(dead_code)` or named `_unused`), no TODO/FIXME left on lines the PR touches, no formatting, re-indent, re-ordering, or import-restructure churn on lines the fix does not need, and no duplicated lines. Explanatory comments about the fix are fine. Fail if any such debris appears, even once, even next to a correct fix; commit messages like "wip", "misc cleanups while debugging" are corroborating evidence, not required. | required |
| template-and-disclosure | The repo facts block's PR-template asks and contribution policy (live: `.github/PULL_REQUEST_TEMPLATE.md`, `docs/CONTRIBUTING.md`, and the course's AI-use disclosure ask), read against the description and the diff. | Every section or checklist item the repo states as required is present with real content, and any stated deliverable the template requires for this kind of change (an issue link such as "closes #N", a changelog or whatsnew entry for a bug fix, a removed xfail marker for a seeded bug) is in the description or diff. If the repo's policy requires AI-use disclosure, the description contains one naming the tool and the extent of help; treat every package as AI-assisted work, so a missing disclosure fails when the policy requires it. Fail if a required section, checklist, issue link, or stated entry is visibly absent, or the required disclosure is missing. When the repo has no template and no AI policy, pass unless a stated ask is visibly ignored. | required |

## Verdict rule

accept if every required check grades `pass`; reject if any required
check grades `fail` or `unclear`. `unclear` counts as `fail`: a PR
whose evidence cannot be verified from the package is not ready to
submit. There are no preferred checks, so every row can hold the
package. A shortfall disclosed in both the plan's deviation notes and
the description is not by itself a fail in any row.
