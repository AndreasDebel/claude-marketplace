---
name: barebone-claude-md
description: Install the barebone principles as a standing rule in this repository's CLAUDE.md, so every future response writes student-readable code by default instead of production-grade code. Idempotently replaces (or appends) a "## Barebone principles" section. Use this whenever the user types /barebone-claude-md, or asks to make a learning/school/course/practice repo produce simpler code from now on, to stop Claude over-engineering in this project, to enforce or install simplicity rules, to add barebone rules to CLAUDE.md, or says the AI-generated code in a study repo is too complex to follow and they want that fixed permanently rather than file by file.
user-invocable: true
license: MIT
---

# /barebone-claude-md — Make simplicity a standing rule in this repo

The problem this solves: AI-generated code isn't verbose, it's *correctness-dense*. It
handles inputs nothing sends, layers abstractions nobody needs yet, and defends against
failures that never happen. All of that is right in production and fatal in a repo whose
only purpose is that a student can read it. Fixing it file by file doesn't stick, because
the next response reverts to default habits. Writing it into `CLAUDE.md` does stick.

This skill is the *standing rule* half of the barebone pair. `/barebone-plan` is the
per-task half; they carry the same six principles and are meant to be tried
independently, so you can see which enforcement actually changes the output.

## Before you write

**Check that this is a learning repository, and stop if it isn't.** These rules tell an
agent to skip validation, error handling, and generality. In a real project that's
damaging advice living permanently in the repo's memory file. Look at what's around you —
a course name, `docs/tickets/`, exercise or assignment structure, a README that says
"school"/"course"/"øvelse", a repo used only locally. If it reads like production
software, or you genuinely can't tell, ask once before writing rather than guessing.

## Procedure

1. **Read the canonical block.** Open
   `${CLAUDE_PLUGIN_ROOT}/principles/BAREBONE-PRINCIPLES.md` and take everything between
   the `BEGIN BAREBONE BLOCK` and `END BAREBONE BLOCK` markers, exclusive of the markers
   themselves. Copy it **verbatim** — don't paraphrase, trim, or "adapt it to this repo".
   The whole point of a single source file is that both skills and every repo you install
   into stay in sync; a local reword silently forks the ruleset you're trying to A/B.

2. **Find the target.** The `CLAUDE.md` at the repository root (the directory containing
   `.git`), not a nested one. If several exist, the root one is the target — say which
   nested ones you're leaving alone.

3. **Write it, idempotently.**
   - If a `## Barebone principles` heading is already present: replace that section —
     from the heading through to the next line beginning `## ` at the same level, or end
     of file — with the fresh block. Re-running the skill after the canonical file changes
     is the normal way to update a repo, so this has to be safe to run any number of
     times.
   - If it's absent: append the block at the end of the file, separated by a blank line.
   - If `CLAUDE.md` doesn't exist: create it with a one-line `# CLAUDE.md` heading
     followed by the block.
   - Preserve everything else in the file byte for byte. Build commands, architecture
     notes, and the user's own conventions are not yours to tidy while you're in there.

4. **Report in two or three lines**: the path written, whether the section was replaced or
   appended, and — if you replaced one — what changed relative to what was there. If the
   old and new blocks are identical, say so; a no-op is a useful answer.

## What this skill does not do

Don't touch source code. Installing the rule and acting on it are separate steps, and
mixing them makes it impossible to tell whether the rule is what changed the next
response — which is the experiment the user is running.
