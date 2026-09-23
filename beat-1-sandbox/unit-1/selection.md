# Unit 1 — Issue Selection

Path: `beat-1-sandbox/unit-1/selection.md`

---

## Selected issue

**Issue link**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/61

**Verdict output**

Live-mode run of my installed `issue-select` skill on three candidates (#61, #6,
#59), pasted as returned. The chosen issue, #61, is accepted; I took it over the
top-ranked #59 for the reasons under Selection rationale below.

````
## Grading summary

**Scope check:** All three issues are from `codepath/pathreview-ai301-fa26-s3`, the scoped repo — confirmed as candidates. Repo-level facts (apply to all three): not archived; newest default-branch commit 2026-09-16 (within 90 days); no AI-restriction policy found in `docs/CONTRIBUTING.md`, `.github/PULL_REQUEST_TEMPLATE.md`, or any dedicated AI-policy file (silence passes); all 5 recent commits authored by `Aburke225`, who is a `COLLABORATOR` (confirmed via issue authorship); no releases published (unclear); sampled 10 recent issues for maintainer responses — the only comments found were student claim comments (`authorAssociation: NONE`), no maintainer reply within 30 days (fail, preferred-only).

| Issue | scope-bounded | no-abandoned-attempts | no-open-claim | Verdict |
|---|---|---|---|---|
| #61 — health check raw SQL | pass: single-file SQLAlchemy 2.x `text()` fix | pass: no linked PRs | pass: no linked PRs, no comments | **accept** |
| #59 — faithfulness checker wording bug | pass: single function, existing failing test named | pass: no linked PRs | pass: no linked PRs, no comments | **accept** |
| #6 — hybrid retriever indexing/normalization | pass: single file, bounded (tier-2, 4-6h est.) | pass: no linked PRs | pass: no linked PRs, no comments | **accept** |

**Ranking (fit profile — RAG/eval-harness and FastAPI/SQLAlchemy background, preference for bounded bugs with an existing covering test):**

1. **#59** — hits "eval harnesses" directly in your fit profile, and the issue body names an actual existing failing test (`test_multiple_context_chunks`) — the clearest match to "a covering test already in the repo."
2. **#61** — squarely in your FastAPI/SQLAlchemy wheelhouse, tier-1, and about as bounded as a fix gets (wrap one raw SQL string in `text()`).
3. **#6** — fits your retrieval experience but is tier-2 with a larger estimate (4–6h) and bundles two related sub-fixes (missing index call + per-batch score normalization), giving it more surface than the other two.

```json
[
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s3/issues/59",
    "checks": [
      {"name": "repo-not-archived", "grade": "pass", "evidence": "isArchived: false"},
      {"name": "recent-default-branch-commit", "grade": "pass", "evidence": "newest commit 2026-09-16, within 90 days of 2026-09-23"},
      {"name": "scope-is-bounded", "grade": "pass", "evidence": "single function `_is_supported()` in one file, with a named existing failing test, not an umbrella/tracking issue"},
      {"name": "no-abandoned-attempts", "grade": "pass", "evidence": "zero cross-referenced/linked PRs on the issue"},
      {"name": "no-open-claim", "grade": "pass", "evidence": "no linked PRs and no comments on the issue"},
      {"name": "ai-work-allowed", "grade": "pass", "evidence": "docs/CONTRIBUTING.md and PR template state no AI restriction"},
      {"name": "maintainer-authored-commit", "grade": "pass", "evidence": "all 5 recent commits authored by Aburke225 (authorAssociation: COLLABORATOR)"},
      {"name": "recent-release", "grade": "unclear", "evidence": "GET releases/latest returned 404 Not Found — no releases published"},
      {"name": "maintainer-responds", "grade": "fail", "evidence": "sampled 10 recent issues; only student (NONE-association) claim comments found, no maintainer reply within 30 days"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s3/issues/61",
    "checks": [
      {"name": "repo-not-archived", "grade": "pass", "evidence": "isArchived: false"},
      {"name": "recent-default-branch-commit", "grade": "pass", "evidence": "newest commit 2026-09-16, within 90 days of 2026-09-23"},
      {"name": "scope-is-bounded", "grade": "pass", "evidence": "single fix in api/routes/health.py (wrap raw SQL in sqlalchemy.text()), clear repro steps, not umbrella/tracking"},
      {"name": "no-abandoned-attempts", "grade": "pass", "evidence": "zero cross-referenced/linked PRs on the issue"},
      {"name": "no-open-claim", "grade": "pass", "evidence": "no linked PRs and no comments on the issue"},
      {"name": "ai-work-allowed", "grade": "pass", "evidence": "docs/CONTRIBUTING.md and PR template state no AI restriction"},
      {"name": "maintainer-authored-commit", "grade": "pass", "evidence": "all 5 recent commits authored by Aburke225 (authorAssociation: COLLABORATOR)"},
      {"name": "recent-release", "grade": "unclear", "evidence": "GET releases/latest returned 404 Not Found — no releases published"},
      {"name": "maintainer-responds", "grade": "fail", "evidence": "sampled 10 recent issues; only student (NONE-association) claim comments found, no maintainer reply within 30 days"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s3/issues/6",
    "checks": [
      {"name": "repo-not-archived", "grade": "pass", "evidence": "isArchived: false"},
      {"name": "recent-default-branch-commit", "grade": "pass", "evidence": "newest commit 2026-09-16, within 90 days of 2026-09-23"},
      {"name": "scope-is-bounded", "grade": "pass", "evidence": "confined to rag/retriever/hybrid.py with a stated 4-6h estimate, not an umbrella/tracking issue"},
      {"name": "no-abandoned-attempts", "grade": "pass", "evidence": "zero cross-referenced/linked PRs on the issue"},
      {"name": "no-open-claim", "grade": "pass", "evidence": "no linked PRs and no comments on the issue"},
      {"name": "ai-work-allowed", "grade": "pass", "evidence": "docs/CONTRIBUTING.md and PR template state no AI restriction"},
      {"name": "maintainer-authored-commit", "grade": "pass", "evidence": "all 5 recent commits authored by Aburke225 (authorAssociation: COLLABORATOR)"},
      {"name": "recent-release", "grade": "unclear", "evidence": "GET releases/latest returned 404 Not Found — no releases published"},
      {"name": "maintainer-responds", "grade": "fail", "evidence": "sampled 10 recent issues; only student (NONE-association) claim comments found, no maintainer reply within 30 days"}
    ],
    "verdict": "accept"
  }
]
```
````

---

## Eval iterations

**Run history**

Four runs, in order:

1. `--limit 3` smoke run (issue-01, issue-02, issue-03) — **agreement: 3/3 scored
   items**. This was a pipeline check rather than a rubric check: the first attempt
   had crashed on Windows before grading anything.
2. `--only issue-01,issue-09,issue-12,issue-20` — **agreement: 3/4 scored items**.
   A deliberate stress test of the four items my rubric was most likely to get
   wrong, run for about $0.80 before committing to a $4 full run. Predicted and
   actual outcomes matched on all four, including the single disagreement.
3. Full 20-issue run — **agreement: 19/20 scored items (bar: 18/20: PASS)**,
   categories `claimed 4/4  clear-accept 8/8  dead-repo 3/3  policy 1/1  scope 3/4`.
4. Full 20-issue run with `--save-run eval-run.txt` — **agreement: 19/20 scored
   items (bar: 18/20: PASS)**, same category line. This is the run committed as
   `eval-run.txt` in this directory, and its only disagreement is again issue-20.

**Issue analysis**

`issue-20` (excalidraw/excalidraw#11811, "Add company logo shape to the toolbar").

My rubric graded it **accept**. The gold label is **reject**, noted as "one-line
feature wish with no spec and a product decision hiding inside".

My rubric read it that way because every disqualifier in my `scope-is-bounded`
check is something a reader can point at in the text, and issue-20 contains none of
them. It does not call itself an umbrella or tracking issue; its body is not a list
of other issue numbers; it does not sweep the codebase — it names
`packages/excalidraw` as the likely surface and even marks custom logo upload as
out of scope for v1; no maintainer says the fix reaches core internals; and it is a
change request, not a support question. It also states success criteria outright
("logo tool in the shapes toolbar → place/resize/move like other elements → correct
export"). On paper it reads better specified than several issues the gold labels
accept. My `no-abandoned-attempts` and `no-open-claim` checks pass it too, because
it carries `linked PRs: none`.

What my rubric cannot see is the phrase `Logo asset TBD` in the Additional context,
together with "our company logo" on an issue opened by `cursor[bot]` carrying no
labels at all. Whose logo Excalidraw should ship is a product decision nobody has
made, so the work cannot actually start however tidy the write-up looks. That is a
judgment about an undecided decision, not about the size of the change, and none of
my five scope disqualifiers points at it.

**Check rationale**

From `tools/issue-select/rubric.md`, the `no-abandoned-attempts` row, quoted as it
is currently written:

> | no-abandoned-attempts | The `linked PRs:` field in repo-facts with the state of each; live: the Development box in the issue sidebar, plus any PRs mentioned in the thread. | Fewer than 2 linked PRs in `closed` state, meaning closed without being merged. `merged` PRs are not counted: they show the issue being carried forward, not abandoned. One dead attempt is ordinary attrition; two is a pattern, and a newcomer is not the person to break it. | required |

The threshold of 2 is not a preference; the eval set forces it. I surveyed the
`linked PRs:` field across all twenty bundles before choosing. issue-09 is a gold
**accept** carrying exactly one closed PR (`conda/conda#11627`), so a threshold of 1
would have rejected a good issue over a single stale attempt from years earlier.
issue-15 is a gold **reject** carrying exactly two closed PRs (`zulip/zulip#20840`,
`zulip/zulip#23123`) behind a friendly `good first issue` label, so a threshold of 3
would have let it through. Only 2 satisfies both, and the reasoning behind the
number is that one abandoned attempt is ordinary — people start things and stop —
while two says the issue has already defeated more than one person.

Excluding `merged` PRs from the count is the other deliberate part. issue-05 has six
merged PRs linked to it; counting those would have read an issue being actively and
successfully worked on as an abandoned one. The state word in the field is what
separates the two, so the check reads the state rather than the number of links.

**Trade-offs**

The quoted check gives up the case where nobody has formally linked a PR at all. It
reads one field, so an issue that several people quietly gave up on without ever
opening a linked PR passes it untouched. An earlier live run on Path Review showed
the same weakness from the other side: on issue #72 the timeline carried two
"referenced" events that turned out to be commits in unrelated personal fork
repositories rather than PRs against the repo, and only opening them told me which
they were. The field is cheap and unambiguous, which is why I kept it, but it sees
attempts only once someone has formalised them.

Nothing changed elsewhere when I settled on 2, and here is how I know: my
`--only issue-01,issue-09,issue-12,issue-20` re-run graded issue-09 `accept`, and
issue-09 is the only gold accept in the set carrying a closed linked PR, so it is
the only item this threshold could have flipped. The two full runs afterwards then
agreed on every item in both the `claimed` and `scope` categories, so no other
verdict turned on this check.

---

## Selection rationale

**Selection rationale**

**Fit to my interests and to the time available.** I have about 2-4 hours for this
one. FastAPI and SQLAlchemy are what I work in already, so the fix itself holds no
surprises for me — and that is the point. For a first contribution I would rather
spend the time learning how contributing to someone else's repo actually works
(claiming, branching, matching their conventions, opening the PR) than spend it
fighting unfamiliar code.

**What the verdict identified correctly, and what I weighed that the rubric could
not.** The verdict got the repo-level picture right on all three candidates: the
repo is not archived, it has recent commits, none of the three is assigned or has an
open linked PR, and the contributing docs place no restriction on AI-assisted work.
It also read the scope of each issue correctly. What it could not weigh is how much
time I actually have this week. The skill ranked #59 first, because my fit profile
names eval harnesses and prefers bugs with a covering test already in the repo, and
on those terms #59 is the better match. I took #61 instead purely on time: it is the
smallest of the three, and finishing something end to end matters more to me right
now than picking the most interesting bug.

**Anticipated difficulty in claiming it.** I expect the claim comment may simply go
unanswered. My own run flagged this: `maintainer-responds` graded `fail` on this
repo, with no maintainer reply inside 30 days across ten sampled issues. So I am not
counting on being told to go ahead. My plan is to reproduce the bug first and
confirm it is real and has not already been fixed on the default branch; if it is
still broken, I will take it.

---

Related paths: `eval-run.txt` in this directory; my skill's files in
`tools/issue-select/`.
