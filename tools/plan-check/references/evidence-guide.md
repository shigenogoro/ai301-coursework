# Evidence guide: where evidence lives in a plan package

## Diagnosis and grounding

Where it lives: the plan's "Cause:" sentence in the Candidate plan section. The facts it must explain are in the Repro evidence block (steps, Actual output, and especially any control or contrast run) and the Issue section. Live: the diagnosis in plan.md, and the student's posted repro comment.
Good looks like: the cause names a mechanism the repro artifacts show (an error text, a log line, a control that differs), and the change targets that mechanism. Bad: the cause contradicts a control run, is asserted with no artifact behind it, or the fix only hides the symptom.

## Scope

Where it lives: the Candidate plan's "Change:" line with its "In:" and "Out:" statements, and the list of files. Compare against the one problem in the Issue section.
Good looks like: one change that fixes the reported problem, with an explicit "not touching X" line. Bad: refactors, migrations, upgrades, or extra fixes bundled in, or no stated edge.

## Executability

Where it lives: the files, functions, and approach named under Change in the Candidate plan. Live: the files-to-touch and approach sections of plan.md.
Good looks like: a stranger could open the named file and location and know what to edit. Bad: only goals ("make it robust"), with no file or function named.

## Test plan

Where it lives: the Candidate plan's "Test:" part, read against the Repro evidence block's Steps and Actual output (the "before").
Good looks like: it re-runs the repro trigger and states a specific observable after-fix result (exit code, status, text, value) that differs from the before and would fail without the fix. Bad: "verify it works", or a check that passes either way.

## Honesty

Where it lives: the risks and unknowns in the Candidate plan, and any hedging or certainty words in the plan and the Candidate plan comment; compared with the Repro evidence block's own limits (what it did not try, platforms covered). Live: the risks and unknowns in plan.md, and the Deviations heading after the build.
Good looks like: gaps in the repro evidence appear as stated unknowns, and hypotheses are labelled as such. Bad: "guaranteed" or "root cause confirmed" with nothing shown, or no unknown where the evidence plainly leaves one.

## Comms

Where it lives: the Candidate plan comment, read against the Thread highlights (maintainer direction, prior-art PRs, test requests) and the Repo facts block (templates, contributing asks, AI-use policy line). Live: the issue's live thread, CONTRIBUTING.md and any AI policy, and comment.md.
Good looks like: the comment answers each explicit maintainer ask (or engages it and says why it differs), engages any prior-art PR, includes any AI disclosure the policy requires, and states a concrete plan specific to this issue. Bad: ignores an owner's direction, races a prior PR, omits a required disclosure, or says "same approach as above".
