# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repo is

The canonical, machine-readable source of truth for the **Neo Premier League** brand (robot
football as a global sport), plus a set of LLM "skills" that use it. See [`README.md`](README.md)
for the human overview and [`PLAN.md`](PLAN.md) for the build plan + progress checklist.

## The one rule that matters most

**There is a single canonical brand source: [`brand/`](brand/). Never duplicate brand text.**

- All brand facts live once, in `brand/`. One fact per file.
- Skills must **not** copy brand text into themselves and must **not** reference brand files by a
  relative path (e.g. `../../brand/voice.md`). Instead a skill names the files it needs **by
  filename only** (e.g. "read `voice.md` and `lexicon.md`"). This keeps skills portable: in Claude
  Code the agent locates the named files in `brand/`; in a web chatbot the user attaches them.

## File conventions

- Every file in `brand/` starts with light **YAML frontmatter** (`title`, `type`, `status`,
  `updated`, `source`) followed by prose. Tools read the frontmatter; humans read the prose.
- Filenames are lowercase-kebab, no spaces.
- The brand **evolves**: `skills/brand-evolver` edits `brand/` files and appends a dated record to
  `brand/decisions/`. Treat `brand/decisions/` as an append-only audit log — never rewrite history.

## Media lives outside the repo

No images or video are committed. All media lives in a public **media library** (Dropbox), indexed
by [`assets/manifest.json`](assets/manifest.json). Refer to assets by **id** (e.g. `robot-solo`,
`kit-03`); the id resolves via the manifest to the library. Binary files are git-ignored —
never commit images or video. When a skill needs a reference image, download it from the library
(Claude Code) or attach it (web chatbot).

## Working norms

- **Commit after each task** (see `PLAN.md`), not in one batch at the end.
- **Build skills one at a time**, pausing for review before the next.
- **Visuals are user-supplied** — color hex values, fonts, and which hero assets to include come
  from the user. Do not infer them from images; ask, then record the answer.

## Skill anatomy

Each `skills/<name>/SKILL.md` has: frontmatter (`name`, `description`), a `## Brand inputs` section
(files needed, by filename), an input contract, an output format, and worked examples. Use
`skills/brand-writer` (generation) and `skills/copy-reviewer` (governance) as the reference
patterns.
