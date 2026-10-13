# Unit 4 — Test and Submit

Path: `beat-1-sandbox/unit-4/pull-request.md`

Record of the pull request you opened against the Path Review repo, and of the evaluation
runs that produced `eval-run.txt`. This file is graded at the path above; a copy kept
anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your pull request

**Pull request**

https://github.com/codepath/pathreview-ai301-fa26-s3/pull/184

**Branch**

fix/61-health-check-text-sql

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

1. Full run 1: `agreement: 19/19 scored items`. pkg-05 came back `ERROR` ("claude exited 1: Warning: no stdin data received in 3s"), so the harness treated it as partial and did not write the file. Every graded package agreed.
2. Full run 2 (3 workers): `agreement: 18/19 scored items`. pkg-05 hit the same `ERROR` again, and pkg-19 was `NO  failed: test-decisive`. The pkg-05 error came from Windows: Python sent the prompt to `claude` in my locale encoding, and pkg-05's box-drawing table broke it. Setting `PYTHONUTF8=1` for the harness fixed it, with no change to my skill.
3. Partial `--only pkg-05,pkg-19,pkg-07,pkg-14,pkg-04,calib-04 --include-calibration`, after loosening test-decisive for control runs: `agreement: 5/5 scored items` (calib-04 also agreed, `reject`).
4. Full run 3 (confirming, `--save-run`): `agreement: 18/20 scored items  (bar: 18/20: PASS)`, with `categories: clear-accept 5/7  not-tested 4/4  silent-drift 4/4  standards-wall 2/2  unreviewable 3/3`. This is the run in `eval-run.txt`.

**Package analysis**

pkg-11 (BurntSushi/ripgrep#3477). My rubric decided `reject`, and the gold label is `accept`. The only failing check was template-and-disclosure, with the evidence "Policy requires AI disclosure; description says only 'this change was AI-assisted with me reviewing and understanding every line' and does not name the tool." My rubric read it that way because I wrote the disclosure clause as "the description contains one naming the tool and the extent of help". That wording comes from ghostty's policy in pkg-20 ("stating the tool used and the extent of the assistance"). ripgrep's policy only asks for a human in the loop who understands the work, and for comments in the person's own words, so pkg-11's own-words line meets ripgrep's ask. My rubric applied the strictest repo's rule to every repo. The fix is to grade disclosure against what each repo's own policy asks. I didn't make that change because I had already used my three full runs.

**Check rationale**

| test-decisive | The test-evidence section's before/after, read against the plan's test plan and the repro evidence's trigger and observed output. | The evidence re-runs the plan's repro trigger (the failing path, not a control or a different input) and shows an observable after-fix result (output text, exit code, status, value) that differs from the before (the before may be quoted from the repro). Every failure mode or bug scenario the plan's test plan names (each input that fails before the fix) is shown with output, or its omission is disclosed as deferred in both plan and description. Controls (inputs that already work before the fix and should stay unchanged) and the repo's suite may be reported in a sentence without output. Fail if the evidence is only "tested locally", "works now", "verified on my machine", or "tests pass" with no repro output; if it re-runs only a control or the unchanged path (e.g. the single-file case when the bug is multi-file, a different request than the issue's); or if it silently skips a failure mode the plan's test plan named. Do not fail only because a control is asserted without output. | required |

It reads this way because of pkg-19. My first version said "Every failure mode or scenario the plan's test plan names is shown". In run 2, pkg-19 (yq) failed test-decisive with "the plan's two controls are only asserted ('Controls ... unchanged') with no command or output". A control is an input that already worked before the fix, so leaving out its output doesn't hide whether the bug is fixed. I split the scenarios into failure modes, which still need output, and controls, which can be stated in a sentence. I rejected the simpler option of dropping the "every scenario" clause entirely. calib-04 (fd) is a reject exactly because the plan's second failure mode, the `--exec` abort, is never shown, and pkg-07 (golangci-lint) is a reject because it re-runs only the single-file control. The clause "re-runs only a control or the unchanged path" keeps that case failing.

**Trade-offs**

Loosening test-decisive for controls could have flipped the not-tested rejects, so I re-ran canaries with `--only`. pkg-04, pkg-07 and pkg-14 (not-tested) and calib-04 all stayed `reject`, and pkg-19 flipped to `accept`. All four not-tested packages agreed again in the confirming full run (`not-tested 4/4`). What I accept it will still miss: in run 3, pkg-05 (nushell) failed test-decisive because the grader read "Same-key redefine prints the one-time warning" as a failure mode asserted without output, when the gold treats it as a side check. The line between a failure mode and a control is a judgment the grader makes per package, so a package whose secondary scenario is asserted in a sentence can still land on either side.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/pr-precheck/`.
