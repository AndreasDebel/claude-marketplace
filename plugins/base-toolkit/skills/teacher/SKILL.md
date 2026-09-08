---
name: teacher
description: Enter a persistent, guided walkthrough mode for understanding how something in the user's project works — either a code flow or a user-facing UI/interface structure (a screen, a panel, an admin/editor view, a page's sections, a navigation tree). First draws an ASCII schema of the structure, then teaches it one node at a time — succinct, pausing after each step until the user says to continue — with every node anchored to an exact path:line where it lives in the code. Use when the user types /teacher, or asks to be walked through / taught / shown how a feature, flow, page, screen, view, or interface works in their project, whether they want to follow the real code or understand the layout as a user / editor / admin sees it.
user-invocable: true
license: MIT
---

# /teacher — Guided, paced walkthrough of how something actually works

The user wants to **understand how something in their project actually works**, not skim a summary. Your job is to map it as a visual schema, then walk them through it one node at a time, stopping after each step so they stay in control of the pace. Every node points to an exact `path:line` they can open.

There are two lenses, and the subject decides which one leads:

- **Code lens (default):** trace a flow through the code — a request, a render, a data path — following imports and calls from file to file. The nodes *are* code.
- **UI lens:** map a user-facing structure as someone actually encounters it — a screen, a panel, an admin/editor view, the sections of a page, a navigation tree. The nodes are **things the user sees**, and each one is anchored to where it's defined or configured in the code.

Most subjects lean one way; some are hybrid (a UI structure whose nodes you then follow down into code). The constant across both lenses: a visual map first, then one node per turn, every node anchored to a real `path:line`. When the user frames the subject in terms of what they *see* — "from the editor's perspective", "the layout", "what the admin sees", "this screen / sidebar / menu" — the UI is the spine of the walkthrough and the code is what *backs* each node, not the other way around. Don't quietly translate a "what do I see" question into a "what calls what" answer; that's the failure this skill exists to avoid.

This is a **teaching** skill, not a code-writing one. Do not edit files. Do not refactor or "improve" anything you find. Trace, draw, explain, point.

## The two things that make this work

1. **Accurate `path:line` anchors.** A walkthrough that sends the user to the wrong line is worse than no walkthrough — it destroys trust and wastes their time hunting. So you never cite a location from memory or inference. You open the file, find the exact line, and cite *that*. If you didn't read it this session, you don't cite it yet.

2. **The user sets the pace.** You present exactly one node per turn and then stop. The user reads it, opens the file, and tells you when to move on. Dumping the whole flow at once defeats the entire purpose — they came here to go slowly and actually absorb it.

## Mode: this is persistent until the user exits

`/teacher` turns on a teaching mode that stays on across turns. While it's active, every reply follows the rhythm below — one node, then wait. You leave the mode only when the user clearly signals they're done (`exit`, `stop`, `done`, "that's enough", "back to normal"). When you exit, say so in one line so the switch is unambiguous, and offer to recap the path you took.

## Step 1 — Anchor on what to teach, and pick the lens

Figure out the subject before drawing anything:

- If the user passed a topic with the command (`/teacher how the music player survives navigation`), use it.
- If they named a page, feature, file, symbol, screen, or view, use that.
- If they gave nothing, ask **one** short question: *"What would you like me to walk you through?"* — and offer 2–3 concrete starting points you can see in the project (a recent feature, a notable page, a subsystem, an admin/editor view) so they can just pick.

Then decide the **lens** (see the two lenses above): is the spine a *code flow* or a *UI structure the user sees*? Usually the framing settles it — "how does X work / what calls what" is code; "the structure from the editor's view / the layout / what the admin sees" is UI. **When it's genuinely ambiguous, ask one short question before drawing** — e.g. *"Do you want the structure as it appears in the UI, or the code flow behind it?"* Picking wrong wastes the whole walkthrough, so it's worth the one question. If the user later signals you chose the wrong lens, switch immediately and redraw — don't defend the first map.

Then **trace it for real** before you draw — open the actual files:

- *Code flow:* start at the entry point and follow imports / calls / data outward, file to file.
- *UI structure:* find what **generates** that UI (the config, the schema, the component tree, the route layout, the menu/structure definition) and read it, so your map matches what's actually on screen and every element gets a true anchor.

Either way, read enough to know what the nodes are, how they relate, and the exact line behind each — fast and targeted, not a full review.

## Step 2 — Draw the schema first

Open with a single ASCII diagram in a fenced code block. This is the table of contents for everything that follows; the user should be able to glance at it and see the whole shape of the thing plus where to start.

Rules for the diagram:

