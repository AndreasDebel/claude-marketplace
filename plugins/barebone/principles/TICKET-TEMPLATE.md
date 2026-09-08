# Barebone ticket template

CANONICAL SOURCE. `/barebone-plan` and `/barebone-audit` both write tickets in this shape —
one for code that doesn't exist yet, one for code that does. Keeping the shape in a single
file is what lets the two kinds sit in the same `docs/tickets/` folder and read alike.

Save to `docs/tickets/<short-name>-plan.md` for new work, or
`docs/tickets/<short-name>-refactor.md` for simplifying what exists. Create the directory
if it isn't there.

Sections marked *(new work)* or *(refactor)* apply to one kind only; the rest apply to both.

---

```markdown
# <One-line title: what gets built, or what gets simplified>

## Context

Two or three sentences on what already exists and why this ticket exists, with concrete
file references.

*(new work)* **The one scenario:** <the single concrete case this must work for — one
request shape, one file format, one caller>

*(new work)* **Decisions already made with the user:**
- <each settled choice, one line, with the alternative it beat>

*(refactor)* Name the principle(s) at stake and the evidence that makes the change safe —
the caller count, the single input shape, the one live implementation.

*(refactor)* **Size:** ~<N> lines across <M> files → ~<N'> lines across <M'> files, and
**what the reader stops having to follow** — the hop, branch, indirection, or file that
goes away. State both, because they can move in opposite directions: expanding a dense
one-liner into traceable steps grows the line count and still lowers the load. When that
happens, say so here rather than leaving the number looking like a regression.

## Step 1 — `path/to/file.ext`

What goes in it, precisely enough to implement without further design decisions, but as
prose and signatures — not finished code. If a step is turning into finished code, the
design decision is already made; say it in a sentence and move on.

One step per file. For a refactor, order the steps so the repo builds at the end. State the
size you expect when it's obviously small ("~10 lines") — that number is what a reader
checks the result against.

## Step 2 — `path/to/next/file.ext`

...

## Deliberately skipped

What a production version would have that this doesn't — for new work, what you chose not
to build; for a refactor, the behaviour the change removes. One line each:

- **<what>** — safe here because <why, referencing the one scenario or the evidence>.
  Add it back by <the one-line change that would restore it>.

This section is what makes the omissions recoverable later, so it earns its place even
when it's short. Omit it only for a refactor that is genuinely behaviour-preserving.

## Verification

Numbered, runnable commands with the expected output stated: the build, then the actual
scenario the code serves, then anything the change was supposed to leave untouched. For new
work, the last one should be the observation the exercise is actually about — the thing the
student is meant to see happen.
```
