# skills/ — LLM tools that use the brand

Each skill is a folder with a `SKILL.md`, sorted into **category buckets** so the kind of skill is
obvious from where it lives. A skill never hard-codes brand text; it names the [`brand/`](../brand/)
files it needs **by filename** in a `## Brand inputs` section. To run one in a **web LLM chatbot**,
paste the `SKILL.md` and **attach the named brand files** (plus any reference images from the media
library). Referencing by filename — not by path — is what makes that work.

## The buckets

```
skills/
├── generation/       make new work
│   ├── brand-writer/          copy for a named surface (tagline, billboard, jersey, social…)
│   ├── name-forge/            names for teams, robots, tournaments, arenas, moves
│   ├── voice-rewriter/        rewrite flat/off-brand copy in the Neo Premier voice
│   ├── image-art-director/    prompt for the underlying image (robots playing) — no type
│   └── key-art-composer/      add headline + telemetry + layout over an image (finished key-art)
├── strategy/         plan the work
│   └── campaign-strategist/   marketing campaign ideas for an objective
├── governance/       check work against the brand before it ships
│   ├── copy-reviewer/         score any copy for brand fit → verdict + fixes
│   ├── image-reviewer/        score an image against the visual identity (JSON verdict)
│   └── robot-fidelity-checker/ check the mascot is on-model vs approved references (JSON verdict)
└── brand-transform/  change the brand source itself
    └── brand-evolver/         edit the canonical brand and log the change (audit trail)
```

## How the categories fit together

- **Generation** makes new work (copy or image prompts).
- **Strategy** plans what to make.
- **Governance** reviews work against the brand before it ships.
- **Brand-transform** changes the brand source itself, with an audit trail.

Pairing a generator with a reviewer in each medium is the intended workflow: generate → review →
ship. See [`examples/`](../examples/) for a worked end-to-end chain.
