---
title: Color
type: visual-color
status: active
updated: 2026-06-06
source: brand owner direction — "the palette is greyscale; all images are black and white"
---

# Color

**The Neo Premier League palette is greyscale.** Black, white, and the greys between. No hue,
ever. Drama comes from **contrast**, not color.

> Brand owner confirmed: greyscale / black-and-white only. The named ramp steps below are a
> proposed working scale grounded in the assets — **confirm or adjust the intermediate hex values
> as needed.** The two anchors (true black, true white) and the "no color" rule are fixed.

## The ramp

| Token | Hex | Role |
| --- | --- | --- |
| `ink` | `#000000` | True black. Primary — the machine, type on light, deep grounds. *(fixed)* |
| `carbon` | `#1A1A1A` | Near-black. Matte surfaces, panels, soft black grounds. *(confirm)* |
| `graphite` | `#3D3D3D` | Dark grey. Shadow detail, secondary type on light. *(confirm)* |
| `steel` | `#8A8A8A` | Mid grey. The neutral seamless backdrop tone. *(confirm)* |
| `ash` | `#C8C8C8` | Light grey. Dividers, muted UI/telemetry, fades. *(confirm)* |
| `paper` | `#FFFFFF` | True white. Light grounds, the kit base, type on dark. *(fixed)* |

## Rules

- **No color.** Not as accent, not as highlight, not "just one pop." Greyscale is the identity.
- **Max contrast is the default.** Pair `ink` and `paper`. Reserve mid-greys for backdrops,
  depth, and the quieter telemetry layer.
- **Matte, not glossy.** Blacks should read as deep matte (see [`treatment.md`](treatment.md)),
  not reflective.
- **Backgrounds** are typically `paper` (poster/editorial), `steel` (studio/seamless), or `ink`
  (cinematic) — never busy.

## Accessibility note

`ink` on `paper` (and the reverse) clears WCAG AAA. For body text, stay on `ink`/`graphite` over
`paper`, or `paper`/`ash` over `ink`. Avoid mid-grey-on-mid-grey for anything that must be read.
