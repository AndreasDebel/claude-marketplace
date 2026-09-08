---
name: e
description: Re-explain the last answer so a smart non-expert actually gets it — a short plain-language version, a longer elaboration on the same theme, and a list of up to five technical terms worth keeping (starred where they're used). Use when the user types /e or /easy, or asks you to "explain that in plain English", "I didn't understand that", "what does <term> mean", "explain it like I'm not a developer", "break that down", "what's actually going on here", or otherwise signals the last answer went over their head. Unlike /simple (which cuts to one short line), /easy is allowed and encouraged to be longer — clarity is the goal, not brevity. Short alias of /easy.
user-invocable: true
license: MIT
---

# /e — make the last answer land

Short alias of `/easy`. Re-explain the same true thing in words that reach a smart non-specialist. Opposite trade-off from `/simple`: extra words are fine here as long as each one earns its place. Length isn't the goal — landing is.

## Target

Default: your own last substantive response. If the user names a part ("/e the AGP bit"), zoom into just that. If there's nothing to re-explain — a fresh question, or a fresh conversation — answer directly, written in this style from the start.

## Format — always these three headings, verbatim (`##`, not bold)

```markdown
## Short version
One or two sentences. The whole answer, stripped to its point — correct on its own, just not deep.

## Long version
Same idea, more room to breathe. Pick whatever form carries it best — prose for
an argument, a table for a comparison, a diagram for structure/flow, numbered
steps for a sequence, bullets for a flat set of facts. Mixing is fine. Length
is set by the idea: two paragraphs is common, but three honest sentences beat
padding.

## Technical terms
- term\* — what it actually is, in a clause a stranger would follow.
- term\* — same. Five max, usually fewer; drop the section if nothing qualifies.
```

Whatever shape the long version takes, the language rules below still apply inside it — a table cell or diagram box is not a licence for a bare acronym.

## Asterisk contract

Star a term where it's first used in the short or long version (`AGP\*` — escape the star, a bare `*` opens markdown emphasis). Every starred term gets a list entry; every list entry must appear starred in the text. No orphans either direction.

## Who you're writing for

A sharp adult who knows nothing about this field — not slow, just not a specialist.

- No unexplained jargon: paraphrase it away, or star + define it. No third option.
- No baby talk — short words, not small ideas.
- Concrete over abstract: "the assembly line that turns code into an app" beats "a build automation tool."
- One honest analogy beats a paragraph of definition; a misleading one costs more than it gives.
- Skip numbers/flags/paths unless the number is the point.

## Say the same thing, not a new thing

This is a re-explanation, not a second attempt — same facts, same conclusion, only the words change. Don't re-research, rebuild, or open new files to answer it. If the honest truth is you never knew something, say that plainly too.
