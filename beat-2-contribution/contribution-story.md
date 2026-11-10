# Contribution: Implement Jest Tests for Box shadow generator

Path: `beat-2-contribution/contribution-story.md`

This file is Assignment 5, and it is graded at the path above; a copy kept anywhere else in
the repository is not read. **Keep every section header below under its exact name** — the
format criteria grade exactly that. Your course repo link is the whole submission: no tool
files and no evidence uploads are part of Assignment 5.

**Contribution Number:** [1]
**Student:** Sheng-Kai Wen
**GitHub Username:** shigenogoro
**Issue:** https://github.com/Bashamega/WebDevTools/issues/391
**Pull Request:** [GitHub PR link, once opened]

One repository, built across units 5 to 8, telling the whole story of your real
contribution. Fill it as you work, not at the end — the sections below ask for evidence that
is far easier to write down as it happens than to reconstruct in the last weekend.

Contribution Number stays `[1]` unless you make more than one contribution this term; it
just numbers them.

---

## Toolkit

Every story section below, from Why I Chose This Issue through Pull
Request, ends with a Toolkit block: which tool did that phase's work
and how you used it, what it produced, what difficulties or
shortcomings it presented, and what you changed or would change
because of them. Together the blocks are the thread the rubric's
Toolkit points read, and they are the raw material for your unit-9
portfolio, so keep them current as you work rather than
reconstructing them later.

A Toolkit block looks like this (copy it into each story section and
fill it there):

```text
**Toolkit**

- Tool: [which tool did this phase's work, and how you used it]
- What it produced: [described in a sentence or a short excerpt]
- Difficulties: [what fought you or fell short, or "none met"]
- What changed: [the patch, revision, or workaround, what you would
  update, or "nothing"]
```

This section also keeps one short dated entry per week of tool work,
starting below: what you built or changed that week, what broke, and
what you changed because of it. The blocks tell the story where it
happened; these entries are the toolkit's own timeline.

All four entries are graded. Keep every heading below, and fill each
one in the week it belongs to.

**Unit 5: Built issue-scout and a GitHub-wide search strategy; it rejected 8 of 8, and I patched the ranking and three rubric checks**

I turned my unit-1 issue-select skill into issue-scout, with three owner-scoped `gh search issues` queries (FastAPI/Pydantic/SQLAlchemy bugs, LLM/RAG good-first-issues), each traced to a sentence of my fit profile, ranked by good-first-issue label, then fewest comments, then recency. The first scan rejected all five: every one was a llama_index issue that already had an open PR, and low comment counts made them look untouched because duplicate PRs show up as links, not comments. I added a 2-per-repo cap to the ranking, re-pointed two rubric checks (maintainer-responds, maintainer-authored-commit) that graded `unclear` on every real repo because their evidence wasn't where the scout looked, and made no-open-claim count assignees and claim comments again now that the Path Review house rule doesn't apply. The scout also rejected all three of my Issue Selection site picks (two had open PRs, one was an umbrella issue); I checked each failing quote against the issue page and it was right, so the tool held up there, and I now check the Development box before I claim.

**Unit 6: Installed the voice guard with five Upstream rules, fixed two Windows gaps in it, and wrote a 36-line repo memory**

I merged my three voice-guide copies into one canonical guide, added five Upstream rules (claims, questions, pings) with wrong/right pairs, wired the guard as a PreToolUse hook, and wrote `CLAUDE.local.md` for WebDevTools from one scoped read of the box-shadow page and its two imports. Two things broke on Windows: the hook only matched the `Bash` tool, so a `gh issue comment` sent through Claude Code's PowerShell tool skipped the guard, and every real check failed with "the claude CLI is not on PATH" because npm installs `claude.cmd`, which a bare `subprocess.run(["claude", ...])` can't find. I widened the matcher to `Bash|PowerShell` and switched the call to `shutil.which("claude")`, then confirmed both with a piped PowerShell payload (stopped) and a manual `--draft` run (a real verdict). Once it ran, the guard stopped my first claim under my own rule "Promise the next step, never the fix" (the line "and then add tests for ..."), a draft repro-check had already passed; I cut the promise, and the hook logged a pass when I posted.

