# Rubric: is this a good first issue?

Recency thresholds are measured against the bundle's stated capture date in
eval mode, and against today in live mode.

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| repo-not-archived | The `archived:` field on the repo line of the repo-facts block; live: the read-only banner across the top of the repo front page. | `archived: no`. An archived repo is read-only and cannot take a pull request at all. | required |
| recent-default-branch-commit | The "last 5 default-branch commits" list in repo-facts: the newest date among the five, which is not always the first line. Live: the commit list on the repo front page. | That newest date falls within 90 days of the capture date. Who authored it is not part of this check, because the bundle's commit list carries names without Owner/Member/Collaborator badges, and a condition the evidence cannot answer would grade `unclear` on every healthy repo. | required |
| scope-is-bounded | The issue title, the issue body, and the comment thread. | None of these holds: (a) the issue calls itself an umbrella, tracking, or mega issue in its title or body; (b) its body is mainly a list of other issue numbers rather than a description of one change; (c) the work is described as sweeping the codebase with no stated endpoint, e.g. "incrementally adding more" with PRs welcome "both big and small"; (d) a maintainer says in the thread that the fix reaches core internals; (e) the issue is a usage or support question rather than a request to change the code. Written as disqualifiers because each one is something a reader can point at in the text, where "small enough for a newcomer" is an adjective no two graders would apply the same way. A body that names several files inside one area of the project is not a disqualifier. | required |
| no-abandoned-attempts | The `linked PRs:` field in repo-facts with the state of each; live: the Development box in the issue sidebar, plus any PRs mentioned in the thread. | Fewer than 2 linked PRs in `closed` state, meaning closed without being merged. `merged` PRs are not counted: they show the issue being carried forward, not abandoned. One dead attempt is ordinary attrition; two is a pattern, and a newcomer is not the person to break it. | required |
| no-open-claim | The `linked PRs:` field in repo-facts with the state of each; live: the Development box in the issue sidebar plus any PRs mentioned in the thread, believing the thread when the two disagree. | No linked PR is in `open` state. An open PR is somebody's live attempt at this issue; a `closed` or `merged` one is not a claim on the work now. Assignees and claim comments are deliberately not part of this check: an assignee is an unreliable signal in many repos, and under the Path Review house rule in `scope.md` classmates' claim comments do not block an issue at all. | required |
| ai-work-allowed | The `contribution policy` line in repo-facts; live: `CONTRIBUTING.md` in the repo root or `.github/`, the contributor docs it links out to, any `AI_POLICY.md` or `AI_USAGE_POLICY.md`, and the pull-request template. | The policy leaves an action that makes an AI-assisted contribution acceptable: disclosure, personal understanding, testing and human review all count as such actions, and a repo that states nothing has stated no restriction, so silence passes. Fail when the policy refuses AI-generated work outright, leaving nothing a contributor could do to make the work acceptable, and fail too when it states that it discourages generative AI for the kind of work this issue asks for, even short of a ban. The second half is deliberately stricter than reading discouragement as a term to follow: a project that says it does not want this way of working is not where a first contribution belongs. | required |
| maintainer-authored-commit | The author names in the same "last 5 default-branch commits" list, matched against maintainer identity wherever the bundle reveals it (a commenter's `author_association` in the thread); live: the badge on the commit, or whose pull request a bot merged. | At least one of the five commits is authored or merged by a maintainer. Eval bundles almost never carry this, so the check usually grades `unclear`; as a preferred check that costs the issue nothing, and it does its real work in live mode, ranking accepted candidates. | preferred |
| recent-release | The `latest release` field in repo-facts; live: the Releases box in the right sidebar of the repo front page. | A release published within 180 days of the capture date. `latest release: none published` grades `unclear`, not fail: a repo that does not ship releases is unmeasurable on this signal, not unhealthy. | preferred |
| maintainer-responds | The "maintainer first-response sample" in repo-facts: days to the first owner/member/collaborator comment on each sampled issue. Live: the first badged reply on a few recently updated issues. | At least 1 sampled issue received a maintainer reply within 30 days. A sample of fewer than 3 issues grades `unclear` (too small to read). A full sample with no reply inside 30 days is a fail. | preferred |

## Verdict rule

`accept` if and only if every `required` check grades `pass`. A single required
fail produces `reject`. The verdict space is binary; there is no third outcome.

An `unclear` on a required check counts as `fail`: an issue whose liveness,
scope, claim state or contribution policy cannot be verified is not one to take
as a first contribution. Every required check above is written against a field
the evidence always carries, so this clause is a fallback for live mode, where a
linked policy page can be missing or a repo page unreachable, rather than
something the eval bundles should ever trigger.

`preferred` checks never change a verdict. They rank the issues that were
accepted: the candidate with more passing preferred checks ranks higher, and
where two accepted candidates tie on that count, the fit profile in `scope.md`
breaks the tie. An `unclear` on a preferred check counts as neither pass nor
fail for ranking; it simply does not count.
