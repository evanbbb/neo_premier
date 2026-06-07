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

## The 8 teams & kits

Asset ids resolve via [`assets/manifest.json`](../../assets/manifest.json). Each team has a flat
kit (`<team>`) and an on-robot 360 (`<team>-360`).

| Team | Kit id | Identity |
| --- | --- | --- |
| **Black Circuits** | `black-circuits` | White; black chevrons + barcode-stripe blocks. |
| **Rust Saints** | `rust-saints` | Black; all-over white liquid/marble distortion. |
| **Forge Union** | `forge-union` | Black; chrome/metallic petal-burst around the collar and shoulders. |
| **The Assembly Line** | `the-assembly-line` | White; thin black pinstripes with black ringer trim. |
| **Graveyard Shift** | `graveyard-shift` | White; a horizontal halftone gradient band across the chest. |
| **The Stack FC** | `the-stack-fc` | Greyscale; halftone orb motif over a vertical stripe fade. |
| **Null State** | `null-state` | Black/grey; bold diagonal stripes, collared polo cut. |
| **The Latents** | `the-latents` | Black; white vertical pinstripes with white ringer trim. |

## Notes

- Asset filenames are the **team slug** (e.g. `black-circuits.png`, `black-circuits_360.png`) — not
  generic numbers — so the file *is* the team.
- When generating or reviewing kitted imagery, keep the robot **on-model** (camera-bar head, matte
  black, mechanical legs) and the kit **greyscale** — a team is its graphic, never a color.
