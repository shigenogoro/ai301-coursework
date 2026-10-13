---
name: pr-precheck
description: Grade a PR package (a candidate pull request read against the plan it claims to implement and the issue that plan belongs to) and decide whether it is ready to submit. Use when checking your own branch, draft PR title, and description before opening the pull request, or when grading an eval package bundle.
---

# pr-precheck: rubric-driven PR grading


## The question

You grade one PR package and answer one question: **is this pull
request ready to submit?** A PR package is a candidate pull request
(its title, description, commit list, unified diff, and test
evidence), read against the plan it claims to implement (including
that plan's deviation notes) and the issue that plan belongs to, plus
the repo's stated standards (PR template, contributing guide, AI-use
policy). Grade exactly one package per run. Do not review code style
for its own sake, do not re-litigate the plan, and do not answer a
different question (is the fix elegant, would I merge it). You answer
by executing `procedure.md`, which applies the checks in `rubric.md`
to evidence located per `references/evidence-guide.md`.

## Inputs and modes

Decide the mode first. If the prompt hands you a package bundle (a
markdown file with Repo facts, Issue, Thread highlights, Plan context,
and Candidate PR sections), you are in eval mode. If the student asks
you to grade their own draft PR, you are in live mode.

**Live mode** (run from the top folder of the student's fork clone,
on their branch). Read these, and nothing else, as the package:

- `scope.md` in this skill directory, first (see the scope seam).
- `plan.md` in the working copy, including its `## Deviations`
  section. A house-chain student reads the house plan and house repro
  pack instead; the same checks grade them.
- The diff: run `git diff main...HEAD` (three dots) for the change
  and `git log --oneline main..HEAD` for the commit list. Only
  committed changes count; uncommitted edits and untracked files are
  not part of the PR. Never treat `plan.md`, `comment.md`,
  `pr_draft.md`, or `test_evidence.md` as part of the diff unless
  `git diff main...HEAD --stat` lists them (if it does, that is debris
  to report).
- `pr_draft.md`: line 1 is the PR title, the rest is the description
  (the repo's PR template, filled in).
- `test_evidence.md`: the captured before/after and check output.
- The issue: `gh issue view <number> --repo <scoped repo> --comments`
  for the body and thread (maintainer direction, prior-art PRs).
- The repo's standards: `.github/PULL_REQUEST_TEMPLATE.md` and
  `docs/CONTRIBUTING.md` in the working copy.
- `voice-guide.md` in this skill directory (see the voice seam).

If a named file is missing, do not hunt for substitutes: grade the
checks that need it as `unclear` and say which file was missing.

**Eval mode**: the bundle text is the whole world. Do not fetch
anything, run no git or gh commands, and read no other file except
this skill's components. Every fact comes from the bundle. Eval mode
always grades a complete package: every check in `rubric.md`, the
full verdict rule.

## The scope seam (live mode only)

In live mode, read `scope.md` before anything else. Take the repo on
its `Repo:` line as the only repo a PR may target, and apply its house
rules (own-fork branch named `<type>/<issue>-<slug>`, one PR per issue
per student, template always used, a classmate's PR does not block
this one) when reading the evidence. If the `Repo:` line still holds a
bracketed placeholder such as `<ORG>/<PATH-REVIEW-REPO>`, stop without
grading and tell the student to fill the `Repo:` line in `scope.md`
with their section's Path Review repo. If the issue URL or the PR's
target repo is not the scoped repo, refuse to grade and say why. Never
guess a scope. In eval mode, ignore `scope.md` entirely.

## The voice seam (live mode only)

In live mode, after grading, read `voice-guide.md` and hold the
outgoing text, the PR title and description in `pr_draft.md`, against
each rule. In the summary, list every rule the draft breaks, quoting
the rule's name and the offending line. Voice notes never change the
verdict: the rubric has no check that reads the voice guide, so a
voice break is advice, not a hold. In eval mode, ignore
`voice-guide.md` entirely.

## Component reads

Read the components in this order before grading:

1. `rubric.md`: the checks table (name, evidence, pass condition,
   weight) and the verdict rule. These are the only checks you grade;
   use their names verbatim in the output.
2. `references/evidence-guide.md`: the map of where each evidence
   family lives in a bundle and in a live working copy, and what good
   looks like.
3. `procedure.md`: execute it as written, step by step. It decides the
   read order, the gathering moves, how each check runs, and how the
   verdict is assembled.

Where the procedure is silent on something you need, do not improvise
a step: make the smallest reading the rubric's text supports and
report the gap in the summary as "procedure gap: ...". If `rubric.md`
has no checks or no verdict rule, or `procedure.md` has no steps,
stop and say so without grading: this tool does not invent checks at
runtime.

## Verdict and output

The verdict is binary: `accept` means ready to submit; `reject` means
hold. There is no third verdict and no score; reservations go in
check evidence lines. Before the JSON you may print a short readable
summary: one line per check (name, grade, evidence), then in live mode
the voice-guide notes and any procedure gaps. End the reply with the
fenced JSON block below, filled in, valid, and last, with nothing
after it. `item` is the PR or issue URL in live mode and the bundle id
(e.g. `pkg-07`) in eval mode; `checks` holds every rubric check in
table order.

```json
{
  "item": "<PR URL or bundle id>",
  "checks": [
    {"name": "<check name>", "grade": "pass|fail|unclear",
     "evidence": "<one line: the fact or quote that decided it>"}
  ],
  "verdict": "accept|reject"
}
```

## Grading discipline

- Evidence first: never grade a check without quoting or naming the
  fact that decided it (a diff hunk, a description sentence, an output
  line). "Looks fine" is not evidence.
- Grade the thing, not the polish: a terse PR whose diff matches the
  plan and whose evidence is decisive is ready; a confident, beautiful
  description over a drifting diff is not. Read the diff yourself; do
  not trust the description's summary of it.
- The rubric decides, not you: if a check passes by its stated
  condition but feels wrong, it passes; note the tension in the
  summary.
- The procedure decides how, not you: follow `procedure.md` and
  report its gaps instead of papering over them.
- Unclear: treat it as the rubric's verdict rule directs. Where the
  rule is silent, `unclear` counts as `fail`: a claim you cannot
  verify from the package is not ready to submit.
- Honesty counts: a shortfall that the plan's deviation notes and the
  description both disclose is scoped work, not a defect.
