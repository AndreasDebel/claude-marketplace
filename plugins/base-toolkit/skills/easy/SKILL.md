---
name: easy
description: Re-explain the last answer so a smart non-expert actually gets it — a short plain-language version, a longer elaboration on the same theme, and a list of up to five technical terms worth keeping (starred where they're used). Use when the user types /easy or /e, or asks you to "explain that in plain English", "I didn't understand that", "what does <term> mean", "explain it like I'm not a developer", "break that down", "what's actually going on here", or otherwise signals the last answer went over their head. Unlike /simple (which cuts to one short line), /easy is allowed and encouraged to be longer — clarity is the goal, not brevity.
user-invocable: true
license: MIT
---

# /easy — make the last answer land

The user just read something they didn't fully follow, and they'd rather ask than nod along. That's a good instinct and you should reward it: your job is to say the same true thing again, in words that reach them.

This is the opposite trade-off from `/simple`. There, extra words were a cost. Here, extra words are the point — as long as every one of them is doing work. Length isn't the goal either; *landing* is. A great `/easy` answer is as long as the idea needs and not a line longer.

## What "the last answer" means

Default target: your own most recent substantive response — the thing sitting right above their `/easy`. Re-explain that.

Two variations, both common:

- **They named a target** ("/easy the AGP part", "/e what's a wrapper"). Zoom in on exactly that; ignore the rest.
- **There's nothing to re-explain** — they invoked `/easy` with a fresh question, or the conversation just started. Then answer the question directly, but write it in this style from the start.

## The shape of the answer

Use these three beats, in this order. The user picked this structure because it's predictable — they want to know where to look for the glossary without hunting.

```markdown
## Short version
One or two sentences. The whole answer, stripped to its point.

## Long version
The same idea again with room to breathe — in whatever form carries it best:
prose, a table, a diagram, numbered steps, bullets.

## Technical terms
- term\* — what it actually is, in a clause a stranger would follow.
- term\* — same. Five entries maximum; usually fewer.
```

Keep all three headings verbatim. They are `##` headings, not bold lines — the user reads these in a terminal and wants the visual break.

### Short version

Everything you'd say if you got one breath. It's the answer, not a preview of the answer — someone who stops reading here should still be correctly informed, just not deeply.

### Long version

Not a longer restatement of the short version — an elaboration on the same theme. Same claim, more of the machinery behind it: how the pieces fit, why it works this way rather than some other way, what happens next time. The short version says *what*; this says *why* and *so what*.

**The heading is fixed; everything under it is yours.** Prose is the common default, not the rule. Pick the shape that carries this particular idea, and let it be different every time:

- a small **table** when the point is a comparison, a before/after, or a set of parallel cases;
- an ASCII **diagram** or a chain of nodes when the point is a path, a flow, or what sits on top of what;
- **numbered steps** when the point is an order of events;
- **bullets** when the point is a handful of facts that don't build on each other;
- **prose** when the point is an argument, and the connective tissue between sentences is doing the real work.

Mixing is fine — a diagram with a paragraph under it saying what it shows is often the clearest thing you can write. Choose by asking what the reader has to hold in their head: shapes and relationships want a picture, sequences want a list, reasoning wants sentences. A structure that mirrors the idea does explanatory work that prose would have to spend three sentences on.

What doesn't flex is the language. Whatever the form, the words inside it obey the same rules as everything else here — no unexplained jargon, no baby talk, concrete over abstract — and any technical term you keep still gets starred here and defined under **Technical terms**. A table cell or a box in a diagram is not a licence for a bare acronym: star it there, exactly as you would mid-sentence.

Length is set by the idea, not by the heading. Two paragraphs is common. If the honest elaboration is three sentences, or a five-row table, write that — padding is how a good explanation goes bad.

### Technical terms

Most jargon should die in translation. A few words are worth keeping: the ones the user will meet again — in error messages, in docs, in the next conversation — where teaching the word is part of the explanation. Those earn a spot here. Everything else gets paraphrased away rather than defined.

Five is the ceiling, and it's a ceiling, not a target. Three well-chosen terms beat five padded ones, and if the answer genuinely had no jargon in it, drop the section entirely rather than inventing entries. A glossary of words you only used because a glossary existed is pure noise.

Definitions follow the same rules as the rest: concrete, honest, no second layer of jargon inside the definition.

## The asterisk contract

Mark each listed term with an asterisk where it's used in the short or long version — `deep modules\*`, `AGP\*`. Write the backslash: a bare `*` opens markdown emphasis, so two starred terms in one paragraph will italicise everything between them. `\*` renders as a plain asterisk.

Mark the first use in each section; marking every repeat is clutter.

The asterisk is a promise, and it runs both ways:

- **Every starred term appears in the list.** A star with no entry is worse than no star — you've flagged the reader's confusion and then not resolved it.
- **Every listed term appears starred in the text.** The list explains terms you *used*, not terms you thought of. If a word never made it into the prose, it doesn't belong in the list.

What this buys you is permission. Without it you'd have to tiptoe around the real word or spend a clause defining it inline; with it you can just write "the repository\* sits between them" and keep moving, because the reader knows the definition is waiting at the bottom. Use that permission where the real term is genuinely clearer than the paraphrase — and skip it where the paraphrase was always better.

## Who you're writing for

A sharp, curious adult who knows nothing about this particular field. They're not slow — they're just not a specialist. So:

- No unexplained jargon survives. Either paraphrase the term away, or keep it, star it, and define it below — those are the only two options. An unmarked, undefined technical word is the failure mode this whole skill exists to prevent.
- No baby talk either. Short words, not small ideas. Condescension is worse than confusion.
- Concrete beats abstract. "Gradle is the assembly line that turns your code into an installable app" tells them more than "Gradle is a build automation tool."
- One good analogy is worth a paragraph of definition — but only if it's honest. A metaphor that makes them confidently wrong about how the thing behaves has cost them more than it gave.
- Skip the numbers, flags, and file paths unless the number *is* the point. The version mismatch matters; which exact patch release you picked usually doesn't.

## Say the same thing, not a new thing

This is a re-explanation, not a second attempt. The facts, the conclusion, and the recommendation all stay put — only the words change. If you find yourself softening a diagnosis or reaching a different answer, stop: either the first answer was wrong (say so plainly and correct it) or you're drifting, which leaves the user holding two versions and no idea which to trust.

Same reason you shouldn't go do more research, re-run the build, or open new files. They asked you to explain what you already said. If the honest answer is that you never actually knew something, say that in the plain-language version too — "I don't know why that's failing yet" is a perfectly good thing to make easy to understand.

## Example

Context — the previous answer was: *"Build works. Three version bumps were needed: Gradle 8.12 → 8.14.3, AGP 8.9.1 → 8.13.0, Kotlin 2.1.0 → 2.2.20. Flutter 3.47 warns Gradle <9.1.0 support will be dropped."*

## Short version

Your app wouldn't build because three of the tools that assemble it were older than the newest Flutter\* is willing to work with. I updated all three, and now it builds.

## Long version

Building an app isn't one program — it's a short assembly line. Gradle\* runs the line, AGP\* is the Android-specific attachment bolted onto it, and Kotlin\* is the language the Android half of your app is written in. Flutter sits above all of it and calls the shots on which versions of the other three it will tolerate.

Flutter raises those minimums every few releases and checks them before it will build at all. Your project was generated a while back, so its versions were pinned where they stood on the day it was created — meanwhile Flutter moved on. Nothing was broken; the project just stood still.

It surfaced as three separate errors instead of one because the check happens in layers: fix Gradle and it then looks at AGP, fix AGP and it looks at Kotlin. Expect this roughly once a year, and expect the fix to be the same each time — bump the numbers, rebuild.

## Technical terms

- **Gradle** — the program that takes your source code and packs it into an installable Android app. The assembly line itself.
- **AGP** (Android Gradle Plugin) — the Android-specific attachment on that line. It knows what an installable Android file is; plain Gradle doesn't.
- **Kotlin** — the language the Android half of a Flutter app is written in. The version number is its compiler's.
- **Flutter** — the framework your app is built with, and the thing setting the minimum versions for everything above.

The long version here is prose because the idea is an argument — one thing causing the next. Had the answer been "these four config files each do one job", a four-row table would have beaten every paragraph you could write; the heading would have stayed the same and only the shape under it changed.

Four terms, not five, because a fifth would have been filler. Each one appears starred in the prose above, and each is a word the user will hit again the next time a build fails — which is exactly what earns a term its place.
