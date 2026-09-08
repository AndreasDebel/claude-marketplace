<!--
CANONICAL SOURCE. Both /barebone-plan and /barebone-claude-md read this file, and
/barebone-claude-md copies the block below verbatim into a repo's CLAUDE.md. Edit the
rules here and nowhere else, so the two enforcement paths never drift apart.

Everything between the BEGIN and END markers is the injectable block. Keep it short
enough to live permanently in a CLAUDE.md without crowding out the repo's own notes.
-->

<!-- BEGIN BAREBONE BLOCK -->
## Barebone principles

This is a **learning repository**. Its code is read by a student trying to understand an
architecture, not run by users who depend on it. Optimise every line for *"a beginner can
follow this in one pass"* — not for robustness, generality, or elegance. The usual
production instincts are the thing making this code unreadable, so set them down here.

1. **One scenario.** Name the single concrete case the code must handle, then build for
   exactly that: one request shape, one file format, one caller, one happy user. Writing
   for inputs nothing sends yet is the largest single source of code a student can't
   follow — it adds branches whose motivation is invisible in the repo.
2. **Happy path only.** No guards, retries, `try`/`catch`, fallbacks, or error branches —
   unless the failure *is* the mechanism being taught. A crash is an acceptable and
   informative outcome here; it points straight at the line that broke.
3. **One representation per concept.** One class or record per idea, used end to end. No
   DTOs, no mappers, no translation layers. If a type is awkward to serialise or share,
   change that type — adding a layer to avoid touching code you own trades one edit for a
   permanent extra hop the reader must follow.
4. **No interface until the second implementation actually runs.** An abstraction earns
   its place by having two live callers *today*, not by being plausible later. One
   interface with one implementation is a file the reader opens for nothing.
5. **Spelled out beats clever.** A six-line `foreach` a student can trace beats a one-line
   LINQ chain. Fewer lines is not the goal; fewer things to hold in your head at once is.
   Prefer obvious names and explicit steps over compression.
6. **Leave simple code alone.** If a file already reads cleanly, don't restructure it.
   Churn costs the reader more than it saves.

**Dropped on purpose, not forgotten.** Error handling, validation, and generality get
added back on request, once the mechanism underneath is understood. So whenever you skip
something a production version would have, say so in one line — in the plan, or in a code
comment. Silent narrowing is how simple code turns into subtly wrong code.
<!-- END BAREBONE BLOCK -->
