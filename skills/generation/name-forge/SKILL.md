---
name: name-forge
description: Generates on-brand Neo Premier League names for teams, robots, tournaments, arenas, and signature moves, following the brand's naming conventions. Use when the user needs to name something in the league — a new team, a robot/machine, a tournament or season, a venue, or a signature move/play — and wants ranked options with rationale.
---

# Neo Premier League Name Forge

Generate names for things inside the league — teams, robots, tournaments, arenas, signature moves —
that obey the brand's naming conventions and sound unmistakably Neo Premier League: engineered,
heroic, a little dangerous.

## Brand inputs

Read these brand files before naming (by filename — they live in `brand/`; in a web chatbot,
attach them):

- `lexicon.md` — **naming conventions** (the per-category rules + house style) and banned words.
- `voice.md` — tone keywords, so names sound on-voice.
- `anti-patterns.md` — name traps to avoid (toy/novelty, corporate, etc.).

## Inputs from the user

- **Category** (required) — what's being named: `team`, `robot`, `tournament`, `arena`, or `move`.
  (For anything else, describe it and the closest convention will be applied.)
- **Brief** (optional) — theme, origin, personality, or constraints (e.g. "scrappy underdog from
  Detroit", "a final with everything on the line", "a brutal aerial finish").
- **Count** (optional) — how many candidates (default 8).

If no category is given, ask — the convention depends on it.

## How to forge

1. **Load the conventions.** Read the matching naming convention in `lexicon.md` for the category,
   plus the house style and banned words.
2. **Mine the brief.** Pull the theme/origin/personality into the naming (a Detroit underdog leans
   industrial, blue-collar, chip-on-shoulder).
3. **Generate widely, then cut.** Produce more than asked, then keep the strongest `count` that fit
   the category's convention and house style from `lexicon.md`. (Don't apply extra word rules of
   your own — `lexicon.md` is the single source.)
4. **Rank and rationalize.** Order best-first; give each a one-line reason. Name a single TOP PICK.

## Output format

```
CATEGORY: [category]
BRIEF: [one-line restatement, or "open"]

CANDIDATES (ranked):
1. [Name] — [one-line rationale]
2. [Name] — [one-line rationale]
...

TOP PICK: [Name] — [why this one wins]
```

## Examples

**User input:** Category: `team`. Brief: "scrappy underdog from Detroit, blue-collar, chip on its shoulder." Count: 6.

```
CATEGORY: team
BRIEF: Detroit underdog — industrial, blue-collar, chip on its shoulder

CANDIDATES (ranked):
1. Motor City Maulers — roots it in Detroit and hits hard; alliteration reads on a jersey.
2. Forge Union — blue-collar "union" + the heat of the build; tribal and proud.
3. The Assembly — double meaning (assembly line + a gathering of fighters); understated menace.
4. Rustbelt — one word, defiant, owns the underdog identity.
5. Dynamo Iron — Detroit dynamo energy with weight behind it.
6. Hammerline — the line where things get built and broken.

TOP PICK: Forge Union — it carries the build, the grit, and the brotherhood in two hard syllables.
```

---

**User input:** Category: `robot`. Brief: "a fast, agile striker." Count: 6.

```
CATEGORY: robot
BRIEF: Fast, agile striker

CANDIDATES (ranked):
1. VX-9 "Razorfoot" — model tag + a fighting name that screams pace and a lethal touch.
2. Mach "Switchblade" — speed plus a quick, dangerous edge.
3. KR-7 "Quickstrike" — engineered designation with a striker's instinct.
4. "Tempest" Unit-04 — storm-fast, name-forward.
5. Halverson "Flux" — a built thing that never stops moving.
6. "Whip" SR-2 — short, fast, cracks like the move it makes.

TOP PICK: VX-9 "Razorfoot" — the model-tag + fighting-name pairing is pure league, and "Razorfoot" sells the striker.
```

---

**User input:** Category: `move`. Brief: "a brutal mid-air bicycle-kick finish." Count: 6.

```
CATEGORY: move
BRIEF: Brutal mid-air bicycle-kick finish

CANDIDATES (ranked):
1. The Guillotine — drops out of the air with finality; a commentator screams it.
2. Steel Arc — the shape of the kick plus the material; clean and visceral.
3. Overdrive — mechanical and explosive, fits the airborne snap.
4. The Backbreaker — brutal, inverted, unmistakable.
5. Skyfall Strike — height + impact in two beats.
6. Reverse Thunder — the bicycle motion as a thunderclap.

TOP PICK: The Guillotine — three syllables, instantly callable, and it lands with the right menace.
```

Be decisive. If the brief is thin, forge anyway and note the assumption. If a requested direction
fights the conventions or hits a banned word, say so and offer the on-brand alternative.
