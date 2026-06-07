---
title: Visual Identity
type: visual-identity
status: active
updated: 2026-06-06
source: brand owner direction + curated assets in assets/
---

# Visual Identity

The overall look of the Neo Premier League and the shape/overlay language that holds it together.
Specific sub-systems live in [`color.md`](color.md), [`typography.md`](typography.md),
[`robot-character.md`](robot-character.md), and [`treatment.md`](treatment.md).

## Look in one line

High-contrast **black-and-white**, matte-machine athletes shot like a sport, broken by **glitch**
and wrapped in a **HUD/telemetry** graphic system. Stealthy, cinematic, engineered, a little
dangerous.

## First principles

- **Greyscale only.** No color. The drama comes from contrast, texture, and motion — never hue.
  See [`color.md`](color.md).
- **Matte over gloss.** Surfaces read as worn, engineered matte black — not shiny showroom render.
  Gloss pulls us toward the cold-corporate-futurism we avoid ([`anti-patterns.md`](../anti-patterns.md)).
- **Shot like sport.** Real athletic posing, real action — volleys, headers, bicycle kicks — not
  a static product turntable.
- **Engineered overlays.** A layer of HUD/telemetry typography and registration marks frames the
  image like a broadcast feed or a build readout.
- **Break it with glitch.** Controlled datamosh/scan-tear conveys speed, signal, and chaos —
  always purposeful, never decoration ([`treatment.md`](treatment.md)).

## Shape & overlay language

The recurring graphic vocabulary (seen across `assets/style/` and the match kit):

- **Chevrons** — sharp downward angle-stacks (the kit's chest mark). Aggression, momentum, rank.
- **Bars / barcode stripes** — clusters of hard rectangular strokes. Data, speed, signal.
- **HUD telemetry blocks** — small mono-style label groups: `MATCH_PROTOCOL`, `SYNC_OK`,
  `// FUTURE_FORM`, ID strings, packet counts. The "build readout" layer.
- **Registration / corner ticks** — framing marks at the edges, like a targeting overlay.
- **Vertical side text** — rotated labels running up the margins.
- **Glitch tears** — horizontal datamosh streaks pulling pixels sideways.

Use these as a kit. A composition usually combines: a greyscale robot athlete + one or two shape
elements + a telemetry layer + (optionally) a glitch tear.

## Layout posture

- Generous negative space on near-white or near-black grounds; subject is the hero.
- Type is set in tight, condensed, uppercase blocks (see [`typography.md`](typography.md)) with
  small mono telemetry as counterpoint.
- Edge-anchored overlays (corners, margins) frame a centered or dynamically-posed subject.

## Reference assets

- Hero treatment: `assets/style/key-art-hero.png`
- Full system on a poster: `assets/style/key-art-poster.png`
- Match energy: `assets/style/key-art-header.png`
- The athlete: `assets/robot/` (archetype, hoodie, poses)
