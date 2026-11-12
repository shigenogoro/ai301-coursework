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
**Pull Request:** https://github.com/Bashamega/WebDevTools/pull/701

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

**Unit 7: Installed the ship-gate with a three-check manifest; it passed my branch three times, after I fixed three Windows bugs in the guard tooling**

My manifest lists the repo's own CI checks (`npm run format:check`, Jest, and Jest with coverage, from `.github/workflows/`), and the ship-gate ran them plus my pr-precheck on `feature/box-shadow-generator-tests` three times, passing all three checks and all six pr-precheck checks each time. What fought me was Windows: the gate ran commands through cmd.exe, so CI's `npm test` (Unix `NODE_OPTIONS=`) had to become `node --experimental-vm-modules node_modules/jest/bin/jest.js`; its hook matched only `Bash` and called a bare `claude` that can't find npm's `claude.cmd` (last week's voice-guard bugs again); the voice guard crashed reading Jest's `●` as cp1252; and Prettier checked my untracked working files, so the template `ship-manifest.md` itself failed `format:check`. I patched all three scripts, formatted every working file, and swapped my voice-guide symlinks for pointer files after plan-check's Glob silently skipped them. The gate's pr-precheck notes caught a ticked "no new warnings" box with no evidence, and my own second review caught a false line in my AI disclosure ("I ran every command above myself"), and I fixed both before PR #701 opened.

**Unit 8: Wrote my playbook from measured response times; the PR monitor drafted a wait note, then a review reply I rewrote and posted**

I installed the PR monitor and wrote my playbook from the repo's own numbers: four recent merged outside PRs (#581, #692, #696, #697) got the owner's first touch within 0.0-0.7 days while #626-#628 have sat since April, so my nudge threshold is 7 quiet days and bot comments don't count as activity. The monitor first crashed on Windows by decoding `gh`'s output as cp1252 (it died on the `●` in my PR description), so I patched its subprocess calls to UTF-8 and to find `claude.cmd`, like the other two hooks. Its first full run read my bot rule and drafted a wait note about CodeRabbit's "Trivial" nitpick, which `--state` had mislabelled as human "FEEDBACK-IN", and I sent nothing until the owner requested changes ("Please apply the code rabbit nit pick comment"). The second run drafted a "Done in 5b92a9f" reply with placeholders where the real output belonged; I filled them in, corrected my description's wrong claim that jsdom couldn't check the preview style, and fixed the three lines the voice guard stopped (no command on the break-it run, no environment, nothing said about what I hadn't covered) before posting.

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

The Box Shadow Generator page has no Jest tests. Its CSS and Tailwind outputs, its sliders, color and inset controls, both copy buttons and its dark-mode toggle could break, and CI's `npm test` would still pass, because no test ever renders the page.

**Expected Behavior**

A test file at `__tests__/customizer/box-shadow-generator/` (mirroring the page's `src/app` path, as contributing.md asks) that covers what the issue's task list names: rendering, user interactions, state changes and the whole flow, and that passes locally and in CI.

**Current Behavior**

On `main` at `3b10434` there is no test for the page anywhere, and a coverage run leaves every line of `page.jsx` unexecuted: 0% across the board, lines 3-202 uncovered.

**Affected Components**

`src/app/customizer/box-shadow-generator/page.jsx` (the page, all of its state, and both outputs); `src/components/Input/InputRange.jsx` (the four sliders); `src/components/navbar.jsx` (the theme toggle and `localStorage`); the `sweetalert2` and `navigator.clipboard` calls behind the copy buttons. The new test goes in `__tests__/customizer/box-shadow-generator/page.test.jsx`. No app code changes.

**Toolkit**

- Tool: my repo-memory file, `CLAUDE.local.md`, written from one scoped read of the page and the two components it imports, instead of mapping the whole repo.
- What it produced: a 36-line map: where the state lives, what the copy buttons call, which existing tests to copy (Lorem Ipsum stubs the clipboard in `beforeEach`), and that the sliders have no labels.
- Difficulties: the page alone didn't tell me how to select the sliders. I had to open `InputRange.jsx` to find that all four share `id="h-offset"` and have no label.
- What changed: I recorded "select the sliders by position with `getAllByRole("slider")`" in the memory file, so later sessions start from that instead of rediscovering it.

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

There is no runtime bug behind #391: the gap is that `src/app/customizer/box-shadow-generator/page.jsx` never got a test, while its sibling customizer pages did (Lorem Ipsum #697, Readme generator #692, Image Color Picker #696). CI runs `npm test` on every PR (`.github/workflows/jest_tests.yml`), but nothing renders this page, so a regression in it would pass CI. Reading the page for testability:

- All of its state lives in one component: `shadow` (`hOffset 0, vOffset 8, blur 24, spread 0, color "#00000080", inset false`) and `isDarkMode`, both from `useState`.
- Its two outputs, `cssShadowStyle` and `tailwindShadowStyle`, are derived from `shadow` with `useMemo` and rendered as text in two `<h3>`s. A test can read them directly.
- Its side effects are `navigator.clipboard.writeText` (jsdom has no clipboard), `Swal.fire` from `sweetalert2` after a successful copy, `console.error` after a failed one, and `NavBar`'s `localStorage` "theme" read and write.
- The four sliders come from `src/components/Input/InputRange.jsx`, which gives every one of them `id="h-offset"` and no label. A test can only find them by position, with `getAllByRole("slider")`.

Reading the page also turned up two real bugs. A throwaway probe test (deleted afterwards) that rendered the page and printed what it found confirmed both:

```
CSS="box-shadow: 0px 8px 24px 0px #00000080 ;"
IDS=["h-offset","h-offset","h-offset","h-offset"]
```

The stray space before `;` comes from the template literal in `cssShadowStyle` (`page.jsx`, around line 62: `${shadow.color} ${shadow.inset ? "inset" : ""};`), and the duplicate ids come from `id="h-offset"` being hardcoded in `InputRange.jsx`. On 2026-11-10 the owner answered my question on #391: "each fix in a separate pr please".

**Proposed Solution**

Add one test file, `__tests__/customizer/box-shadow-generator/page.test.jsx`, which mirrors the `src/app` path as contributing.md asks and follows the Lorem Ipsum test's style. It mocks `sweetalert2`, stubs `navigator.clipboard` in `beforeEach`, and selects the sliders by position. The default-CSS assertions accept the string with or without the stray space (`#00000080\s*;`), so this PR passes whether or not the space fix lands first.

The issue's last task, "Update the documentation to include instructions on running the tests", is already covered: contributing.md's "Run the Tests" section (added since the issue was filed) gives `npm test`, `npm test -- <folder>` for one folder, coverage, and the PowerShell form. So this PR adds no docs.

Deliberately NOT changing: `page.jsx`, `InputRange.jsx`, the Jest config, `package.json`, or contributing.md. The stray space and the duplicate slider ids are real bugs, but per the owner each fix gets its own PR, so neither is fixed here.

**Implementation Plan**

1. Add `__tests__/customizer/box-shadow-generator/page.test.jsx`, modelled on `__tests__/customizer/LoremIpsumGenerator/page.test.jsx`.
2. Rendering: the heading, four sliders, an unchecked inset box, both copy buttons, and the default values in the slider labels and both outputs.
3. Interactions: each slider updates its label and both outputs; the color picker updates the label and both outputs; inset adds `inset` to both outputs and removes it when unchecked.
4. Copy buttons, with `navigator.clipboard` stubbed and `sweetalert2` mocked: Copy CSS and Copy TailwindCSS each write the exact output string and fire a success alert; a rejected write logs `Failed to copy text:` and shows no alert.
5. Theme: the NavBar toggle switches the page's classes and saves `theme` to `localStorage`; a stored dark theme applies on load.
6. Run the full suite, the coverage run and Prettier, then open the PR with `Fixes #391`. Expected results: the full suite goes from 11 suites / 54 tests to 12 suites / 64 tests, all passing; coverage of `box-shadow-generator/page.jsx` goes from 0% (lines 3-202 uncovered) to about 97% statements, with only line 53 (the Copy TailwindCSS error path) uncovered; `npm run format:check` passes.
7. After that, take the stray space and the duplicate slider ids up separately, one fix each, as the owner asked.

Deviation, recorded: I wrote the tests (steps 1-5) in Unit 6, before this plan existed, so the plan describes branch commit `0ea90cb` rather than coming before it. I also renamed the branch from `test/box-shadow-generator-391` to `feature/box-shadow-generator-tests` to match contributing.md's `feature/your-feature-name`.

Deviation, recorded 2026-11-11: after the owner asked me to apply CodeRabbit's review, steps 2 and 3 also assert the preview box's inline `boxShadow` (on load, after the sliders and color change, and with inset on and off), in a second commit, `5b92a9f`. Before that I'd left the preview out of the plan on the untested assumption that jsdom couldn't check it.

**Toolkit**

- Tool: plan-check, run from my clone on `plan.md` and a draft plan comment in `plan-comment.md` (`claude "plan-check: grade my plan in plan.md and draft comment in plan-comment.md for issue …"`), twice.
- What it produced: accept both times, with all six checks passing. The first run flagged three gaps that didn't change the verdict: my plan never addressed the issue's "update the documentation" task, step 6 gave no expected numbers, and I called both bugs "confirmed" without showing the probe output. The second run caught two voice slips: an unsourced "a probe render confirmed", and "I'll send … as its own PR", which promises a fix.
- Difficulties: on the first run it reported "no voice-guide.md in any skill folder", even though `plan-check/voice-guide.md` was there as a symlink. Its file search (Glob) doesn't follow symlinks on Windows, so my voice rules were silently skipped. Its procedure also assumes a bug with a before/after and a risks section, and a test-only issue has neither, so it had to improvise.
- What changed: I replaced the three skills' voice-guide symlinks with the one-line pointer file INSTALL.md offers as a fallback, and the second run followed it. In the plan I added the docs finding (contributing.md's "Run the Tests" section, added in #692 on 2026-11-04, already covers it), the expected before/after numbers, and the probe output. I fixed both voice slips in the comment, which I'm not posting.

---

## Testing Strategy

This issue adds tests rather than fixing behavior, so "before and after" means the coverage run from my reproduction, re-run on the branch, plus proof that the new tests would catch a real regression. Everything ran in a fresh cmd.exe at the clone root, the same shell the ship-gate uses.

1. **The reproduction, re-run.** `node --experimental-vm-modules node_modules/jest/bin/jest.js --coverage --collectCoverageFrom=src/app/customizer/box-shadow-generator/page.jsx`. On `main` (`3b10434`): `page.jsx` at 0% on every column, lines 3-202 uncovered, 11 suites / 54 tests. On the branch (`0ea90cb`, and unchanged after the review commit `5b92a9f`): 96.66% statements, 100% branches, 93.75% functions, only line 53 uncovered, 12 suites / 64 tests.
2. **The tests decide something.** I temporarily removed `inset_` from `tailwindShadowStyle` in `page.jsx` and ran the new file. The result, on `0ea90cb`, was `● … › checking inset adds it to both outputs, unchecking removes it`, `Tests: 1 failed, 9 passed, 10 total`. Then I restored the page with `git checkout`. After review I did the same for the new preview assertions, dropping `inset` from the preview's style expression only, and the inset test failed with `Expected: "0px 8px 24px 0px #00000080 inset"`, `Received: "0px 8px 24px 0px #00000080"`.
3. **The repo's own checks**, as in my ship manifest and taken from `.github/workflows/format.yml` and `jest_tests.yml`: `npm run format:check` printed "All matched files use Prettier code style!", the full Jest suite passed 12/12 suites and 64/64 tests, and the coverage run passed the same. The husky pre-commit hook passed both of its steps when I committed.
4. **Scope.** `git diff --stat main...HEAD` shows one file across both commits: `1 file changed, 212 insertions(+)`.

The 10 tests: renders the heading, the controls, and both copy buttons; starts from the default shadow; moving each slider updates its label, both outputs, and the preview; picking a color updates the label, both outputs, and the preview; checking inset adds it to both outputs and the preview, unchecking removes it; Copy CSS copies the CSS rule and confirms it; Copy TailwindCSS copies the Tailwind class and confirms it; a failed copy logs the error and shows no confirmation; the toggle switches to dark and back, and saves each choice; a stored dark theme is applied on load.

Not covered: line 53, the Copy TailwindCSS failure path, whose twin for Copy CSS is tested; and the page in a real browser. Until review I also listed the preview box's inline `boxShadow` here, saying jsdom couldn't check it. That was wrong: jsdom reports it exactly, and `5b92a9f` asserts it.

**Toolkit**

- Tool: the ship manifest's three checks, run by hand in a fresh cmd.exe, plus a one-line mutation of `page.jsx` to test the tests. The evidence is collected in `test_evidence.md`.
- What it produced: before and after coverage (0% to 96.66%), suite counts (54 to 64 tests), a failing run under the mutation, and all three manifest checks passing.
- Difficulties: on a test-only issue there's no failing test to show "before", because coverage measures an absence. And `npm test`, the command CI uses, can't run in cmd.exe at all.
- What changed: I added the mutation check, so the evidence shows the tests catch a regression rather than just executing lines. In the manifest I wrote the Jest rows as `node --experimental-vm-modules node_modules/jest/bin/jest.js`, which is what `npm test` runs, in a form cmd.exe accepts, and said so in each row's Source.

---

## Implementation Notes

**2026-11-09: claim, reproduction, report-back**

I claimed #391 after the voice guard made me cut "and then add tests for …" from my first draft. Forked, cloned, `npm ci`, and measured the gap: the suite passed (11 suites, 54 tests) and `box-shadow-generator/page.jsx` was at 0% coverage, lines 3-202. Reading the page for the tests, I suspected two bugs: all four sliders share `id="h-offset"` with no labels, and the CSS string looked like it ended in `#00000080 ;`. I posted the report-back on the issue the same evening and asked the owner one question: fix the trailing space in this PR, or open a separate issue? The guard stopped that draft once too, because I'd written "passes (11 suites, 54 tests)" without pasting the output.

**2026-11-09: tests written on a local branch**

On `test/box-shadow-generator-391` I wrote 10 tests in `__tests__/customizer/box-shadow-generator/page.test.jsx`, modelled on the Lorem Ipsum tests: rendering and defaults, the four sliders, color, inset on and off, both copy buttons (success, plus a rejected clipboard write that must log and not confirm), and the dark-mode toggle including a stored theme. Decisions: I mocked `sweetalert2`, since no existing test had, and selected the sliders by position because they have no labels. I wrote the default-CSS assertions as `#00000080\s*;` so they pass whichever way the owner answers about the trailing space. A throwaway probe test confirmed both suspicions (`"box-shadow: 0px 8px 24px 0px #00000080 ;"`, and four `"h-offset"` ids), and I deleted the probe afterwards. Coverage went from 0% to 96.66% (only line 53, the Tailwind copy error path, is uncovered), and the full suite passes at 12 suites and 64 tests.

Two wrong turns on Windows, both in the husky pre-commit hook. First, it flagged 193 files I hadn't touched: `core.autocrlf=true` had checked everything out with CRLF, and Prettier wants LF, so I set `core.autocrlf=false` in this clone and re-checked the files out. Second, its `npm run test` step failed with "'NODE_OPTIONS' is not recognized", because npm runs scripts through cmd.exe. I didn't skip the hook; I committed with `npm_config_script_shell` pointed at Git Bash, and both hook steps passed (commit `c3f5abb`, not pushed yet).

**2026-11-10: owner's answer, ship-gate, plan, evidence**

The owner answered on #391: "Feel free to open prs but each fix in a separate pr please." So this PR stays test-only, and the stray space and the duplicate slider ids each get their own later. I renamed the branch to `feature/box-shadow-generator-tests`, to match contributing.md's `feature/your-feature-name`.

I installed the ship-gate and found the same two Windows gaps the voice guard had. The hook matched only `Bash`, and the pr-precheck call used a bare `claude`, which can't find npm's `claude.cmd`. I patched both and confirmed a PowerShell payload is now stopped. Writing the manifest showed that the gate runs checks through cmd.exe, so `npm test` (Unix `NODE_OPTIONS=`) can't be a row, and that Prettier checks my untracked working files too: the template `ship-manifest.md` itself failed `format:check`. Its `.git/info/exclude` entry hides it from git, not from Prettier. I now run `prettier --write` on every working file I make.

plan-check accepted the plan twice. The second run is the one that actually read my voice guide, after I swapped the symlinks for pointer files. The mutation check (dropping `inset_`) failed exactly one test, as it should.

**2026-11-10: a second review before opening the PR**

Before opening the PR I reviewed the test file and the PR draft again, and fixed four things.

- Test file: the color test only checked `toHaveTextContent("#ff0000")`, which would pass even if the color landed in the wrong place, so it now matches the whole CSS string like the other tests do.
- Test file: the `console.error` spy was restored only when its test passed, so a failure would have leaked it into later tests. An `afterEach(jest.restoreAllMocks)` now restores it either way.
- PR draft: the before/after block was my own condensed layout, so I swapped in the coverage table exactly as Jest prints it.
- PR draft: "which every suite on `main` prints" claimed more than I'd checked, so it now says `main` prints the same warning.

I also caught a sentence in the AI disclosure that wasn't true ("I ran every command above myself") and rewrote it to say what actually happened. The voice guard had stopped the draft once more first, under "A cause is a hypothesis until the output shows it", until I quoted `page.jsx` line 62 as the evidence. I amended the commit to `0ea90cb` (202 lines, still unpushed). The mutation check still fails exactly one test, and the ship-gate passed again.

**2026-11-10: PR opened, monitor installed**

I opened PR #701 through Claude Code. The ship-gate reused its 10:48 PASS, and CI passed prettier and test; Vercel's "Authorization required to deploy" also shows on the merged #696. I installed the PR monitor, patched its Windows encoding bug, and wrote the playbook from measured owner response times. CodeRabbit left one "Trivial" nitpick. The monitor drafted a wait note, and I posted nothing: no human maintainer has replied yet, and my nudge threshold is 2026-11-17.

**2026-11-11: review round 1**

The owner requested changes: apply CodeRabbit's nitpick, which asks for assertions on the preview's `boxShadow`. My PR description had said jsdom couldn't check that style reliably. I'd never tested that claim, and a probe showed it was wrong: jsdom reported `"0px 8px 24px 0px #00000080"`, then `"5px …"`, `"… #ff0000"`, and `"… inset"` after each interaction. I added a `previewShadow(container)` helper and five assertions in a new commit (`5b92a9f`), rather than amending the pushed one, so the owner can see exactly what changed. Dropping `inset` from the preview expression alone failed the inset test, so the new assertions decide something. The full suite stayed at 12 suites / 64 tests, and coverage stayed at 96.66%. I updated the PR description (the "Not covered" line, the corrected jsdom claim, and a note that the old break-it output ran on `0ea90cb`), then posted the reply through the voice guard after three stops.

**Toolkit**

- Tool: Claude Code in my clone, with `CLAUDE.local.md` loaded each session, the husky pre-commit hook, and a throwaway probe test.
- What it produced: the 10-test file, the branch commit (`c3f5abb`, amended to `0ea90cb` after my own review), the review-round commit `5b92a9f`, each with the hook passing, the probe outputs (the two bugs, and the preview's `boxShadow` in jsdom), and the running notes above.
- Difficulties: on Windows the repo's own hook failed twice for reasons that had nothing to do with my change: CRLF line endings made Prettier flag 193 untouched files, and cmd.exe can't parse `NODE_OPTIONS=` in `npm test`. The course hooks had the same platform gaps.
- What changed: I set `core.autocrlf=false` in the clone, committed with `npm_config_script_shell` pointed at Git Bash instead of skipping the hook, and recorded both fixes in `CLAUDE.local.md` so later sessions don't rediscover them.

---

## Pull Request

**PR Link:** https://github.com/Bashamega/WebDevTools/pull/701

**PR Description:** "test: add Jest tests for Box Shadow Generator", opened 2026-11-10 from `shigenogoro:feature/box-shadow-generator-tests` into `Bashamega:main`, with `Fixes #391`. It's one file, `__tests__/customizer/box-shadow-generator/page.test.jsx`, in two commits: `0ea90cb` (+202, the tests) and `5b92a9f` (the preview assertions from review round 1), +212 in total. The description says what the 10 tests cover (rendering and defaults, the sliders, color, inset, both copy buttons including a failed clipboard write, and the theme toggle), and why the issue's docs task needed no change (contributing.md's "Run the Tests" section from #692). It includes:

- the coverage table exactly as Jest prints it, before (0%, lines 3-202, 54 tests) and after (96.66%, line 53 uncovered, 64 tests)
- the mutation check (dropping `inset_` fails exactly one test)
- all three checks with their exact commands
- what isn't covered
- the two bugs I found and deliberately left for separate PRs, with the probe output and `page.jsx` line 62 / `InputRange.jsx` line 9 as evidence
- an AI-use note in my own words

On 2026-11-11 I updated it after review: the interactions bullet now includes the preview, the "Not covered" line no longer lists the preview and says plainly that my jsdom claim was wrong, and the old break-it output is marked as run on `0ea90cb`.

It answers every item of the repo's PR template. Both "Type of change" boxes are left unticked with an N/A reason, since this is a test-only change. CI on the PR: prettier pass, test pass, greet and moderate pass. Vercel shows "Authorization required to deploy", the same as on the merged #696, because fork PRs need the owner's approval to deploy a preview.

**Maintainer Feedback:**

- 2026-11-10: none yet from the owner on the PR. On the issue, before I opened it, the owner wrote "Feel free to open prs but each fix in a separate pr please", which is why this PR is test-only. On the PR, the CodeRabbit bot left one review comment, labelled "Trivial": assert the preview box's `boxShadow` style after the interactions.
- 2026-11-10: I didn't reply to the bot or change the branch. The preview's inline style is already listed under "Not covered" in my description, and my playbook says bot reviews aren't a round to answer. If the owner asks for it, I'll add the assertion and reply with the commit and the test output.
- 2026-11-11: the owner submitted a "Changes requested" review: "Please apply the code rabbit nit pick comment".
- 2026-11-11: I applied it in a new commit, `5b92a9f` ("test: assert the box shadow preview style after each interaction"). It asserts the preview's inline `boxShadow` on load, after the sliders and color change, and with inset checked and unchecked. A break-it check (dropping `inset` from the preview expression only) failed the inset test, and CI passed prettier and test. I also corrected the PR description, which had wrongly said jsdom couldn't check that style; a probe showed it reports `boxShadow` exactly. I replied on the PR with the commit, the test and Prettier output, and that I'd only run the break-it check for inset: https://github.com/Bashamega/WebDevTools/pull/701#issuecomment-6811000590. The re-request-review API returned 404 (I don't have write access to the repo), so the re-request goes through the Re-request review button on the PR page.

**Status:** Awaiting review (changes applied in `5b92a9f`; waiting for the owner to re-review)

**Toolkit**

- Tool: the ship-gate (`check_gate.py`), run by hand on the branch with `--branch --title … --body-file pr_draft.md`, and then as a PreToolUse hook when I opened the PR with `claude "run this command: gh pr create …"`. The voice guard checked the same body.
- What it produced: three PASS runs, each with all three manifest checks ok (Prettier 3s, Jest about 25-35s, coverage about 26s) and pr-precheck accepting all six checks: diff-matches-plan, description-matches-diff, test-decisive, repo-checks-run, diff-clean and template-and-disclosure. At PR time it reused the 10:48 PASS instead of re-running, and the voice guard logged a pass.
- Difficulties: the first PASS still came with voice notes that mattered. A ticked "no new warnings" box had no evidence behind it, the check commands were abbreviated as `jest -> …`, and the probe was cited without its output. The voice guard then stopped the revised draft under "A cause is a hypothesis until the output shows it". Each revision of `pr_draft.md` invalidated the PASS and cost another run.
- What changed: I put the exact commands and raw output in the description, added the warnings evidence and a "Not covered" line, and quoted `page.jsx` line 62 as the cause. I also rewrote the AI disclosure so it says what Claude Code actually did. I'd now draft the description against my voice rules before the first gate run, not after it.

---

## Learnings and Reflections

**Technical Skills Gained**

- **React Testing Library on a page with no labels.** I selected the sliders with `getAllByRole("slider")` by position, read derived output straight from the rendered text, and asserted that output with a regex (`#00000080\s*;`), so the test holds with or without a pending bug fix.
- **Mocking a side-effecting library and a missing browser API in Jest.** I mocked `sweetalert2` with an `__esModule` factory and stubbed `navigator.clipboard` with a resolving `jest.fn()` (and a rejecting one for the failure path). Restoring spies in `afterEach` keeps a failing test from leaking its `console.error` spy into the next one.
- **A mutation check as the evidence for a test-only change.** Coverage shows the lines ran. Deleting `inset_` from `page.jsx` and watching exactly one test fail shows the tests decide something.
- **Windows-specific tooling failures.** Python's `subprocess` can't find `claude.cmd` by its bare name, `text=True` decodes as cp1252 unless you pass `encoding="utf-8"`, npm runs scripts through cmd.exe (so `NODE_OPTIONS=x jest` fails), `core.autocrlf=true` makes Prettier flag every file, and ripgrep-based Glob doesn't follow symlinks.
- **Reading a repo's real conventions** from `.github/workflows/`, the PR template and contributing.md (for example, `feature/<name>` branches and tests mirroring `src/app`), instead of guessing.

**Challenges Overcome**

- **Finding an issue that wasn't taken.** My scan and two dozen site picks hit open PRs or recent claims (see Why I Chose This Issue). I solved it with a free `gh` pre-check for linked PRs and claim comments before paying to grade. GitHub's `-linked:pr` qualifier would have done most of that filtering in the search itself.
- **The course hooks didn't run on Windows.** The voice guard, the ship-gate and the PR monitor all had the same `claude.cmd` lookup bug, and the hooks matched only the `Bash` tool, not PowerShell. Two of them also crashed on UTF-8 text. Each time I found it by watching a real run fail (a post that skipped the guard, a "claude not on PATH" stop, a cp1252 traceback), patched the smallest line that fixed it, and confirmed the fix with a piped test payload.
- **The repo's own pre-commit hook failed for reasons unrelated to my change** (193 CRLF files; `NODE_OPTIONS` in cmd.exe). I fixed the clone's line endings and pointed npm's script shell at Git Bash rather than skipping the hook.
- **My own words overreaching.** The voice guard stopped me six times: a claim that promised the fix, a report-back missing its output, a PR draft naming a cause without evidence, and three stops on my review reply (no command on the break-it run, no environment, nothing said about what I hadn't covered). My own review also caught an AI disclosure saying I'd run commands Claude Code ran. Each stop pointed at a real problem, so I fixed the text every time instead of the rule. The worst overreach the guard couldn't see was in my PR description: I'd written as fact that jsdom couldn't check the preview style, without ever testing it. Review round 1 proved it wrong.

**What I'd Do Differently Next Time**

- **Check claim signals before anything else.** I'd put `-linked:pr` into my scout's queries on day one, and treat an issue-body offer ("I can open a PR") or a bot "is-working" label as a claim. Most of my unit-5 and unit-6 time went into issues that were already taken.
- **Plan before building.** I wrote the tests in unit 6, before the plan existed, and had to record that as a deviation. On a real bug I'd write `plan.md` and get plan-check's accept first, because the plan is what keeps the PR to one fix.
- **Run my voice rules on the PR draft before the first ship-gate run**, not after. Each revision invalidated the PASS and cost another run.
- **Test a claim before I write it down.** "jsdom isn't a faithful check of it" went into my evidence, my story and my PR as a reason to leave something untested. A five-line probe disproved it, after the owner had already asked for the work.
- **Test the tooling on my platform first.** A two-minute run of each hook with a piped PowerShell payload and a UTF-8 file would have surfaced all the Windows bugs before they blocked real posts.

---

## Resources Used

- WebDevTools `contributing.md`, especially the "Run the Tests" section added in #692. It gave me the test layout (`__tests__/` mirrors `src/app`), the commands, and the PowerShell form: https://github.com/Bashamega/WebDevTools/blob/main/contributing.md
- The merged Lorem Ipsum tests (#697), the model I followed for structure, the clipboard stub and the theme tests: https://github.com/Bashamega/WebDevTools/pull/697
- The repo's CI workflows, which my ship manifest is built from: `.github/workflows/format.yml` and `.github/workflows/jest_tests.yml`
- The owner's answer on #391, which set this PR's scope: https://github.com/Bashamega/WebDevTools/issues/391
- Testing Library's query priority guide, for choosing `getByRole` over test ids, and why unlabeled inputs leave only positional queries: https://testing-library.com/docs/queries/about/#priority
- Jest's mock function and module-mocking docs, for `jest.mock` with an `__esModule` factory and `restoreAllMocks`: https://jestjs.io/docs/mock-functions
