# Procedure: how this skill grades a plan package

## Read order

1. Live mode: read scope.md first and confirm the issue's repo matches. Eval mode: skip it.
2. Read the issue (title, body) and note the ONE problem it reports and its trigger.
3. Read the thread highlights and note every maintainer direction, prior-art PR, or request for tests/approach.
4. Read the repo-facts block and note the templates, contributing asks, and AI-use policy (does it require disclosure covering comments? an own-words rule?).
5. Read the repro evidence block and note the steps, the observed output, and any control run (what it rules in or out). Read it before the plan, so the plan is judged against facts, not the other way round.
6. Read the candidate plan, then the candidate plan comment. Note the stated cause, in/out of scope, files, approach, test plan, and unknowns.

## Evidence gathering

1. cause-grounded: copy the plan's cause sentence and the repro artifact or control result that bears on it. Record whether they agree, contradict, or are unrelated.
2. scope-bounded: copy the in-scope and not-in-scope lines and the list of files; compare each to the one problem from Read order step 2. Record anything beyond it.
3. executable: list the concrete files/functions/locations the plan names and the action at each. Record "none" if there are none.
4. test-decisive: copy the test plan's expected result and the repro's observed "before" result. Record whether they differ and whether the test would fail without the fix.
5. honest-unknowns: list the unknowns the plan states; list what the repro evidence did not cover (platforms, callers, paths); copy any certainty words ("guaranteed", "root cause confirmed").
6. thread-and-convention: pair each maintainer direction and repo rule from Read order steps 3-4 with the line in the plan comment that answers it, or record that none does. Record any disclosure line.
7. Eval mode: use only the bundle text. Live mode: take issue-side facts from the live thread, repro evidence from the student's posted repro comment, and plan facts from the drafts.

## Check execution

1. Run the checks in table order using only the evidence recorded above; re-read only the lines you copied, not the whole package, for each check.
2. Grade `pass` only if the pass condition is met outright; grade `fail` if any fail clause applies.
3. Grade `unclear` only if the evidence the check needs is genuinely absent from the package (not merely weak). Record "absent: <what>" as the evidence.
4. Judge the content, never the formatting: a terse plan that meets the condition passes; a long confident one that does not, fails.
5. If a check passes by its stated condition but feels wrong, it still passes.

## Verdict assembly

1. Apply the rubric's verdict rule: accept only if all six checks grade `pass`; any `fail` or `unclear` gives reject.
2. In the output, give each check one line of evidence quoting the fact that decided it. For a reject, the first failing check's line quotes the plan text and the evidence text that conflict.
3. Emit the JSON block last, with the verdict matching the grades.
