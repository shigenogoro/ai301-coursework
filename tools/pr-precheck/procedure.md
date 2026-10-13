# Procedure: how this tool grades a PR package

## Read order

1. Live mode: read `scope.md` first; stop if its `Repo:` line is a placeholder, refuse if the issue is not in that repo. Eval mode: skip it.
2. Read the repo facts (live: `.github/PULL_REQUEST_TEMPLATE.md` and `docs/CONTRIBUTING.md`). Write down every stated ask: required template sections or checklist items, issue-link format, changelog/whatsnew entries, test/check commands, and the AI-use policy (does it require disclosure?).
3. Read the issue and its thread highlights (live: `gh issue view`). Note the one reported problem and any explicit maintainer direction.
4. Read the plan context BEFORE the PR (live: `plan.md`, including `## Deviations`). Write down: (a) the Files list, (b) the in-scope change, (c) every "not in scope" item, (d) every promised deliverable (fix, test, docs, warning), (e) the test plan's scenarios and expected-after results, (f) the repro's trigger and observed before, (g) any deferral or deviation note. The plan comes first so the diff is judged against the plan, not against the description's account of it.
5. Read the diff (live: `git diff main...HEAD`, and `git log --oneline main..HEAD` for commits). Read it before the description, so you see what changed before being told what changed.
6. Read the title and description (live: `pr_draft.md`, title on line 1), then the test evidence (live: `test_evidence.md`).

## Evidence gathering

1. diff-matches-plan: list every file and hunk in the diff. Beside each, write which plan item (b), test, or deviation note (g) covers it, or "unplanned". Then list each promised deliverable (d) and mark it "in diff", "deferred (noted)", or "missing". Flag any hunk that matches a not-in-scope item (c).
2. description-matches-diff: copy every claim in the title and description about what the PR changes or does not change. Beside each, write the hunk that shows it, or "not in diff". For fidelity claims ("exactly as planned", "no changes beyond", "no functional changes outside"), list the unplanned hunks from step 1 that contradict them.
3. test-decisive: pair each test-plan scenario (e) with the test-evidence output that re-runs it. Record the command or input actually run, the before, and the after. Note whether the run uses the repro's trigger (f) or a control or different input. Label each scenario "failure mode" (fails before the fix) or "control" (works before and should stay unchanged). Mark any failure mode with no output as "not shown", and whether a deferral note covers it; a control stated in a sentence is enough.
4. repo-checks-run: pair each repo check from Read order step 2 (suite, lint, type check) with the evidence line reporting its outcome; record "not shown" where none, and copy the reason given for any failure.
5. diff-clean: scan every added and removed line for debug output, commented-out code, dead or unused functions, TODO/FIXME on touched lines, whitespace/indent/import/ordering churn, and duplicated lines. Quote each hit with its file. Note the commit messages.
6. template-and-disclosure: pair each stated ask from Read order step 2 with the description section, checklist item, or diff file that satisfies it, or record "absent". Copy the AI-use disclosure line if one exists.
7. Eval mode: use only bundle text. Live mode: use only the files and commands SKILL.md lists; a missing file means its checks record "absent: <file>".

## Check execution

1. Run the six checks in rubric table order, using only the evidence recorded above; re-open the package only to confirm a quoted line.
2. Grade `pass` only when the pass condition is met outright; grade `fail` as soon as any fail clause applies, quoting the hunk or line.
3. Grade `unclear` only when the evidence the check needs is genuinely absent from the package (not merely thin), and write "absent: <what>".
4. Before failing a check for something missing or skipped, look for a deferral or deviation note in the plan AND a matching disclosure in the description; if both exist, that item does not fail the check.
5. Judge the artifact, not the writing: a terse description over a matching diff passes; a confident one over drift fails. A perfect checklist or decisive evidence never excuses a failure in a different check; grade each check on its own evidence.

## Verdict assembly

1. Apply the verdict rule: accept only if all six checks grade `pass`; any `fail` or `unclear` gives reject.
2. The deciding check is the first failing (or unclear) check in rubric table order. In the summary, quote for it the two things that conflict (for example, the plan's not-in-scope line and the hunk that crosses it).
3. Give every check one evidence line naming the fact that decided it.
4. Live mode: after the checks, list voice-guide breaks in the summary; they do not change the verdict.
5. Emit the JSON block last, checks in table order, with the verdict matching the grades.
