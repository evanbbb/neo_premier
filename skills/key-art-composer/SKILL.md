---
name: key-art-composer
description: Composes an on-brand key-art layout for the Neo Premier League for a specific surface (poster, social key-art, thumbnail) from a concept. Use when the user needs art direction for a finished piece — composition, focal hierarchy, type placement, shape/overlay usage, and the hero image — not just a single generation prompt. Pairs with image-art-director for the hero image.
---

# Neo Premier League Key-Art Composer

Take a concept and a surface and lay out the finished key art: where the hero sits, the focal
order, how the **headline (type)**, the HUD/telemetry system, and the shape-language elements are
placed. This is **art direction / composition** — it **adds the type and design system on top of an
image**; it does **not** generate the underlying image.

**Where the image comes from:** the hero picture (e.g. robots playing soccer) is made by
`image-art-director` or supplied as an attachment. This skill arranges everything *around and over*
that image — the typeset, finished poster/social/thumbnail. Division of labor:

- `image-art-director` → the underlying **image** (no type).
- `key-art-composer` → the **layout + headline + telemetry + shapes** over that image.

## Brand inputs

Read these brand files before composing (by filename — they live in `brand/`; in a web chatbot,
attach them):

- `visual/identity.md` — the look and the **shape/overlay language** (chevrons, bars, HUD, ticks).
- `visual/typography.md` — British Inserat for headlines; mono for telemetry.
- `visual/color.md` — greyscale only.
- `visual/treatment.md` — glitch / HUD / grit finishing.
- `visual/robot-character.md` — so the hero stays on-model.
- The matching **surface spec** in `surfaces/` if the surface is also a copy surface (for headline
  length/register).

**Reference images are attachments, not paths** (same as `image-art-director`): describe what to
attach by role + description; never emit file paths.

## Inputs from the user

- **Hero image** (expected) — the **approved underlying image** to compose over, attached. Standard
  flow: it's already been made by `image-art-director` and approved by the reviewers. If no image
  exists yet, this skill can fall back to emitting an `image-art-director` brief (see step 4).
- **Concept** (required) — the idea to express (often a concept from `campaign-strategist`).
- **Surface** (required) — `poster`, `social`, or `thumbnail` (sets aspect ratio + composition).
- **Headline** (optional) — the approved copy (from `brand-writer`); if absent, suggest one.
- **Notes** (optional) — mood, must-include elements, constraints.

## How to compose

1. **Read the visual brand + surface.** Load the inputs above; lock the aspect ratio for the surface.
2. **Set the focal hierarchy.** Decide what the eye hits first (usually the hero image), then second
   (headline), then third (telemetry / shape elements). Everything serves that order.
3. **Place the system over the image.** Position the headline (British Inserat, uppercase), the
   HUD/telemetry layer (edges/corners), and the shape elements (chevrons/bars) on top of the hero
   image using `identity.md` — leaving the image to read.
4. **Hero image.** Normally you compose over the **approved attached image**. Only if no image
   exists yet, emit an `image-art-director` brief in `hero_image.image_art_director_handoff` so one
   can be generated first, then re-run this skill.
5. **Hold the look.** Greyscale only; matte; glitch/grit per `treatment.md`; generous negative space.
6. **Deliver as JSON** in the format below.

## Output format

Return **only a JSON object** in this shape (no prose around it):

```json
{
  "concept": "string — restated concept",
  "surface": "string — surface + aspect ratio",
  "layout": {
    "composition": "string — the overall arrangement / zones",
    "focal_point": "string — the hero element and where it sits",
    "headline_zone": "string — where the headline goes",
    "telemetry_zone": "string — where HUD/telemetry marks sit",
    "negative_space": "string — where it breathes"
  },
  "focal_hierarchy": ["1 — ...", "2 — ...", "3 — ..."],
  "type": {
    "headline": "string — the headline (British Inserat, uppercase)",
    "placement": "string",
    "telemetry": "string — mono labels to include"
  },
  "shape_language": ["string — element + placement", "..."],
  "palette_treatment": "string — greyscale + glitch/grit notes",
  "hero_image": {
    "source": "approved_attachment | needs_generation",
    "description": "string — what the hero image shows",
    "image_art_director_handoff": "string — ONLY when source is needs_generation: the subject to pass to image-art-director; empty otherwise"
  },
  "attachments": [
    { "role": "hero_image | treatment | other", "description": "what to attach and why" }
  ]
}
```

## Example

**User input:** Concept: "Witness History — the night the lab became an arena." Surface: poster.
Headline: "WITNESS HISTORY".

```json
{
  "concept": "Witness History — the night the lab became an arena",
  "surface": "poster (A1, portrait 2:3)",
  "layout": {
    "composition": "Single hero robot, centered and slightly low, rising into a tall portrait frame on a near-white ground; system marks framing the edges.",
    "focal_point": "The hooded robot, camera-bar head at the upper third — the eye lands there first.",
    "headline_zone": "Lower third, full-width, baseline-anchored.",
    "telemetry_zone": "Top-left and right margins + corner registration ticks.",
    "negative_space": "Generous around the figure; the white does the breathing."
  },
  "focal_hierarchy": [
    "1 — the robot's camera-bar head",
    "2 — the WITNESS HISTORY headline",
    "3 — telemetry marks + a single chevron cluster"
  ],
  "type": {
    "headline": "WITNESS HISTORY",
    "placement": "Lower third, British Inserat, uppercase, huge, tight tracking, ink on paper.",
    "telemetry": "// FIRST_SEASON 001 · MATCH_PROTOCOL · SYNC_OK"
  },
  "shape_language": [
    "A single downward chevron cluster behind the headline for momentum",
    "Corner registration ticks framing the poster",
    "Vertical mono label running up the left margin"
  ],
  "palette_treatment": "Greyscale only; matte black figure on near-white; restrained horizontal glitch tear off the figure's edge; light photocopy grit overall.",
  "hero_image": {
    "source": "approved_attachment",
    "description": "The approved hooded matte-black robot portrait, head-on, camera-bar visor, heroic and still.",
    "image_art_director_handoff": ""
  },
  "attachments": [
    { "role": "hero_image", "description": "the approved hooded-robot image to compose the type over" }
  ]
}
```

Compose for the surface and protect the focal order. Greyscale, British Inserat, and the
shape/overlay system are non-negotiable — they are what make it read as Neo Premier League.
