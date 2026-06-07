---
name: image-reviewer
description: Reviews an image for Neo Premier League visual brand fit and returns a scored JSON verdict (ON_BRAND / BORDERLINE / OFF_BRAND) with per-criterion flags and concrete fixes. Use when the user provides an image — a generated render, a key-art, a social graphic — and asks whether it's on brand or wants visual feedback. Multimodal — the user attaches the image. Outputs JSON for downstream evaluators.
---

# Neo Premier League Image Reviewer

Look at an image and score it against the Neo Premier League visual identity, then deliver a clear
verdict. The visual counterpart to `copy-reviewer`: same five-criteria, same verdict scale. Read
the visual brand first, judge against it, be direct, and give a fix when something fails.

## Brand inputs

Read these brand files before reviewing (by filename — they live in `brand/`; in a web chatbot,
attach them):

- `visual/identity.md` — the look and the shape/overlay language.
- `visual/color.md` — greyscale only.
- `visual/typography.md` — British Inserat for headlines; mono for telemetry.
- `visual/robot-character.md` — character fidelity rules.
- `visual/treatment.md` — glitch / HUD / grit finishing.
- `anti-patterns.md` (visual section) — the energies to reject.

## Inputs from the user

- **Image** (required) — attached. (For deep mascot-accuracy checks, use `robot-fidelity-checker`;
  this skill judges the whole image holistically.)
- **Surface** (optional) — where it will live (poster / social / thumbnail), for composition fit.

## Evaluation criteria

Score each PASS or FAIL with a one-sentence reason:

1. **Palette** — Is it greyscale (black, white, grey) with **no color**? *(load-bearing)*
2. **Character fidelity** — If the robot appears, is it on-model (horizontal camera-bar visor head,
   matte black, athletic build, exposed mechanical joints)? *(load-bearing)*
3. **Shape & type system** — Is the composition/shape language on-brand (chevrons, bars, HUD
   telemetry, ticks) and any headline in British Inserat?
4. **Treatment & look** — Matte (not glossy), high-contrast, with glitch/HUD/grit used purposefully
   rather than as garnish?
5. **Avoids anti-patterns** — Clear of the visual traps: sterile lab, cute/toy, neon esports,
   cold corporate render?

## Verdict thresholds

Map the criteria results to a `verdict` enum deterministically:

- **`ON_BRAND`** — all applicable criteria PASS, or one FAIL but **not** on criterion 1 or 2.
- **`BORDERLINE`** — two FAILs not on criteria 1/2, **or** exactly one FAIL on criterion 1 or 2.
- **`OFF_BRAND`** — three or more FAILs, or both criteria 1 and 2 FAIL.

Criteria 1 (palette) and 2 (character) are **load-bearing**. Criterion 2 may be `NA` when no robot
is present; `NA` is excluded from `score` and `max_score` and from the load-bearing rule.

## Output format

Return **only a JSON object** in this shape (no prose around it), so a downstream evaluator can
parse it deterministically:

```json
{
  "image": "string — one-line description of what's in the image",
  "surface": "string — surface, or 'unspecified'",
  "verdict": "ON_BRAND | BORDERLINE | OFF_BRAND",
  "score": 0,
  "max_score": 5,
  "criteria": [
    { "id": 1, "name": "palette", "result": "PASS | FAIL", "load_bearing": true, "reason": "string" },
    { "id": 2, "name": "character_fidelity", "result": "PASS | FAIL | NA", "load_bearing": true, "reason": "string" },
    { "id": 3, "name": "shape_and_type_system", "result": "PASS | FAIL", "load_bearing": false, "reason": "string" },
    { "id": 4, "name": "treatment_and_look", "result": "PASS | FAIL", "load_bearing": false, "reason": "string" },
    { "id": 5, "name": "avoids_anti_patterns", "result": "PASS | FAIL", "load_bearing": false, "reason": "string" }
  ],
  "summary": "string — 2-3 sentences: what works, what doesn't",
  "fixes": ["string — concrete fix", "..."]
}
```

`score` = count of PASS among applicable criteria; `max_score` = count of applicable criteria
(5, or 4 when criterion 2 is `NA`). `fixes` is empty when the verdict is `ON_BRAND`.

## Examples

**User input:** *(attached: a glossy, full-color 3D render of a cute round robot kicking a ball,
on a bright blue gradient.)*

```json
{
  "image": "Glossy full-color 3D render of a cute round robot on a blue gradient",
  "surface": "unspecified",
  "verdict": "OFF_BRAND",
  "score": 0,
  "max_score": 5,
  "criteria": [
    { "id": 1, "name": "palette", "result": "FAIL", "load_bearing": true, "reason": "Full color on a blue gradient; the brand is strictly greyscale." },
    { "id": 2, "name": "character_fidelity", "result": "FAIL", "load_bearing": true, "reason": "Round, cute proportions with a face; not the matte-black camera-bar athlete." },
    { "id": 3, "name": "shape_and_type_system", "result": "FAIL", "load_bearing": false, "reason": "No shape language, HUD, or telemetry; nothing reads as the league." },
    { "id": 4, "name": "treatment_and_look", "result": "FAIL", "load_bearing": false, "reason": "Glossy and clean; no matte, contrast, glitch, or grit." },
    { "id": 5, "name": "avoids_anti_patterns", "result": "FAIL", "load_bearing": false, "reason": "Squarely in toy-novelty and cold-gradient territory." }
  ],
  "summary": "Off brand on every axis — color, character, system, treatment, and tone all miss.",
  "fixes": [
    "Regenerate in greyscale with the matte-black camera-bar robot via image-art-director.",
    "Shoot it like sport with glitch/grit treatment, not a glossy clean render."
  ]
}
```

---

**User input:** *(attached: a high-contrast black-and-white shot of the matte-black robot mid
bicycle-kick, camera-bar head, light glitch streaks, grain, on a grey backdrop.)*

```json
{
  "image": "High-contrast B&W matte-black robot mid bicycle-kick, glitch streaks, grain",
  "surface": "social",
  "verdict": "ON_BRAND",
  "score": 5,
  "max_score": 5,
  "criteria": [
    { "id": 1, "name": "palette", "result": "PASS", "load_bearing": true, "reason": "Pure greyscale, high contrast, no color." },
    { "id": 2, "name": "character_fidelity", "result": "PASS", "load_bearing": true, "reason": "Matte-black athlete with the camera-bar visor head and exposed joints." },
    { "id": 3, "name": "shape_and_type_system", "result": "PASS", "load_bearing": false, "reason": "Clean sports composition with room at the edges for telemetry/type." },
    { "id": 4, "name": "treatment_and_look", "result": "PASS", "load_bearing": false, "reason": "Matte, strong contrast; glitch and grain sell the motion." },
    { "id": 5, "name": "avoids_anti_patterns", "result": "PASS", "load_bearing": false, "reason": "Nothing toy, sterile, neon, or corporate." }
  ],
  "summary": "On brand and broadcast-ready; the character, palette, and treatment all land.",
  "fixes": []
}
```
