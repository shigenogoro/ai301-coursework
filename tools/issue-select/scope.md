# Scope: where to look, and who is looking

<!--
This file is the skill's field of view. The rubric (rubric.md) decides
whether an issue is GOOD; the scope decides which issues are candidates
at all, and whose hands the issue would land in. It applies in live mode
only: in eval mode the bundle is the whole world and this file is
ignored.

Two parts. Staff wrote the first; you write the second.
-->

## Where candidates come from

Only issues in the course's Path Review repository are candidates:

- Repo: `codepath/pathreview-ai301-fa26-s3` <!-- paste your section's repo from the Unit 1 Check-In page -->

Do not search, fetch, or grade issues from any other repository, however
promising. The wider GitHub comes later in the course; for now the field
is Path Review.

**Path Review house rule.** Path Review is a classroom, and your
classmates are not strangers. Ignore the usual claim signals here: other
students' claim comments (and there may be several on one issue) do not
block an issue, and finding some on the issue you want is normal. Claim
anyway: course credit attaches to the pull request you open, not to
whether it merges, so a shared issue costs nobody anything. Everything
else in the rubric applies as written.

## Your fit profile

<!-- YOU write this part: a few sentences about you. What languages and
tools you have actually used, what you want to get better at, anything
you want to avoid. The skill uses this only to RANK the issues your
rubric accepts, never to change a verdict: fit cannot rescue an issue
your rubric rejects, and cannot sink one it accepts. -->

I am a CS master's student who works in Python day to day: FastAPI and Pydantic
backends, SQLAlchemy and PostgreSQL, pytest, and a lot of RAG and LLM-integration
work (retrieval, output parsing, eval harnesses, provider routing). I am also
comfortable in TypeScript/React and SQL, and have written Java and C/C++ for
coursework.

What I want to get better at is working inside someone else's codebase rather than
my own: reading unfamiliar code, following the conventions already there, and
writing the test and the pull request the way the project does it. Bounded bugs
with a covering test already in the repo, and docs or configuration fixes where the
correct behaviour is stated somewhere already, suit that best.

For a first contribution I want to avoid anything whose design is still being
argued out, and anything that needs a heavy local environment (compiled toolchains,
emulators, large datasets) before I can even reproduce it.
