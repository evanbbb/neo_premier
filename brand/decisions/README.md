# brand/decisions/ — the evolution log

The brand is **not static**. Whenever a canonical `brand/` file changes in a meaningful way, a
dated record is added here. This is an **append-only audit trail** — add new entries, never rewrite
old ones. The `skills/brand-evolver` skill **produces** a decision record (along with the proposed
edits) for you to save into this folder; you can also write one by hand.

## File naming

`YYYY-MM-DD-short-slug.md` — e.g. `2026-06-06-grit-over-nasa.md`. If two decisions land on the
same day, add a numeric suffix (`-2`).

## Record format

```markdown
---
title: Lean harder into garage-grit, less NASA polish
type: decision
date: 2026-06-06
status: active
changes:
  - brand/voice.md
  - brand/foundation.md
supersedes: null   # or the slug of an earlier decision this overrides
---

## What changed
One or two sentences on the concrete edit(s).

## Why
The reasoning / trigger for the change.

## What this supersedes
Link to any earlier decision or wording this replaces (or "nothing — new direction").
```
