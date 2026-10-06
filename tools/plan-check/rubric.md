# Rubric: is this plan ready to post and build from?

Six required checks, one per way a bad plan gets posted: a cause the
repro evidence does not support, a change with no edge, a plan a
stranger cannot start, a test that proves nothing, certainty about
things the author has not verified, and a comment that ignores the
thread or the repo's rules. Every pass condition judges the thing
itself against the evidence, never the write-up's length or headings.

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| cause-grounded | The plan's stated cause, read against the repro evidence block (steps, artifacts, any control run) and the issue text. | The stated cause explains the behavior the repro evidence actually shows, and the fix targets that cause, not only the visible symptom. Fail if the cause contradicts a repro artifact or control run (e.g. blames a component the control shows is fine), is a guess with no tie to any shown artifact, or the change patches the symptom (hides the error, special-cases the input) while the evidence points at a cause elsewhere. | required |
| scope-bounded | The plan's in-scope statement, its not-in-scope statement, and the files/areas it says it will change, read against the issue's one reported problem. | The plan is one change that fixes the reported problem, and it names what it will NOT touch. Fail if it adds refactors, migrations, redesigns, dependency upgrades, or fixes for other issues that the repro does not require, or if nothing says where the change stops. | required |
| executable | The plan's files/areas and approach, read as a stranger who has the repo but not the author. | A stranger could start without asking: the plan names the specific file, module, or code area to change and what the change is. A plan that names a specific component and the concrete change, and says the exact function is pinned while making the change, passes. Fail if it only states a goal ("make it robust", "refactor and fix"), names no concrete place in the code, or gives no concrete action. | required |
| test-decisive | The plan's test plan, read against the repro evidence's steps and observed output. | The test plan re-runs the repro's trigger and names an observable result that differs before and after the fix (an exit code, output text, HTTP status, a value), and it would fail if the fix were absent. Fail if it only says "test it", "verify it works", or names a check that passes with or without the fix. | required |
| honest-unknowns | The plan's risks and unknowns and its certainty words, read against what the repro evidence did and did not cover. | The plan and comment do not claim more than the evidence shows: a diagnosis the plan presents as its working cause, or hedged where untraced, passes, and so does a short or "none beyond X" risk line when nothing in the evidence contradicts it. Fail only if the plan or comment gives a guarantee or a promised outcome ("guaranteed", "will definitely fix"), states a root cause as verified or confirmed when no shown artifact backs it, or asserts a fact the repro evidence contradicts or plainly never touched that the change depends on. Do not fail a plan merely for listing few unknowns. | required |
| thread-and-convention | The plan comment, read against the issue's thread highlights (maintainer direction, prior-art PRs, requests for tests or approach) and the repo-facts block (templates, contributing asks, AI-use policy). | The comment follows explicit maintainer direction in the thread (or engages it and says why it differs) and any stated repo convention. If the repo's policy requires AI-use disclosure covering comments, the comment contains one naming the tool or kind of help. If the repo has a stated own-words rule, the comment is specific to this issue, not boilerplate. Fail if the comment ignores a maintainer's explicit ask, races or duplicates a prior-art PR without engaging it, or omits a required disclosure. The comment must also state a concrete plan, not "same approach as above". | required |

## Verdict rule

accept if every required check grades `pass`; reject if any required
check grades `fail`. `unclear` counts as `fail`: a plan whose
evidence cannot be verified is not ready to post. There are no
preferred checks.
