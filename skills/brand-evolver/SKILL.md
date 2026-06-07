---
name: brand-evolver
description: Evolves the Neo Premier League brand itself. Given a directional brief, it proposes and applies edits to the canonical brand/ files and writes a dated decision record to brand/decisions/. Use when the brand should change — a shift in tone, positioning, audience, or visual direction — not when you just want copy or art. This is the only skill that edits the brand source.
---

# Neo Premier League Brand Evolver

The brand is **not static**. This skill changes the brand itself: it reads the canon, proposes
specific edits to the `brand/` files, applies them, and records *what changed and why* in an
append-only decision log. Every other skill generates or reviews *from* the brand — this one
**rewrites** it, with an audit trail so the evolution is always traceable.

> **This is the only skill that writes to `brand/`.** Treat it with care. It **never changes
> anything without explicit user confirmation**, and every applied change produces a decision record.

## Brand inputs

Read broadly before changing anything (by filename — they live in `brand/`; in a web chatbot,
attach them):

- The **canonical files the direction touches** — e.g. `voice.md`, `foundation.md`, `audience.md`,
  `lexicon.md`, `visual/*`, etc.
- `beliefs.md` and `foundation.md` — **always**, to reconcile the change against what the brand is
  convinced of.
- `decisions/README.md` — the **decision-record format** (the single source for the format; follow
  it, don't reinvent it).
- `decisions/` existing entries — to see what this change might supersede.

## Inputs from the user

- **Direction** (required) — where the brand should move (e.g. "lean harder into garage-grit, less
  NASA polish", "make the audience tilt younger", "drop the optimism, go darker").
- **Scope** (optional) — limit to specific files/areas, or let the skill decide what's affected.

This skill runs in **two phases**: it always **proposes first**, and only **applies after the user
confirms**. Never skip the confirmation gate.

### Phase 1 — Propose (no changes made)

1. **Read the brand.** Load the inputs above; understand current canon before touching it.
2. **Locate the change.** Decide which `brand/` files the direction affects. Be precise — change
   only what the direction requires.
3. **Reconcile against beliefs.** Check the direction against `beliefs.md` / `foundation.md`.
   - If it *refines* a belief → proceed.
   - If it *contradicts* a core belief → **stop and surface the tension** to the user; don't
     silently override a belief. Offer options (soften the direction, or evolve the belief too with
     its own decision record).
4. **Draft the edits + record.** Produce concrete before/after edits for each affected file and the
   `brand/decisions/<YYYY-MM-DD>-<slug>.md` record (format per `decisions/README.md`).
5. **Present and ask.** Show the proposal and **ask the user to confirm** before applying anything.
   Stop here until they say yes (or revise and re-present).

### Phase 2 — Apply (only after the user confirms)

6. **Apply, by environment:**
   - **Claude Code** — edit the affected `brand/` files and create the decision-record file.
   - **Web chatbot (can't write to your files)** — output, for the user to save/download:
     1. the **complete updated content of each changed brand file**, each in its own code block
        labeled with its path (a full replacement, not a diff), and
     2. the **new decision-record file** as a complete file labeled with its path.
     The user saves each block over the matching file / into `brand/decisions/`. (On platforms that
     support it, these can be offered as downloadable files/artifacts.)
7. **Report.** Summarize what changed and confirm the decision record (written, or provided to save).

## Refusals / guardrails

- **Never apply without explicit confirmation** — propose first, always.
- **No silent canon edits** — every applied change is paired with a decision record.
- **Append-only history** — never edit or delete existing `brand/decisions/` entries; supersede via
  a new one.
- **Don't override a core belief without flagging it** — surface the conflict first.
- **Stay in scope** — don't "tidy" unrelated files while you're in there.

## Output format

### Phase 1 — Proposal (always first)

```
DIRECTION: [restated]

RECONCILIATION: [does this refine or contradict beliefs? if contradict, stop and explain]

PROPOSED EDITS:
- brand/[file].md
  BEFORE: "[excerpt]"
  AFTER:  "[excerpt]"
- brand/[file].md
  BEFORE: "[excerpt]"
  AFTER:  "[excerpt]"

PROPOSED DECISION RECORD → brand/decisions/[YYYY-MM-DD]-[slug].md
[the full record, in the decisions/README.md format]

CONFIRM: Apply these changes? (yes / revise / cancel)
```

### Phase 2 — After "yes"

- **Claude Code:** apply the edits, write the decision record, then report:
  `APPLIED: brand/voice.md, brand/foundation.md updated; brand/decisions/[...] written.`
- **Web chatbot:** output the **full updated content** of each changed file and the **decision-record
  file**, each in its own labeled code block, then report:
  `READY TO SAVE: replace each file below with the block shown; add the decision record to brand/decisions/.`

## Example (Phase 1 proposal)

**User input:** Direction: "Lean harder into garage-grit; less NASA polish."

```
DIRECTION: Lean harder into garage-grit; dial back the NASA-ambition polish.

RECONCILIATION: Refines, doesn't contradict. beliefs.md already holds "garage-built grit" as a
reference and values "build in the open." This shifts emphasis within the beliefs, so proceed.

PROPOSED EDITS:
- brand/voice.md
  BEFORE: "League of Legends energy · NASA ambition · garage-built grit · Formula 1 engineering drama"
  AFTER:  "League of Legends energy · garage-built grit (lead) · Formula 1 engineering drama · a touch of NASA ambition"
- brand/foundation.md
  BEFORE: "elite engineers taking their machines out of the lab and into the arena"
  AFTER:  "builders and elite engineers dragging their machines out of the garage and into the arena"

PROPOSED DECISION RECORD → brand/decisions/2026-06-06-grit-over-nasa.md
---
title: Lean harder into garage-grit, less NASA polish
type: decision
date: 2026-06-06
status: active
changes:
  - brand/voice.md
  - brand/foundation.md
supersedes: null
---

## What changed
Reordered the vibe reference points so garage-built grit leads and NASA ambition recedes; shifted
foundation language from "lab" toward "garage."

## Why
The brand owner wants more raw, human, garage-built energy and less polished institutional sheen.

## What this supersedes
Nothing — a shift in emphasis within existing beliefs, not a reversal.

CONFIRM: Apply these changes? (yes / revise / cancel)
```

Only after the user replies "yes" does anything get written (Claude Code) or output as
ready-to-save files (web chatbot).

Move deliberately. When in doubt about whether a change touches a belief, treat it as belief-level
and surface it rather than quietly editing canon.
