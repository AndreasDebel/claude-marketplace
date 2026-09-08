---
name: barebone-audit
description: Audit an entire learning repository against the barebone principles and propose refactor tickets — finding the abstraction layers, DTO/mapper hops, single-implementation interfaces, defensive branches, and general-purpose handling that make AI-generated study code hard for a student to follow. Fans the reading out across subagents, then writes one ticket per independently-shippable change to docs/tickets/. Use this whenever the user types /barebone-audit, or asks to review, audit, or survey a whole school/course/learning repo for unnecessary complexity, says the existing code in a study project is too complex or too layered to understand and asks where to start simplifying, wants to know what could be stripped out or what the over-engineered parts are, or asks for refactor tickets/plans to make an existing repo simpler and more readable.
user-invocable: true
license: MIT
---

# /barebone-audit — Find the complexity, then propose tickets that remove it

This is the retrospective half of the barebone family: `/barebone-plan` keeps new code
small, `/barebone-claude-md` makes that a standing rule, and this skill deals with the code
that already exists. It reads the whole repository, finds where readability was traded for
robustness or generality, and writes refactor tickets.

**Read `${CLAUDE_PLUGIN_ROOT}/principles/BAREBONE-PRINCIPLES.md` first.** Those six
principles are the audit criteria; this file only describes the procedure.

Two boundaries that define the skill:

- **You propose, you don't refactor.** No source edits. The output is tickets the user
  reads and chooses to run. An audit that also rewrites removes the review step, which is
  the only place a wrong finding gets caught cheaply.
- **"Nothing to do" is a valid result.** Principle 6 rules out change that removes nothing,
  and an audit that always finds work is an audit that manufactures it. A repo that already
  satisfies the principles should come back with a short report and no tickets. Note the
  direction of that principle, though: it licenses *no* finding, not a *weak* one. A file
  that reads tidily but hides a mapper hop or a one-implementation interface still fails
  principles 3 and 4 — being pleasant to look at is not a defence.

## Step 1 — Establish scope, and what the system actually does

Before reading for complexity, get two things:

- **What runs.** Entry points, the projects/modules, how they talk to each other. Build
  files, solution files, `README`, `CLAUDE.md`, launch configs. Principle 1 is about the
  inputs the system *actually sends today*, so you need the real call graph — not the one
  the code is prepared for.
- **Confirm it's a learning repo** — follow
  `${CLAUDE_PLUGIN_ROOT}/principles/LEARNING-REPO-CHECK.md`. This audit proposes deleting
  working code, so it's worth one look before reading further.

Also ask, or infer and state, **what the repo is teaching**. Some complexity is the subject
matter: a proxy has to copy something, a search has to rank something, a scaling exercise
needs its instances. Knowing the lesson is what stops the audit from proposing to delete
the assignment.

## Step 2 — Fan out the reading

Repositories are wide and the six principles need whole-file context, so split by natural
unit — one subagent per project, module, or top-level source directory. Reading a slice in
full is what lets a subagent see that an interface has one implementation, or that a DTO is
mapped in exactly one place; a keyword search across the tree cannot see either.

Give each subagent the principles file path, its slice, the call-graph summary from Step 1,
and the finding shape below. Ask for evidence, not opinions — `path:line` and a count, so
you can rank findings later without re-reading the code.

Two things worth telling every subagent, because they're the common failure modes:

- **Count the callers before calling something unnecessary.** "One implementation" and
  "mapped in one place" are claims about the whole repo, so they need a check outside the
  slice. Flag as uncertain rather than guessing.
- **Report what's already fine.** A slice that comes back empty is real information, and
  it's what keeps Step 4 from padding tickets with marginal work.

Have each subagent report findings in this shape:

```
- principle: <1-6>
  what: <the construct, one line>
  where: <path:line, plus every other site involved>
  size: <lines this touches / lines it would become — may go up, see below>
  reader load: <what the reader stops having to hold in their head: a hop, a branch,
                an indirection, a file they no longer need to open>
  why safe: <the observation that makes removing it safe — a caller count, the single
             input shape, the one implementation>
  removes behaviour: <yes + what observable thing disappears, or no>
  confidence: <high | needs-check: what to check>
```

## Step 3 — Merge and rank

Findings arrive per slice, but the real ones usually cross slices — a DTO layer touches the
API and the client, an interface touches its callers. Merge those into one finding covering
every site, then sort by **how much a reader stops having to hold in their head, against how
much the change disturbs**. A 90-line type chain collapsing into one record beats six
scattered one-line simplifications, even though the count of findings favours the latter.

Rank by reader load, not by line count — they usually agree, and when they don't, line count
is the one that's wrong. Deleting a layer removes lines; expanding a dense one-liner into
steps a student can trace adds them, and is just as much a win. So a finding whose `size`
goes *up* is legitimate: say so plainly in the ticket rather than quietly dropping it
because the number looks like a regression.

Drop anything you can't defend with evidence. Verify every `needs-check` before it reaches
a ticket — a proposal to delete an interface that turns out to have two live callers costs
the user more trust than the finding was worth.

## Step 4 — Write the tickets

**One ticket per independently-shippable change.** The test is whether the repo still
builds and runs with that ticket applied and nothing else. Findings that only make sense
together belong in one ticket; findings that don't need each other should be separate, so
the user can take the cheap ones and leave the rest.

Use the shared shape in `${CLAUDE_PLUGIN_ROOT}/principles/TICKET-TEMPLATE.md`, following its
*(refactor)* branches — the same template `/barebone-plan` writes to, so both kinds of
ticket sit in `docs/tickets/` and read alike. Read it now if you haven't.

Two things the template leaves to you here:

- **Order the steps so the repo builds at the end**, not only after the last one. A
  half-applied refactor the user can't compile is worse than the complexity it removed.
- **Fill in `Deliberately skipped` with the behaviour the change removes**, and be concrete
  about when it would have mattered. On new code an omission is theoretical; here you are
  deleting something that works today.

## Step 5 — Report

Summarise in a handful of lines: what you read, the tickets written with their paths and
rough line savings, and — separately — **what you deliberately left alone and why**. That
last part is the audit's most useful output for a student. "These four files are already as
simple as the problem allows" tells them where to stop looking.

If a finding would delete something the repo demonstrably teaches, don't bury it in a
ticket: raise it here as a question. The user decides whether the lesson or the line count
wins.
