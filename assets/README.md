# assets/ — the media library pointer

**No media is stored in this repo.** All Neo Premier League images and video live in a single
**public media library** on Dropbox, so the repo stays lean and never balloons as generated images
and video accumulate.

## Get the media

➡️ **Public media library:**
<https://www.dropbox.com/scl/fo/vj5i6qmw8o88kjkiqpmnk/AA95hhKryhzA89U27g142b0?rlkey=ys426o4603970s2m6nqm7lyne&st=snhoww7a&dl=0>

Students and brand users grab any image or video from there. When running an image skill in a web
chatbot, download what you need and **attach** it.

## How assets are referenced

The repo holds only [`manifest.json`](manifest.json) — a machine-readable index of the approved
assets. Brand files and skills refer to assets by their **`id`** (e.g. `robot-solo`, `forge-union`),
exactly the way skills refer to brand files by filename. The id resolves to the manifest entry; the
actual file lives in the media library above.

This is the same principle the whole repo uses: **reference by name, keep the thing in one place.**

| id | category | what it is |
| --- | --- | --- |
| `robot-solo` | robot | Canonical character — the robot on its own, clean front view. |
| `robot-360` | robot | The robot in 360 (five angles) — the definitive character reference. |
| `black-circuits` … `the-latents` | kit | The **8 team kits** (flat). One per team; all greyscale, each a distinct graphic. |
| `<team>-360` | kit | Each team kit shown **on the robot**, in 360 (e.g. `forge-union-360`). |
| `robot-explore-a`, `robot-explore-b` | exploration | 3×3 model exploration grids (reference only). |
| `key-art-hero` | style | Hooded portrait with heavy glitch tear — hero treatment. |
| `key-art-header` | style | Two robots contesting a header, glitch + telemetry. |
| `key-art-poster` | style | Finished "NEO_STYLE" poster — overlay/type + HUD system. |

The league has **8 teams**, one per kit — see [`brand/visual/kits.md`](../brand/visual/kits.md).

> Binaries are git-ignored (see the repo `.gitignore`). Add new media to the library and a row to
> `manifest.json`; don't commit image or video files.
