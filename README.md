# claude-marketplace

Personal Claude Code plugin marketplace.

| Plugin         | Skills                                          |
|----------------|-------------------------------------------------|
| `base-toolkit` | `/easy` (`/e`), `/simple` (`/s`), `/teacher`, `/socrates` |
| `barebone`     | `/barebone-plan`, `/barebone-claude-md`         |

## barebone

For **learning repositories only.** AI-generated code isn't verbose so much as
correctness-dense — it handles inputs nothing sends, layers abstractions nobody needs yet,
and defends against failures that never happen. Correct in production, unreadable in a
repo whose only job is that a student can follow it.

Both skills carry the same six principles, kept in
`plugins/barebone/principles/BAREBONE-PRINCIPLES.md`, and enforce them two different ways
so the two can be compared:

- **`/barebone-plan`** — per task. Authors an implementation plan for the smallest version
  that actually runs, with a "Deliberately skipped" section, to `docs/tickets/<name>-plan.md`.
- **`/barebone-claude-md`** — standing rule. Idempotently installs the principles as a
  `## Barebone principles` section in the repo's `CLAUDE.md`.
