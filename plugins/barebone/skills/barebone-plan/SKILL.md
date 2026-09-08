---
name: barebone-plan
description: Author an implementation plan under the barebone principles — the smallest, most readable version of a feature that actually runs, with error handling, abstraction layers, and generality deliberately left out and listed as skipped. Writes the plan to docs/tickets/<name>-plan.md. Use this whenever the user types /barebone-plan, or asks to plan a feature, project, or exercise in a learning/school/course repo and wants the result simple enough to read and understand rather than production-ready — including phrases like "plan this but keep it minimal", "I need to be able to follow this code", "don't over-engineer it", "student-level version", or when they're about to have you build something in a study repo and complexity is the thing they're worried about.
user-invocable: true
license: MIT
---

# /barebone-plan — Plan the smallest version that actually runs

Write an implementation plan for a learning repository: the version a student can read in
one pass, not the version that survives production. This is the *per-task* half of the
barebone pair; `/barebone-claude-md` is the standing-rule half. Both carry the same rules,
so start by reading them.

**Read `${CLAUDE_PLUGIN_ROOT}/principles/BAREBONE-PRINCIPLES.md` before planning
anything.** The six principles there are the whole ruleset — this file only says how to
turn them into a plan document.

You are writing a plan, not code. Don't edit source files.

## Step 1 — Pin the one scenario

Principle 1 needs an input, and when the code doesn't exist yet there is no "what it
actually handles today" to read off the repo. So establish it first, in one exchange:

> *What is the single concrete case this has to work for?*

Push for something specific enough to design against — "one browser sends
`GET /api/search?query=…` and gets JSON back", not "handles search requests". If the user
answers vaguely, offer the narrowest reading you can defend and let them widen it. A plan
built on a vague scenario silently re-expands into the general-purpose version, because
generality is the default every agent falls back to when the boundary is unstated.

Then, if the plan touches an existing codebase, read the files it will change. Principle 6
means untouched-and-readable beats rewritten-and-tidier, and you can't apply it blind.

## Step 2 — Name what you're leaving out

Before writing steps, list — for yourself — what a normal, competent plan would include
here: the validation, the interface, the DTO layer, the retry, the config abstraction, the
second implementation. Then cut each one and note *why it's safe under the named scenario*.

This inversion matters. If you plan forward from "what does this feature need", you
rebuild the production version by habit and the principles never bite. Planning what to
*delete* from the obvious design is what actually produces the small version — and it also
hands you the "Deliberately skipped" section for free, which is what makes the omissions
recoverable later.

## Step 3 — Write the plan

Save to `docs/tickets/<short-name>-plan.md` (create the directory if needed). Use this
shape — it matches the convention these repos already use, and each section earns its
place:

```markdown
# <One-line title: what gets built>

## Context

Why this is being built and what already exists — the current state in two or three
sentences, with concrete file references. Then:

**The one scenario:** <the single concrete case, stated plainly>

**Decisions already made with the user:**
- <each settled choice, one line, with the alternative it beat>

## Step 1 — `path/to/first/file.ext`

What goes in it, precisely enough to implement without further design decisions, but as
prose and signatures — not as finished code. One step per file. State the size you expect
it to be when it's obviously small ("~10 lines"), because that number is the thing a
reader can check the result against.

## Step 2 — `path/to/next/file.ext`

...

## Deliberately skipped

- **<what>** — safe here because <why, referencing the one scenario>. Add it back by
  <the one-line change that would restore it>.

## Verification

Numbered, runnable commands with the expected output stated. The last one should be the
observation the exercise is actually about — the thing the student is meant to see happen.
```

## Rules for the plan itself

- **Every file gets a path and a step.** A plan that says "add a service layer" without
  naming files is where invisible complexity enters.
- **Fewest files that still separate the idea being taught.** One extra class is fine when
  it isolates the mechanism a student should open first; three are not.
- **Prose and signatures, not implementations.** If a step is turning into finished code,
  the design decision is already made — say it in a sentence and move on.
- **Flag anything you can't shrink.** Some complexity is the subject matter, not clutter —
  a proxy has to copy something, a search has to rank something. When a step stays big
  because the domain is big, say so in the step, so the reader doesn't hunt for the
  simpler version that doesn't exist.
- **Explain the surprising choices in the plan.** A student reading it later needs to know
  why the interface isn't there, not just that it isn't.

## Step 4 — Hand it over

Report the path and summarise the plan in a handful of lines: files, rough total size, and
the one scenario it's built for. Then stop. Ask before implementing — reviewing the plan
while it's still cheap to change is the point of writing one.