**Unit 7: [one line on the tool work]**

[2-4 sentences: the ship-gate and your gate manifest. What it produced
on your real branch, what fought you, what changed because of it.]

**Unit 8: [one line on the tool work]**

[2-4 sentences: the PR-monitor and your playbook. What it read, what it
drafted, what you did with the draft.]

---

## Why I Chose This Issue

This issue came from the AI301 Issue Selection site, after a long search. My scout's own scan (owner-scoped queries over FastAPI/Pydantic/SQLAlchemy and LLM/RAG repos) graded five llama_index issues and rejected all five, each already carrying an open PR. Then I took picks from the site in rounds: dna#255 and two ArduPilot issues (all rejected), EdgeTX#368 (accepted, but rated ambitious: C++ firmware with an open design question, the opposite of my profile), and over a dozen more from ArduPilot, Altinn, ChurchCRM and Red-DiscordBot that a free `gh` pre-check showed were already taken by an open PR or a recent claim comment. I graded three Python issues I found myself with a `-linked:pr` search (only quart#483 passed, and it was off-site), and three WebDevTools test issues from the site. The scout accepted #391 with difficulty **straightforward**: every required check passed, with no assignee, no linked PR, and only a bot comment; the owner had merged sibling Jest-test PRs (#692, #696, #697) in the week before I graded; and the code is one file, `src/app/customizer/box-shadow-generator/page.jsx`.

It isn't Python, which is where my profile points, but it fits the sentence of my profile I care most about: working inside someone else's codebase and writing the test the way the project already does. Jest, React Testing Library, CI and two model test files are already there, and it runs with `npm ci && npx jest` and no heavy environment. I want to learn this repo's testing conventions well enough that my test reads like theirs, and to find out whether writing tests surfaces real bugs: reading the page I already suspect a stray space in the CSS output and four sliders sharing one `id`. An honest read of the scout: its rubric was right every time I checked a failing quote against the issue page, but its ranking and my site picks kept walking into taken issues. Comment count can't see a linked PR, and the claim check reads only comments, not an offer in the issue body or a bot's "is-working" label. The cheapest fix turned out to be GitHub's `-linked:pr` search qualifier, which I'd add to my strategy's queries. Claim comment: https://github.com/Bashamega/WebDevTools/issues/391#issuecomment-6757338718

**Toolkit**

- Tool: issue-scout, run in direct mode on each batch of site picks (`claude "issue-scout: grade <urls>"`) after a free `gh` pre-check for open PRs, assignees and claim comments, plus one full scan in Unit 5.
- What it produced: 0/5 accepted on the scan; 0/3 then 0/3 again on my first picks; accept on EdgeTX#368 (ambitious), quart#483 (moderate), and WebDevTools #391 and #385 (straightforward) and #398 (moderate). On #391 every required check passed and the note read "straightforward."
- Difficulties: most wild good-first-issues were already taken, and the scout only found out at grading time (about $0.20 each); `maintainer-responds` graded `unclear` on WebDevTools because no issues were opened in its 30-180 day sample window; claim signals in an issue body or a bot label slipped past `no-open-claim`.
- What changed: in Unit 6 I replaced my strict `scope-is-bounded` check with `scope-feasible` plus a difficulty note, so open edges inform instead of rejecting. Re-grading last week's picks changed the reasons but not the verdicts. I started running a free pre-check before paying to grade, and logged three more patches in `scan-notes.md`: add `-linked:pr` to the queries, read the issue body and bot labels for claims, and fall back to recent PR reviews when there are no recent issues to sample.

---

## Understanding the Issue

**Problem Description**

[In your own words, what is broken or missing?]

**Expected Behavior**

[What should happen?]

**Current Behavior**

[What actually happens?]

**Affected Components**

