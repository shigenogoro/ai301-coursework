# Evidence guide: where proof lives in a reproduction package

The map for every family a rubric check names. Each section says where
to look in an eval bundle, where to look in live mode, and the
observable condition that separates good from not-ready.

A package has four parts, in this order: the repo-facts block, the
issue (title, body excerpt, opener), the thread highlights, and the two
candidates (the claim comment and the repro report). Read the issue and
thread first: they set the target every candidate line is read
against.

## Environment

Where it lives:

- Eval bundle: the repro report, usually a line starting
  `Environment:` or a table near the top. The target it is read against
  lives in the issue body (the version, OS, build, or driver the
  reporter names), the thread (maintainers or others naming what
  matters, e.g. "works in Debug, crashes in Release"), and the
  repo-facts `latest release` line and `bug reports:` template line
  (the template names what the repo considers environment).
- Live mode: the draft repro comment; the target is on the issue page
  (body and comments) and in the repo's issue template under
  `.github/ISSUE_TEMPLATE/`, plus `README`/docs for how the project is
  run (Python version, database, env vars).

What good looks like:

- The tool's version and the OS/platform are named, plus every factor
  the issue or thread says changes the behavior (a driver on a
  driver-specific bug, the build profile when the thread says the
  failure differs by build, the shell when the bug is shell-specific,
  the code state when the target is the default branch).
- Differences from the target are said out loud: "the issue was filed
  against 13.0.0; behavior is unchanged on 15.2.0" or "the report is
  macOS + fish; mine is Linux + zsh". Newer-than-target with the delta
  stated is fine.
- Not good: no environment line at all; an older version than the one
  the issue was confirmed on, stated without comment (the output then
  describes the old version, not the bug); a different release channel
  (Store release vs git main) presented as confirming the bug there.

## Steps

Where it lives:

- Eval bundle: the repro report's `Steps:` section and its code blocks
  (shell commands, scripts, config files, input files printed with
  `cat`/`printf`). Inputs may also be referenced from the issue ("the
  issue's script verbatim", "the issue's playground link"); the issue
  body in the bundle shows what that input is.
- Live mode: the draft repro comment; referenced inputs should be on
  the issue page or in the public repo at a named commit.

What good looks like:

- Starting state to trigger, with nothing a stranger has to guess:
  the command that triggers the behavior is written out, and every file
  it reads is either shown or is a public input named precisely.
- Terse is fine. Three commands and a printed input file are complete.
- Not good: no commands at all ("I run long sessions and it lags");
  "checked out our company monorepo (private)", "our internal config
  (not shareable)"; steps that drop a setting the issue says the bug
  needs (the driver flag on a Windows-driver issue).

## Behavior shown

Where it lives:

- Eval bundle: the code blocks in the repro report that show output
  from the reporter's own run (terminal output after a `$` command,
  log lines, tracebacks, produced CSS/JSON, parser failures), and the
  report's `Expected:` / `Actual:` lines. The target symptom is in the
  issue body: its quoted error text, exit code, wrong output, or
  crash description.
- Live mode: the same, in the draft repro comment; the target symptom
  is on the issue page.

What good looks like:

- The artifact shows the issue's symptom, not a neighbour of it. Match
  on the kind of failure and its text: `capacity overflow` panic with
  exit 101 is not an `Invalid value for '--line-range'` error with
  exit 1; `Invalid path expression` is not `$b is not defined`; a
  terminal crash is not a screen of escape-sequence text with the
  prompt returning; a blank pane is not a session list showing three
  tabs.
- The trigger is the issue's trigger. Compare the command in the report
  with the command in the issue character by character where it
  matters: range syntax (`:-N` vs `N:`), the bound variable, `=` vs
  `:`. A changed trigger that produces a different message is a
  different bug.
- A control run (same command with the suspected factor removed) that
  behaves correctly is the strongest form: it shows the symptom
  depends on what the issue says it depends on.
- For a cannot-reproduce, good is an artifact of the issue's trigger
  behaving correctly on the reporter's machine (the prompt that did
  render, the marker order that stayed in order).
- Not good: no code block of the reporter's own output; "the screenshot
  I took shows..." with no content; output that proves only the
  program is installed (`--version`, `ls`).

## Honesty

Where it lives:

- Eval bundle: result and certainty sentences anywhere in the claim
  comment and repro report ("I have reproduced", "confirmed", "100%",
  "guaranteed", "I verified the root cause", "this demonstrates it is
  not limited to..."), read against the artifacts found under
  Behavior shown.
- Live mode: the same sentences in the drafts.

What good looks like:

- Every result sentence can be pointed at an artifact that shows it.
  "Actual: 1, 2, 3, 4 as shown above" with those lines above is
  honest; "the crash is confirmed" above a graceful error is not.
- Causes without a shown artifact are hedged ("seems", "looks like",
  "my hypothesis"); a root cause stated as verified needs something
  shown that verifies it (a trace, a timing log, a code excerpt with
  the path exercised).
- An honest cannot-reproduce states the outcome first ("I could NOT
  reproduce"), shows what was run, and names what differed from the
  report's conditions. That is a pass, not a failure.
- Not good: emphatic certainty with no artifact; the narrated result
  contradicting the shown output; reach beyond the evidence (claiming
  a platform or release the evidence does not cover, especially one a
  maintainer in the thread could not reproduce on).

## Comms

Where it lives:

- The claim comment against the issue: the bundle's `Candidate claim
  comment` section read against the issue title, body, and thread
  highlights. Live: the draft claim file against the issue page.
- The repo's rules: the repo-facts `contribution policy` line (which
  names CONTRIBUTING.md, AI_POLICY.md, or an AI section and summarizes
  it) and the `bug reports:` template line. Live: `CONTRIBUTING.md`
  (root, `docs/`, or `.github/`), any `AI_POLICY.md` or
  `AI_USAGE_POLICY.md`, and `.github/ISSUE_TEMPLATE/`. In Path Review,
  `scope.md` house rules also apply (a classmate's claim does not
  block a claim; no piggyback repros).

What good looks like:

- A specific claim: it names something only this issue has (the
  symptom, the file or function the thread points at, the version it
  reproduced on) and one concrete next step (read X, trace Y, test the
  draft patch against both configurations, report back). It promises
  investigation, never a fix, a date, or a guarantee.
- Not good: "+1 any updates?", "assigning myself", "kindly assign it
  to me, I will fix it within 2 days guaranteed", praise-and-reserve
  boilerplate that would fit any issue in any repo.
- AI policy, read in this order:
  1. Does the policy require disclosure of AI use for issues or
     comments, or for "all AI usage in any form"? Then at least one
     comment must disclose the tool or kind of help and its extent
     (e.g. "I used an AI assistant to organize this report; I ran and
     verified every step myself"). Course packages are AI-assisted
     work, so silence here fails.
  2. Is the disclosure ask scoped to pull requests only, or is there
     no disclosure ask? Then the comments need no disclosure.
  3. Does the policy ask that comments be in the contributor's own
     words? A specific first-person comment tied to this issue meets
     it; only interchangeable boilerplate breaks it.
  4. No stated AI policy: pass.
