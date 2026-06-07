# Neo Premier League — Brand-as-Code

> **This is the source-of-truth plan for the project.** It is intentionally committed to the repo
> so it survives across sessions. Update the checklist below as work proceeds.

## Progress checklist

- [x] **Task 1** — Init repo + persist this plan (`PLAN.md`)
- [x] **Task 2** — Scaffold repo structure (`README.md`, `CLAUDE.md`, dirs)
- [x] **Task 3** — Author the text brand source (`brand/*.md`)
- [x] **Task 4** — Capture visuals from the user + curate hero assets (`brand/visual/*`, `assets/`)
- [x] **Task 5** — `brand-writer` skill
- [x] **Task 6** — `copy-reviewer` skill
- [x] **Task 7** — `name-forge` skill
- [x] **Task 8** — `voice-rewriter` skill
- [x] **Task 9** — `campaign-strategist` skill
- [x] **Task 10** — `brand-evolver` skill
- [ ] **Task 11** — `voice-linter` skill
- [ ] **Task 12** — `image-art-director` skill
- [ ] **Task 13** — `key-art-composer` skill
- [ ] **Task 14** — `variation-generator` skill
- [ ] **Task 15** — `image-reviewer` skill
- [ ] **Task 16** — `robot-fidelity-checker` skill
- [ ] **Task 17** — Capstone example (`examples/season-1-launch/`)
- [ ] **Task 18** — Keep heavy media (images/video) out of the repo (external-media strategy)

**Working rules:** commit after every task • build skills one at a time and pause for review •
visuals (hex, fonts, hero assets) are supplied by the user, never inferred • skills reference
brand files **by filename only** (no relative paths) so they also work as web-chatbot attachments.

---

## Context

The **Neo Premier League** is a robot-football brand. This repo is also a teaching artifact: it
shows a class how to organize a brand so it is **machine-readable and reusable**. The original
working files were scattered — brand text duplicated across files, real assets mixed with
unrelated material, and no formal definitions for color, typography, voice rules, beliefs, or
naming.

The organizing principle the class teaches: **one fact per file**, light YAML frontmatter so
machines can read it + prose so humans can, a **single canonical brand source**, and a clear
split between skills that **generate**, skills that **govern/review**, and a skill that
**transforms the brand itself** — kept flat and teachable.

**Outcome:** (1) a deep, well-organized brand definition as a single shared source, (2) a curated
set of hero assets the user selects, (3) twelve LLM-based "skills" across text and image, and
(4) worked examples — all reusable and designed to teach separation of concerns.

## Decisions

- **Location:** this git repo. A *curated* set of hero assets is copied in; the large raw working
  folder stays put elsewhere as the source archive (not moved/deleted).