[Which parts of the codebase are involved?]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Reproduction Process

**Environment Setup**

Windows 11 Pro (10.0.26300) in Git Bash, Node v24.16.0, npm 11.18.0, Bashamega/WebDevTools `main` at `3b10434` ("test: add Jest tests for Image Color Picker (#696)"). I forked the repo to `shigenogoro/WebDevTools`, cloned it, added `upstream`, and installed with `npm ci`; Jest and React Testing Library come from the repo's own `package.json`. The one Windows catch: the `npm test` script sets `NODE_OPTIONS` with Unix syntax, which works in Git Bash but not PowerShell (`contributing.md` gives the PowerShell form), so I ran Jest directly as `NODE_OPTIONS=--experimental-vm-modules npx jest`. `npm ci` warned that two packages' install scripts weren't allow-listed; the suite ran fine without them.

**Steps to Reproduce**

1. `git clone https://github.com/Bashamega/WebDevTools.git && cd WebDevTools && git checkout 3b10434 && npm ci`
2. Run the suite as-is: `NODE_OPTIONS=--experimental-vm-modules npx jest`
3. Look for any existing test of the page: `grep -rniE "box-shadow-generator|box shadow" __tests__ src --include='*.test.*'`
4. Measure coverage of the page, with a tested page as a control: `NODE_OPTIONS=--experimental-vm-modules npx jest --coverage --collectCoverageFrom='src/app/customizer/LoremIpsumGenerator/page.jsx' --collectCoverageFrom='src/app/customizer/box-shadow-generator/page.jsx'`
5. Observed: the suite passes (11 suites, 54 tests), grep finds nothing (exit 1), and `box-shadow-generator/page.jsx` is 0% covered on every column with lines 3-202 unexecuted, while the control page is at 96%.

**Reproduction Evidence**

- **Commit showing reproduction:** none (the reproduction is a coverage measurement on upstream `3b10434`; nothing to commit yet)
- **Screenshots/logs:**

  ```
  Test Suites: 11 passed, 11 total
  Tests:       54 passed, 54 total

  $ grep -rniE "box-shadow-generator|box shadow" __tests__ src --include='*.test.*'; echo "exit=$?"
  exit=1
  $ ls __tests__/customizer
  LoremIpsumGenerator  Readme-generator

  File                  | % Stmts | % Branch | % Funcs | % Lines | Uncovered Line #s
   LoremIpsumGenerator  |   96.15 |      100 |     100 |      96 |
    page.jsx            |   96.15 |      100 |     100 |      96 | 18
   box-shadow-generator |       0 |        0 |       0 |       0 |
    page.jsx            |       0 |        0 |       0 |       0 | 3-202
  ```
- **My findings:** the issue's claim holds on today's `main`: nothing tests the page. Reading the code for the test, I found two things I've only read, not yet confirmed with a test: `InputRange` hardcodes `id="h-offset"` and `name="h-offset"` on all four sliders and none has a label, so a test can only select them by position (`getAllByRole("slider")`); and with inset off, `cssShadowStyle` builds `... #00000080 ;` with a space before the semicolon. Tests will either confirm these or show I misread them; fixing app code is out of this issue's scope unless the owner agrees.

**Toolkit**

- Tool: repro-check, run on the claim draft alone (`claude "repro-check: grade my draft claim comment in claim-draft.md for issue ..."`), then on the claim plus `repro-draft.md` together.
- What it produced: accept on the claim (twice, before and after the voice-guard revision) and accept on the claim plus repro, with all required checks passing and the preferred `control-shown` check passing because of the Lorem Ipsum 96% row. It also checked my stray-space observation against the page source.
- Difficulties: on the claim, repro-check and the voice guard disagreed: repro-check passed "and then add tests for ...", and the guard stopped it as a promised fix. On a test-only issue, "reproduce" means measuring an absence (coverage), and the rubric's checks fit that only loosely.
- What changed: I cut the promise from the claim. On repro-check's notes, I pasted the grep exit status and the `ls` output instead of describing them, and I switched step 1 to clone upstream at `3b10434` rather than my fork, so a stranger doesn't have to trust my fork.

