---
title: Robot Character
type: visual-character
status: active
updated: 2026-06-07
source: approved media library (see assets/manifest.json); canonical = robot-solo + robot-360
---

# Robot Character

The Neo Premier League's athlete and mascot. One consistent character, worn in any of the team
kits. The canonical references are **`robot-solo`** (clean front) and **`robot-360`** (the full
turnaround) in the media library (see [`assets/README.md`](../../assets/README.md)) — every render
should trace back to them.

## The character (canonical)

A humanoid robot built like an athlete. Matte **black** throughout, greyscale only.

- **Build:** lean, athletic, human male-ish proportions. Reads as a player, not a tank.
- **Head:** *the signature.* No face. A horizontal **black camera-bar visor** — a rounded
  rectangular sensor slot with two circular lens elements — mounted on a segmented, ribbed neck
  column. Anonymous, stealthy, a little menacing. This is the brand's "face."
- **Surface:** matte black bodysuit-like skin over articulated mechanical structure. Subtle seams
  and a faint sternum line.
- **Limbs:** exposed mechanical joints — segmented armored thighs, visible knee actuators, jointed
  shins. Gloved mechanical hands.
- **Hips:** a utility belt / pelvic housing with mechanical detailing.
- **Feet:** black athletic sneakers/boots.

## Approved looks

Asset ids resolve via [`assets/manifest.json`](../../assets/manifest.json) → the media library.

| Look | Asset id | Use |
| --- | --- | --- |
| **Solo** | `robot-solo` | Canonical "base" character, clean front. |
| **360 turnaround** | `robot-360` | Definitive reference; five angles. |
| **Team kits** | `black-circuits` … `the-latents` | The 8 team kits (flat) — see [`kits.md`](kits.md). |
| **Kits on robot** | `<team>-360` (e.g. `forge-union-360`) | Each kit worn on the robot, in 360. |

The robot wears a team kit on the upper body; the legs stay the robot's matte-black mechanical
limbs. (The hooded glitch portrait used in treatment lives in the `neo-style-1` style board.)

## Fidelity rules (on-model checklist)

A render is **on-model** when:

1. **Head is the camera-bar visor** — horizontal sensor slot with twin lenses, on a ribbed neck.
   No face, no eyes, no mouth, no humanoid head.
2. **Matte black**, greyscale only — no color, no glossy chrome.
3. **Athletic human proportions** — lean and agile, not bulky/boxy/toy.
4. **Visible mechanical joints** at knees/limbs; gloved mechanical hands; sneaker-style feet.
5. **One character** — consistent body; the kit changes, the robot does not.

## Off-model (reject)

- A face, eyes, or a humanoid/helmet head instead of the camera-bar.
- Color, chrome/gloss, or a non-greyscale finish.
- Cute/toy proportions, chibi, or bulky mech-suit bulk.
- Fully covered limbs with no mechanical articulation (reads as a person in a suit).

The [`robot-fidelity-checker`](../../skills/robot-fidelity-checker/SKILL.md) skill scores images
against this checklist.