- **Plan lives in the repo:** this file (`PLAN.md`) is the durable plan.
- **Brand depth:** author the **full deep set** of net-new on-brand *text* content (beliefs,
  voice do/don'ts, lexicon, naming, messaging, anti-patterns).
- **Visuals are user-supplied, not inferred:** the user **selects/provides** color hex values,
  font choices, and which hero assets to include. The build presents candidates and the user
  decides; `visual/*` files are filled from the user's answers (clearly-marked TODO until then).
- **Iterate skill-by-skill:** skills are built **one at a time**, each as its own step, with a
  review/iteration pass before moving to the next — not batch-generated.
- **Wiring (no relative paths):** **single shared brand source** (`brand/`), but each skill
  declares the brand files it needs **by name** (e.g. "read `voice.md`, `lexicon.md`"), never by a
  relative path. This keeps one canonical source (no duplicated brand text) AND makes every skill
  portable: in Claude Code the agent locates the named files; in a web chatbot the user simply
  **attaches** those named files. Declaring brand dependencies by name is the central teaching point.

## Repo structure

```
neo_premier/
├── README.md                 # what this is + the philosophy (brand-as-code) for the class
├── PLAN.md                   # this file
├── CLAUDE.md                 # how Claude operates here; brand-by-name rule; points to brand/ + skills/
├── brand/                    # ◀ SINGLE SHARED BRAND SOURCE (canonical, reusable)
│   ├── README.md             #   index / map of brand files
│   ├── foundation.md         #   mission, vision, background, positioning statement
│   ├── beliefs.md            #   what the brand is convinced of (deep list)
│   ├── values.md             #   core principles
│   ├── audience.md           #   segments: hardcore builders ↔ casual spectators
│   ├── voice.md              #   voice & tone: principles, do/don't, register per surface
│   ├── lexicon.md            #   words we use / ban; naming conventions
│   ├── messaging.md          #   pillars, key messages, approved taglines, boilerplate
│   ├── anti-patterns.md      #   what the brand avoids (text + visual)
│   ├── visual/
│   │   ├── identity.md       #   overall visual direction + shape/overlay language
│   │   ├── color.md          #   palette w/ hex (USER-PROVIDED)
│   │   ├── typography.md     #   display/body type system (USER-PROVIDED)
│   │   ├── robot-character.md #  the mascot: description, fidelity rules, asset refs
│   │   └── treatment.md      #   grit / xerox / glitch photographic treatment
│   └── decisions/            #   ◀ audit trail: brand-evolver writes dated change records
│       └── README.md         #     (e.g. 2026-06-06-grit-over-nasa.md) — the brand evolves
├── assets/                   # curated HERO assets (USER-SELECTED), not the raw dump
│   ├── README.md             #   what each asset is + its source path
│   ├── robot/                #   selected mascot hero shots
│   ├── style/                #   selected look refs
│   └── reference/            #   refs that inform the brand
├── skills/                   # LLM-based tools — Claude Code SKILL.md format
│   ├── README.md             #   catalog: generation / governance / brand-transform × text/image
│   ├── brand-writer/SKILL.md
│   ├── name-forge/SKILL.md
│   ├── voice-rewriter/SKILL.md
│   ├── campaign-strategist/SKILL.md
│   ├── brand-evolver/SKILL.md
│   ├── copy-reviewer/SKILL.md
│   ├── voice-linter/SKILL.md
│   ├── image-art-director/SKILL.md
│   ├── key-art-composer/SKILL.md
│   ├── variation-generator/SKILL.md
│   ├── image-reviewer/SKILL.md
│   └── robot-fidelity-checker/SKILL.md
└── examples/
    └── season-1-launch/      #   capstone: skills chained writer → art-director → reviewers
```

Every file in `brand/` gets light **YAML frontmatter** (`title`, `type`, `status`, `updated`,
`source`) above prose — the human reads the prose, a machine/skill reads the frontmatter. This is
the core "machine-readable" lesson, kept deliberately simple.

## The twelve skills

Each is a folder with a `SKILL.md` using the same frontmatter format as a Claude Code skill
(`name`, `description`). Each opens with a **`## Brand inputs`** section naming the brand files it
requires **by filename only** — no relative paths — so it works inside Claude Code (agent locates
the files) and in a web chatbot (user attaches the files). Then a defined input contract, an
output format, and worked examples. Categories: **generation**, **strategy**, **governance**,
**brand-transform**, across **text** and **image**.

**Text — generation**
1. **brand-writer** — copy for a named **surface** (tagline / OOH billboard / jersey / social set /
   broadcast lower-third / manifesto / press release). Brand inputs: `voice.md`, `messaging.md`,
   `lexicon.md`, `anti-patterns.md`.
2. **name-forge** — names for teams, robots, tournaments, arenas, signature moves. Brand inputs:
   `lexicon.md`, `voice.md`. Ranked candidates with one-line rationale each.
3. **voice-rewriter** — rewrites flat/off-brand/draft copy in the Neo Premier voice. Brand inputs:
   `voice.md`, `lexicon.md`, `anti-patterns.md`.

**Text — strategy**
4. **campaign-strategist** — marketing **campaign ideas** for an objective + context. Output: 2–4
   concepts each with big idea, hook, target segment, channels, signature activations, success
   signal. Brand inputs: `foundation.md`, `audience.md`, `messaging.md`, `voice.md`, `anti-patterns.md`.

**Text — brand-transform** *(the "brand is not static" skill)*
5. **brand-evolver** — proposes AND writes updates to the canonical brand files, then writes a
   dated record to `brand/decisions/<YYYY-MM-DD>-<slug>.md` (what changed, why, what it
   supersedes). The one skill that mutates the source. In a web chatbot it returns the proposed
   edits + decision record for the user to apply.

**Text — governance**
6. **copy-reviewer** — scores any copy against the brand. Brand inputs: `voice.md`,
   `anti-patterns.md`. Criteria PASS/FAIL → ON / BORDERLINE / OFF brand verdict + fixes.
7. **voice-linter** — fast inline pass flagging banned words, clichés, off-voice phrases. Brand
   inputs: `lexicon.md`, `anti-patterns.md`.

**Image — generation**
8. **image-art-director** — structured image-gen prompt (subject, robot ref, style refs,
   composition, palette, surface, negative prompt). Brand inputs: the `visual/*.md` files.
9. **key-art-composer** — art-direction brief for a surface (poster / social key art / thumbnail):
   layout, focal hierarchy, type placement, shape-language usage, asset callouts. Brand inputs:
   `identity.md`, `typography.md` + hero assets.
10. **variation-generator** — N on-brand prompt variations from one concept. Brand inputs: the
    `visual/*.md` files.

**Image — governance (multimodal)**
11. **image-reviewer** — reads an actual image and scores it against the `visual/*.md` files
    (palette, type, shape language, robot fidelity, anti-patterns) → verdict.
12. **robot-fidelity-checker** — focused multimodal check: is the mascot on-model? Brand inputs:
    `robot-character.md` + the curated robot refs in `assets/robot/`.

## Build sequence (commit after every task)

1. **Init repo + persist plan** → commit "Add project plan".
2. **Scaffold repo** (tree, `README.md`, `CLAUDE.md`) → commit "Scaffold repo structure".
3. **Author `brand/*.md`** (text only) → commit "Add brand text definitions".
4. **Capture visuals from user + assets** → commit "Add visual identity + hero assets".
5–16. **Twelve skills, one at a time** in order: brand-writer, name-forge, voice-rewriter,
   campaign-strategist, brand-evolver, copy-reviewer, voice-linter, image-art-director,
   key-art-composer, variation-generator, image-reviewer, robot-fidelity-checker. Pause for review
   after each → commit "Add `<skill-name>` skill". (brand-writer + copy-reviewer first as the
   reference patterns.)
17. **Capstone example** → commit "Add worked example".
18. **External-media strategy** — keep full-res images and all video **outside** the repo so it
    doesn't balloon. In-repo: a machine-readable **asset manifest** (id, description, dimensions,
    external location) + optional small thumbnails/proxies. Decide mechanism with the user (Git
    LFS vs external store + manifest vs `.gitignore` + manifest), add `.gitignore` rules for binary
    media, reconcile the existing `assets/` hero set, and point image skills + `assets/README.md`
    at the manifest rather than committed binaries → commit "Add external-media asset strategy".

## Verification

- **No duplicated brand text:** a signature line appears in exactly one file under `brand/`.
- **No relative paths in skills:** `grep -rn "\.\./" skills/*/SKILL.md` returns nothing — every
  SKILL.md names its brand inputs by filename, so a skill + its named brand files can be attached
  to a web chatbot and still work. (Nav links in `skills/README.md` are fine.)
- **Generation skill runs:** `brand-writer` with a brief + surface returns surface-shaped copy.
- **Governance runs end-to-end:** `brand-writer` output → `copy-reviewer`; a sample image →
  `image-reviewer`; both produce a verdict in the defined format.
- **Brand-transform safety:** `brand-evolver` edits the right `brand/*` file(s) AND writes a dated
  `brand/decisions/<date>-<slug>.md` record (no silent canon edits).
- **Assets:** every file in `assets/` is non-duplicate and listed in `assets/README.md` with its
  origin; total `assets/` size is small (hero set only).
