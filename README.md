# Neo Premier League — Brand-as-Code

The **Neo Premier League** is robot football reimagined as a global sport — where engineering,
entertainment, and competition collide.

This repository is the brand's **single source of truth**, structured so that both **humans and
machines (LLMs)** can use it. It is also a teaching artifact: a worked example of how to organize
a brand so its parts are **separated, reusable, and machine-readable**.

## The core idea

A brand book is usually a PDF a human reads once. Here the brand is **code**:

- **One fact per file.** Mission, voice, lexicon, color, etc. each live in their own small file.
- **Machine layer + human layer in the same file.** A short YAML frontmatter block at the top is
  what a tool reads; the prose below is what a person reads. One artifact, two audiences.
- **One canonical source.** All brand truth lives in [`brand/`](brand/). Nothing is duplicated.
- **Skills, not screenshots.** The brand *does* things. [`skills/`](skills/) holds LLM tools that
  generate copy and images, review them for brand fit, and even evolve the brand itself.

## What's here

| Folder | What it holds |
| --- | --- |
| [`brand/`](brand/) | The canonical brand definition — one fact per file (foundation, voice, lexicon, visual system, …). |
| [`assets/`](assets/) | A manifest pointing to the **public media library** (Dropbox) where all images + video live. No binaries are committed. |
| [`skills/`](skills/) | LLM tools that **generate**, **govern/review**, and **transform** the brand. |
| [`examples/`](examples/) | Worked outputs showing the skills used together. |
| [`PLAN.md`](PLAN.md) | The build plan and progress checklist. |
| [`CLAUDE.md`](CLAUDE.md) | Operating instructions for AI agents working in this repo. |

## How to use a skill

Each skill is a folder under `skills/` with a `SKILL.md`. A skill names the brand files it needs
**by filename** (e.g. `voice.md`, `lexicon.md`) — never by a path. That means you can use a skill
two ways:

1. **In Claude Code** — the agent reads the named files straight from `brand/`.
2. **In any web chatbot** — paste the `SKILL.md` and **attach the named brand files**. The skill
   works the same, because it never depends on where the files live.

## The skills at a glance

- **Generate (text):** `brand-writer`, `name-forge`, `voice-rewriter`
- **Strategy (text):** `campaign-strategist`
- **Govern / review (text):** `copy-reviewer`
- **Transform the brand:** `brand-evolver`
- **Generate (image):** `image-art-director`, `key-art-composer`
- **Govern / review (image):** `image-reviewer`, `robot-fidelity-checker`
