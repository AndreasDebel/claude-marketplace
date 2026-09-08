# Is this a learning repository?

CANONICAL SOURCE. `/barebone-claude-md` and `/barebone-audit` both run this check — one
before installing the principles permanently, one before proposing to delete working code.

The barebone principles tell an agent to skip validation, error handling, and generality.
That is correct for a repository whose only job is that a student can read it, and
damaging for software anyone depends on. The two skills that act on an existing repo are
the ones that can do lasting harm with it, so both stop here first.

## What to look at

Read what's already around you rather than asking cold — a course or module name, an
assignment or exercise structure, `docs/tickets/`, a `README` or `CLAUDE.md` that describes
the repo as school/course/practice/study work (in any language), a project that only ever
runs locally, a git remote that's a personal or class account.

Against that, the signals that it *isn't*: deployment configuration, CI pipelines, a test
suite that gates merges, real users or customers named anywhere, secrets management,
dependencies on other teams' systems.

## What to do about it

- **Clearly a learning repo** — carry on without asking. The check shouldn't become a
  speed bump on the repos the plugin exists for.
- **Clearly not, or genuinely ambiguous** — ask once, plainly, and say what the principles
  would do to this repo if applied. Don't guess: the cost of asking is one question, and
  the cost of guessing wrong is either a memory file that tells every future session to
  drop error handling, or a ticket proposing to delete code that something depends on.

If the user confirms, that settles it — proceed with the full task and don't raise it again.
