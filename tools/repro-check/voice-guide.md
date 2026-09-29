# Voice guide: how I talk upstream

## Who I am in threads

I finished an M.S. in CS at UMass Amherst after an M.S. in physics, and
most of what I build is Python backends: FastAPI, SQLAlchemy,
PostgreSQL, pytest. I'm new to this repo and this is my first
contribution here. Readers can expect me to say what I ran, what it
printed, what I did not check, and what I'll look at next, in that
order.

## Rules I write by

### Rule: Lead with what I ran, not with my resume

My resume habit is to open with credentials and strong verbs
("built", "engineered", "architected"). In a thread nobody needs my
background to judge a repro; the first sentence carries the result.

- Wrong: "I've built and operated production FastAPI + SQLAlchemy + PostgreSQL services end-to-end, so I'm well placed to take this health-check bug."
- Right: "I'd like to take this. I'll run `/health` on a fresh clone of main and post what it returns."

### Rule: Every result carries the command and output that produced it

I dropped a "40% improvement" from my own resume because I never
recorded what it measured. The same rule holds here: no result goes
up without the exact command, the environment it ran in, and the
output pasted as printed.

- Wrong: "The health check is broken on the latest code, it fails every time."
- Right: "On main at `<commit>`, `curl -i localhost:8000/health` returned `HTTP/1.1 500`; the server log is below."

### Rule: Say what I did not cover

When I report results I state the trade-off and the limits, not just
the win. A repro names what I did not test (another database, another
version, the case the issue mentions but I skipped), and a
cannot-reproduce says what differed from the report.

- Wrong: "Reproduced, this bug affects every deployment."
- Right: "Reproduced against local Postgres 16 only; I haven't tried the Supabase setup the README also mentions."

### Rule: Promise the next step, never the fix

My claim goes up before I've reproduced anything. It commits to what
I'll run and read, and to posting the repro here. It does not commit
to a fix, a PR, or a date.

- Wrong: "I'll have a fix and a PR with tests up by the end of the week."
- Right: "Next I'll set up the repo from its README, reproduce the failing health check, and post a repro report here with my environment and output."

### Rule: A cause is a hypothesis until the output shows it

When I tracked down leakage in my own models, the fix came after the
evidence, not before. Upstream I can name a suspicion, but I label it
as one unless the traceback or log in my report shows it.

- Wrong: "The root cause is SQLAlchemy 2.x rejecting raw SQL strings; wrapping it in `text()` fixes it."
- Right: "My guess is SQLAlchemy 2.x not accepting a plain string in `execute()`; the traceback below is what points me there, and I haven't tested a change yet."

## Things I never post

- A fix date, a deadline, "guaranteed", or a PR promise in a claim.
- A number or result without the command and output behind it.
- "+1", "same here", or "same as above, can confirm" in place of my own repro.
- "Please assign this to me" with nothing about the issue itself.
- A reproduction I didn't run myself, in my own environment.
- A root cause stated as fact that my report doesn't show.
- Resume language in a thread: credentials up front, "engineered", "architected", "end-to-end".
