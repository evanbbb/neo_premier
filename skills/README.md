# skills/ — LLM tools that use the brand

Each skill is a folder with a `SKILL.md`. A skill never hard-codes brand text; it names the
[`brand/`](../brand/) files it needs **by filename** in a `## Brand inputs` section, so it works
both in Claude Code (agent reads the files) and in a web chatbot (user attaches the files).

## The catalog

| Skill | Category | Medium | What it does |
| --- | --- | --- | --- |
| `brand-writer` | generation | text | Writes copy for a named surface (tagline, billboard, jersey, social, manifesto…). |
| `name-forge` | generation | text | Names for teams, robots, tournaments, arenas, signature moves. |
| `voice-rewriter` | generation | text | Rewrites flat or off-brand copy in the Neo Premier voice. |
| `campaign-strategist` | strategy | text | Generates marketing campaign ideas for an objective. |
| `brand-evolver` | brand-transform | text | Edits the canonical brand and logs the change. |
| `copy-reviewer` | governance | text | Scores any copy for brand fit → verdict + fixes. |
| `image-art-director` | generation | image | Prompt for the **underlying image** (e.g. robots playing) — no type. |
| `key-art-composer` | generation | image | Adds **headline + telemetry + layout** over an image; the finished key-art. |
| `image-reviewer` | governance | image | Scores an actual image against the visual identity. |
| `robot-fidelity-checker` | governance | image | Checks the mascot is rendered on-model. |

## How the categories fit together

- **Generation** makes new work (copy or image prompts).
- **Governance** reviews work against the brand before it ships.
- **Brand-transform** changes the brand source itself, with an audit trail.

Pairing a generator with a reviewer in each medium is the intended workflow: generate → review →
ship. See [`examples/`](../examples/) for a worked end-to-end chain.
