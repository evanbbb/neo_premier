# brand/ — the canonical brand source

Every brand fact lives here, **once**. One fact per file. Each file opens with YAML frontmatter
(machine layer) above prose (human layer). Skills reference these files **by filename**.

## Core (text)

| File | What it defines |
| --- | --- |
| `foundation.md` | Mission, vision, background, positioning statement. |
| `beliefs.md` | What the brand is convinced of — the deep belief list. |
| `values.md` | Core operating principles. |
| `audience.md` | Who it's for, from hardcore builders to casual spectators. |
| `voice.md` | Voice & tone: principles, do/don't, register per surface. |
| `lexicon.md` | Words we use / words we ban; naming conventions. |
| `messaging.md` | Pillars, key messages, approved taglines, boilerplate. |
| `anti-patterns.md` | What the brand avoids — in words and visuals. |

## Surfaces (`surfaces/`)

One file per surface (tagline, billboard, jersey, social, …), each defining the length and register
copy must obey there. The single source for surface specs — see `surfaces/README.md`.

## Visual (`visual/`)

| File | What it defines |
| --- | --- |
| `identity.md` | Overall visual direction + shape / overlay language. |
| `logo.md` | The primary logo (NPL crest) and its usage. |
| `color.md` | Color palette with hex values. *(user-provided)* |
| `typography.md` | Display + body type system. *(user-provided)* |
| `robot-character.md` | The mascot: description, fidelity rules, asset references. |
| `kits.md` | The 8 team kits and the greyscale kit system. |
| `treatment.md` | Photographic / texture treatment (grit, xerox, glitch). |

## Evolution (`decisions/`)

`decisions/` is an append-only log of how the brand has changed over time. The `brand-evolver`
skill writes a dated entry here whenever it updates a canonical file. See `decisions/README.md`.