---

## Solution Approach

**Analysis**

[Your analysis of the root cause: what is causing the issue, traced
to the files and functions involved.]

**Proposed Solution**

[High-level description of your fix approach, and what you are
deliberately NOT changing.]

**Implementation Plan**

1. [Modify file X to do Y]
2. [Add or change Z]
3. [Update tests]

[Record deviations here as they happen: what changed mid-build and
why. A recorded deviation is honest work; silent drift is not.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Testing Strategy

[What observable checks prove the fix: your reproduction steps re-run
against the built change (before and after), and the repo's own test
suite or checks with the outcome shown. "Tests pass" with nothing
observable named is not a strategy.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Implementation Notes

**2026-11-09: claim, reproduction, report-back**

I claimed #391 after the voice guard made me cut "and then add tests for …" from my first draft. Forked, cloned, `npm ci`, and measured the gap: the suite passed (11 suites, 54 tests) and `box-shadow-generator/page.jsx` was at 0% coverage, lines 3-202. Reading the page for the tests, I suspected two bugs: all four sliders share `id="h-offset"` with no labels, and the CSS string looked like it ended in `#00000080 ;`. I posted the report-back on the issue the same evening and asked the owner one question: fix the trailing space in this PR, or open a separate issue? The guard stopped that draft once too, because I'd written "passes (11 suites, 54 tests)" without pasting the output.

**2026-11-09: tests written on a local branch**

On `test/box-shadow-generator-391` I wrote 10 tests in `__tests__/customizer/box-shadow-generator/page.test.jsx`, modelled on the Lorem Ipsum tests: rendering and defaults, the four sliders, color, inset on and off, both copy buttons (success, plus a rejected clipboard write that must log and not confirm), and the dark-mode toggle including a stored theme. Decisions: I mocked `sweetalert2`, since no existing test had, and selected the sliders by position because they have no labels. I wrote the default-CSS assertions as `#00000080\s*;` so they pass whichever way the owner answers about the trailing space. A throwaway probe test confirmed both suspicions (`"box-shadow: 0px 8px 24px 0px #00000080 ;"`, and four `"h-offset"` ids), and I deleted the probe afterwards. Coverage went from 0% to 96.66% (only line 53, the Tailwind copy error path, is uncovered), and the full suite passes at 12 suites and 64 tests.

Two wrong turns on Windows, both in the husky pre-commit hook. First, it flagged 193 files I hadn't touched: `core.autocrlf=true` had checked everything out with CRLF, and Prettier wants LF, so I set `core.autocrlf=false` in this clone and re-checked the files out. Second, its `npm run test` step failed with "'NODE_OPTIONS' is not recognized", because npm runs scripts through cmd.exe. I didn't skip the hook; I committed with `npm_config_script_shell` pointed at Git Bash, and both hook steps passed (commit `c3f5abb`, not pushed yet).

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Pull Request

**PR Link:** [GitHub PR URL when opened]

**PR Description:** [what the PR says; much of the content above
adapts into it]

**Maintainer Feedback:**

- [Date]: [feedback received, or "none yet"; silence is a normal
  state and costs you nothing]
- [Date]: [how you addressed it]

**Status:** [Awaiting review / Iterating / Merged / Closed. The
status is a fact you record, never a grade: the PR is graded as
opened.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Learnings and Reflections

**Technical Skills Gained**

[What you learned technically, named concretely.]

**Challenges Overcome**

[What was hard and how you solved it; point at the real events, the
Toolkit blocks above are full of them.]

**What I'd Do Differently Next Time**

[Reflection on your process.]

---

## Resources Used

[What actually helped, not a reading list. List things this story
already shows you using: the doc you followed to set the environment
up, the thread that explained the bug, the person who answered you.
One real entry beats ten plausible ones.]

- [Link to documentation that helped]
- [Discussion, issue, or post that helped]
