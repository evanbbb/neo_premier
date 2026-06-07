---
title: Robot Character
type: visual-character
status: active
updated: 2026-06-06
source: curated assets in assets/robot/ (archetype = no shirt.png)
---

# Robot Character

The Neo Premier League's athlete and mascot. One consistent character, shown in multiple looks.
The canonical reference is **`assets/robot/archetype.png`** — every render should trace back to it.

## The archetype (canonical)

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

| Look | Asset | Use |
| --- | --- | --- |
| **Archetype** | `assets/robot/archetype.png` | Canonical reference; "base" character. |
| **Hoodie (full)** | `assets/robot/hoodie.png` | Streetwear/culture vibe; off-pitch identity. |
| **Hoodie portrait** | `assets/robot/hoodie-portrait.png` | The iconic head-in-hood shot; avatars, hero. |
| **Match kit** | `assets/robot/pose-uniform.png` | On-pitch: white chevron jersey + black underlayer/legs. |
| **Action** | `assets/robot/pose-volley.png`, `assets/robot/pose-bicycle-kick.png` | Dynamic football moments. |

## Fidelity rules (on-model checklist)

A render is **on-model** when:

1. **Head is the camera-bar visor** — horizontal sensor slot with twin lenses, on a ribbed neck.
   No face, no eyes, no mouth, no humanoid head.
2. **Matte black**, greyscale only — no color, no glossy chrome.
3. **Athletic human proportions** — lean and agile, not bulky/boxy/toy.
4. **Visible mechanical joints** at knees/limbs; gloved mechanical hands; sneaker-style feet.
5. **One character** — consistent body; looks change (hoodie/kit), the robot does not.

## Off-model (reject)

- A face, eyes, or a humanoid/helmet head instead of the camera-bar.
- Color, chrome/gloss, or a non-greyscale finish.
- Cute/toy proportions, chibi, or bulky mech-suit bulk.
- Fully covered limbs with no mechanical articulation (reads as a person in a suit).

The [`robot-fidelity-checker`](../../skills/robot-fidelity-checker/SKILL.md) skill scores images
against this checklist.
