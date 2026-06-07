---
title: Team Kits
type: visual-kits
status: active
updated: 2026-06-07
source: approved media library (robot/kits/) — see assets/manifest.json
---

# Team Kits

The league fields **8 teams**, and each team has its own **kit** (jersey). The kits share one
greyscale system but each carries a distinct graphic identity, so teams read apart instantly — on
the pitch, on a scoreboard, on a jersey.

## The system

- **Greyscale only.** Black and white, per [`color.md`](color.md). No team color — teams are told
  apart by *pattern and graphic*, not hue.
- **Worn on the robot.** A kit is the upper-body jersey. Below it, the robot stays its matte-black
  mechanical self (see [`robot-character.md`](robot-character.md)) — kit on top, machine legs below.
- **League cuts.** V-neck or crew, often with ringer collar/cuff trim. Athletic, modern, clean.
- **Shape-language family.** Patterns draw on the brand's [`identity.md`](identity.md) vocabulary —
  chevrons, bars/stripes, halftone gradients, distortion — rendered in black and white.

## The 8 kits

Asset ids resolve via [`assets/manifest.json`](../../assets/manifest.json). Each kit has a flat
(`kit-0N`) and an on-robot 360 (`kit-0N-360`).

| # | Kit id | Identity |
| --- | --- | --- |
| 1 | `kit-01` | White; black chevrons + barcode-stripe blocks. |
| 2 | `kit-02` | Black; all-over white liquid/marble distortion. |
| 3 | `kit-03` | Black; chrome/metallic petal-burst around the collar and shoulders. |
| 4 | `kit-04` | White; thin black pinstripes with black ringer trim. |
| 5 | `kit-05` | White; a horizontal halftone gradient band across the chest. |
| 6 | `kit-06` | Greyscale; halftone orb motif over a vertical stripe fade. |
| 7 | `kit-07` | Black/grey; bold diagonal stripes, collared polo cut. |
| 8 | `kit-08` | Black; white vertical pinstripes with white ringer trim. |

## Notes

- **Team names are not yet assigned.** Names are generated with
  [`name-forge`](../../skills/name-forge/SKILL.md); pair each name to a kit as teams are finalized.
- When generating or reviewing kitted imagery, keep the robot **on-model** (camera-bar head, matte
  black, mechanical legs) and the kit **greyscale** — a team is its graphic, never a color.
