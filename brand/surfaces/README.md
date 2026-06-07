# brand/surfaces/ — surface specs

A **surface** is a place copy (or art) lives. Each surface has its own spec file defining the
length and register it demands. These are the canonical, reusable definitions — skills like
[`brand-writer`](../../skills/brand-writer/SKILL.md) read the matching file and obey it.

One file per surface. Each file's frontmatter (`surface`, `length`, `register`) is the machine
layer; the prose is the human layer.

| Surface | File | Length |
| --- | --- | --- |
| Tagline / headline | `tagline.md` | ≤ 10 words |
| Billboard / OOH | `billboard.md` | 3–7 words |
| Jersey / kit | `jersey.md` | 1–4 words |
| Broadcast lower-third | `broadcast-lower-third.md` | a phrase |
| Social post | `social.md` | 1–3 sentences |
| Teaser | `teaser.md` | 3–5 sentences |
| Manifesto / announcement | `manifesto.md` | 1–3 paragraphs |
| Press release | `press-release.md` | standard PR shape |

To add a surface, copy an existing file, change the frontmatter, and add a row above.
