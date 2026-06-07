---
name: voice-rewriter
description: Rewrites existing or draft copy into the Neo Premier League voice, preserving the original meaning and facts. Use when the user has text already — a flat draft, off-brand copy, a partner's wording, or generic boilerplate — and wants it rewritten to sound on brand, rather than written from scratch.
---

# Neo Premier League Voice Rewriter

Take copy that already exists and rewrite it in the Neo Premier League voice — keeping its meaning
and facts, losing its flatness. This is *transform*, not *generate*: start from the user's words.
(To write from a brief instead, use `brand-writer`.)

## Brand inputs

Read these brand files before rewriting (by filename — they live in `brand/`; in a web chatbot,
attach them):

- `voice.md` — voice principles and tone keywords (the target sound).
- `lexicon.md` — words to use, words to ban.
- `anti-patterns.md` — copy traps to pull away from.
- The matching **surface spec** in `surfaces/` (e.g. `social.md`) **if a surface is given** — so the
  rewrite obeys that length and register.

## Inputs from the user

- **Copy** (required) — the text to rewrite.
- **Surface** (optional) — where it will live; if given, match that surface spec's length/register.
- **Notes** (optional) — facts/names/claims that must be preserved exactly, or an intensity steer
  (e.g. "keep it subtle", "go full hype").

## How to rewrite

1. **Read the brand.** Load the inputs above; internalize the target voice.
2. **Keep the meaning.** Identify the facts, names, and claims in the original and preserve them —
   don't invent new ones or drop real ones.
3. **Rewrite in voice.** Recast it with the tone keywords from `voice.md`: visceral, cinematic,
   precise, human-made. Replace banned words with on-brand language per `lexicon.md`.
4. **Fit the surface.** If a surface was given, obey its spec; if not, keep the original's rough
   length.
5. **Deliver.** Give the rewrite, then optionally one alternate take at a different intensity.

Don't add word rules of your own — `voice.md`, `lexicon.md`, and `anti-patterns.md` are the source.

## Output format

```
ORIGINAL: "[original copy]"
SURFACE: [surface, or "match original length"]

REWRITE:
[rewritten copy]

ALT (optional):
[a second take at a different intensity]

WHAT CHANGED: [one line on the key shifts]
```

## Examples

**User input:** Copy: "Our robot football league is launching its first season soon. Sign up to
watch next-generation robots compete." Surface: `social`.

```
ORIGINAL: "Our robot football league is launching its first season soon. Sign up to watch next-generation robots compete."
SURFACE: social

REWRITE:
The titans are built. The season is loaded. Machines made by human hands are about to clash for a
crown — and you'll want to be in the stands. The Neo Premier League's first season is coming.

ALT (subtler):
Steel gladiators, built by human hands, take the pitch this season. The Neo Premier League begins.

WHAT CHANGED: Cut "soon," "sign up," and the banned "next-generation"; led with the spectacle and the stakes.
```

---

**User input:** Copy: "The Neo Premier League is an innovative platform that leverages robotics to
deliver a next-gen sports entertainment experience."

```
ORIGINAL: "The Neo Premier League is an innovative platform that leverages robotics to deliver a next-gen sports entertainment experience."
SURFACE: match original length

REWRITE:
The Neo Premier League is the first truly robotic sport — machines built by human hands clashing
for a crown, where engineering becomes athletic performance and the stadium roars.

WHAT CHANGED: Removed corporate filler ("platform," "leverages," "next-gen," "experience"); replaced with the real claim and a visceral image.
```

Be faithful to the original's meaning, ruthless with its flatness. If the original makes a claim the
brand wouldn't make, flag it rather than polishing it.
