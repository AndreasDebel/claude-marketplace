# claude-marketplace

Personal Claude Code plugin marketplace.

| Plugin         | Skills                                          |
|----------------|-------------------------------------------------|
| `base-toolkit` | `/easy` (`/e`), `/simple` (`/s`), `/teacher`, `/socrates` |
| `barebone`     | `/barebone-plan`, `/barebone-audit`, `/barebone-claude-md` |

## barebone

For **learning repositories only.** AI-generated code isn't verbose so much as
correctness-dense — it handles inputs nothing sends, layers abstractions nobody needs yet,
and defends against failures that never happen. Correct in production, unreadable in a
repo whose only job is that a student can follow it.

Everything the three skills share lives in `plugins/barebone/principles/` and is referenced,
never restated — `BAREBONE-PRINCIPLES.md` (the six rules, and the block installed into a
repo's `CLAUDE.md`), `TICKET-TEMPLATE.md` (the shape both ticket-writing skills emit), and
`LEARNING-REPO-CHECK.md` (the guard on the two skills that act on an existing repo).

They enforce the same rules at three different points, so the three can be compared:

- **`/barebone-plan`** — before the code exists. Authors an implementation plan for the
  smallest version that actually runs, with a "Deliberately skipped" section, to
  `docs/tickets/<name>-plan.md`.
- **`/barebone-audit`** — after it exists. Fans the reading out across subagents, then
  writes one refactor ticket per independently-shippable change to
  `docs/tickets/<name>-refactor.md`. Returning no tickets is a valid result.
- **`/barebone-claude-md`** — always on. Idempotently installs the principles as a
  `## Barebone principles` section in the repo's `CLAUDE.md`.