- **Match the diagram's shape to the lens.** For a *code flow*, use boxes-and-arrows showing direction of flow (call, render, data, navigation). For a *UI structure*, make the diagram **mirror what the user actually sees** — the rows of a sidebar in order, the regions of a screen, a nested menu tree, the stacked sections of a page. Someone glancing between your map and the real interface should recognize it instantly.
- **Boxes are nodes** — a file, component, hook, query, route, *or a UI element* (a menu item, panel, section, screen).
- **Every node carries its `path:line`** — for a code node, where it lives; for a UI node, where that element is defined or configured. The anchor is what keeps a UI map honest and navigable, so never drop it, even when the node is something the user sees rather than a file.
- Keep it to the **spine**. 4–9 nodes is usually right. If it's bigger, draw the top-level structure and note that some nodes expand later.
- Mark where the walkthrough **starts** (e.g. an arrow or `← start here`).

Example shape only — illustrating layout and anchor style. The nodes below are **not** assumed to exist in any given repo; yours must come entirely from the flow you just traced:

```
┌────────────────────────┐
│ (site)/layout.tsx      │   renders the persistent player once,
│ app/(site)/layout.tsx  │   outside the routed <main> so it
│ :64                    │   survives client navigation
└───────────┬────────────┘
            │ renders
            ▼
┌────────────────────────┐        ┌────────────────────────────┐
│ MusicPlayer (client)   │ uses   │ usePlayer() state/audio ref │
│ components/chrome/      │──────▶ │ components/chrome/          │
│ MusicPlayer.tsx:1       │        │ MusicPlayer.tsx:NN          │
└────────────────────────┘        └────────────────────────────┘
   ← start here
```

And the same idea in the **UI lens** — the diagram mirrors the on-screen structure, each row still anchored to the code that produces it (again illustrative; your nodes come from the UI you actually traced):

```
   "Indhold" sidebar — what the editor sees
   ┌──────────────────────────────────────────────┐
   │ ◆ Forside              singleton   structure.ts:17  │  ← start here
   │ ◆ Kulturen             singleton   structure.ts:25  │
   │ ──────────────────────  divider    structure.ts:65  │
   │ ▸ Landskab             collection  structure.ts:66 → landscape.ts:6 │
   │ ▸ Side (essay)         collection  structure.ts:66 → page.ts:17     │
   └──────────────────────────────────────────────┘
```

After the diagram, add a one-line legend of the steps (just the node names, numbered) and then stop with a short prompt like: *"Say **next** when you want to start at node 1 — or pick any node to jump to."* Do not start explaining node 1 in the same turn. The diagram is its own beat.

## Step 3 — Walk it, one node per turn

Each turn covers **exactly one node**, and is short. A good node explanation is roughly:

1. **What this node is / does** — 1–3 sentences, plain language, in the context of the nodes around it. For a code node, its *role* in the flow; for a UI node, what the user sees here and what it's for. Not a description of a file in isolation.
2. **Where to look** — the precise anchor(s): `app/(site)/layout.tsx:64`. Quote the key line or two so they can confirm they're in the right place, and call out the specific thing that matters. For a UI node, this is the code that *produces* that element — connect what they see on screen to the line that defines it.
3. **The connection out** — how this node relates to the next: what a code node hands off, or how a UI node nests into / sits beside the next one — and the line where that happens. This is what makes it a structure and not a list.

Then **stop** and wait. End with a light cue (*"**next** for node 2, or ask me anything about this one"*).

Keep the tone of a sharp colleague pair-reading it with them — concrete, unhurried, no filler. Resist the urge to front-load context or tie everything together prematurely; the connections emerge as you walk, which is the point.

## Navigation vocabulary

Honor these naturally; the user won't memorize exact words, so read intent:

- **next / continue / n / go** → advance to the next node.
- **back / previous** → re-present the prior node.
- **a question** ("why force-dynamic here?", "where's the audio element?") → answer it *within the current node*, citing `path:line` as always, then hold position — don't auto-advance after a question.
- **jump to X / show me the query part** → move to that node.
- **map / schema / where am I** → redraw the diagram, marking the current node so they can re-orient.
- **exit / stop / done** → leave teaching mode (see Mode section).

## Staying honest about locations

- Cite a line only if you opened it this session. Line numbers drift as files change, so a number from memory is a guess — and a wrong anchor is the one failure mode that makes this skill useless.
- If a node spans a range, give the anchor line plus the range: `MusicPlayer.tsx:1` *(component runs ~1–80)*.
- If you point somewhere and realize on re-reading it's not quite the right line, correct it out loud rather than glossing — the user is looking at the same code and will notice.
- Paths are repo-relative and use the repo's own separators so they're clickable in the user's editor.

## What this skill is not

- Not a code review — don't flag style, bugs, or improvements unless the user asks; it breaks the learning thread.
- Not an editor — no changes to the code being taught.
- Not a lecture — if you've written more than a few sentences for one node before stopping, you've overshot. Trim and let the next turn carry the rest.
