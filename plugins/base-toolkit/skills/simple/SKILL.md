---
name: simple
description: Answer one question as simply and concisely as humanly possible — plain language, no preamble, no caveats, no follow-up. Use when the user types /simple or /s, or asks you to "just answer", "keep it short", "in one line", "ELI5", or signals they want a single bare answer to a single question rather than an explanation or a conversation.
user-invocable: true
license: MIT
---

# /simple — one question, the shortest true answer

The user wants the answer and nothing else. They already know you *could* elaborate — that's exactly what they're opting out of. Treat extra words as a cost they asked you not to pay.

## How to answer

Give the shortest response that is actually correct and actually answers what was asked. Often that's a single sentence; sometimes a single word, number, or line of code. Use plain language a non-expert would follow — no jargon unless the question is itself technical, and then only the necessary term.

Cut everything that isn't the answer:

- No preamble ("Great question", "Sure", "Well,"), no restating the question back.
- No "it depends" throat-clearing. If it genuinely depends, pick the most likely case, answer it, and say the condition in a half-sentence.
- No caveats, disclaimers, or "but note that…" unless leaving it out would make the answer wrong or harmful.
- No follow-up offers ("Want me to…?"), no summary, no closing line.

## Scope: one question

Answer the single question in front of you. If the user actually asked several things, answer the main one in one breath rather than turning it into a list — concision is the whole point. The exception is a genuinely binary ask ("X or Y?") where the honest answer is short on both sides.

## When short would be wrong

If a one-liner would be misleading or unsafe, give the *shortest honest* answer instead of a wrong short one — but still strip the filler. Brevity is the goal; accuracy is the limit. Never shorten by guessing at facts you don't have: if you don't know, say so in a few words.

## Examples

Q: What's the capital of Australia?
A: Canberra.

Q: Should I use `let` or `const` by default in JS?
A: `const` — switch to `let` only when you need to reassign.

Q: Why is the sky blue?
A: Air scatters short blue wavelengths of sunlight more than the rest, so the sky looks blue.

Q: Is it faster to use a set or a list to check membership in Python?
A: A set — O(1) lookups vs. O(n) for a list.
