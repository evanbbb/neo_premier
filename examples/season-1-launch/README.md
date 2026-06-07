# Worked example — Season 1 Launch

A capstone showing the Neo Premier League skills used **together**, end to end: one objective runs
through strategy → copy → art direction → image prompt, and every output is checked by a governance
skill before it ships. This is the intended workflow: **generate → review → ship**, all anchored to
the single `brand/` source.

> Outputs below are illustrative — the skills are LLM-driven, so exact wording varies. The point is
> the **chain** and how each step feeds the next.

```
campaign-strategist ─┬▶ brand-writer ─▶ copy-reviewer ───────────────▶ ✅ approved headline ─┐
                     │                                                                        │
                     └▶ image-art-director ─▶ [generate] ─┬▶ image-reviewer ─────────────┐    │
                                                          └▶ robot-fidelity-checker ──────┴▶ ✅ approved image ─┐
                                                                                                                │
                          key-art-composer  ◀── lays the approved headline + system over the approved image ◀──┘
                                  │
                                  ▼
                            finished key-art ─▶ ship
```

The underlying **image is made first**; `key-art-composer` is the **final assembly** step that lays
the approved headline (type) and the HUD/shape system over the approved image.

---

## Step 1 — Strategy (`campaign-strategist`)

**Objective:** "Launch Season 1 — drive awareness and opening-match ticket sales, social-first."

**Output (chosen concept):**

```
CONCEPT 1: Witness History
Big idea:     You can tell people you were there when a new sport was born.
Pillar:       A new sport is being born
Audience:     The Spectators (casual, future-curious)
Hook direction: Frame the opener as a historic first — the night the lab became an arena.
Channels:     Short-form video, a countdown, paid social retargeting.
Signature activations: Daily "build reveal" countdown; livestreamed first walk-out; "first 1,000 fans" founding tier.
Success signal: Opening-match ticket conversions from social.

HANDOFF: Develop "Witness History". Next: brand-writer for copy, key-art-composer + image-art-director for the visual.
```

## Step 2 — Copy (`brand-writer`)

**Input:** Brief = the "Witness History" concept. Surface = `teaser`.

**Output:**

```
SURFACE: teaser — 3–5 sentences, rising rhythm, ends on a challenge
BRIEF: Tease the Season 1 opener as a historic first
PILLAR: A new sport is being born

COPY:
The silence before the roar. The hum before the thunder. From workshops the world never watched, the
builders have unleashed their titans. This is not the start of a season — it is the ignition of a
sport. Be there when history is made.
```

## Step 3 — Govern the copy (`copy-reviewer`)

**Input:** the teaser above. Surface = `teaser`.

**Output:**

```
COPY: "The silence before the roar. ... Be there when history is made."
SURFACE: teaser
VERDICT: ON BRAND

SCORES:
1. Tone & voice match:     PASS — Cinematic, rising, visceral; the voice is unmistakable.
2. Pillar / mission:       PASS — Squarely on "a new sport is being born."
3. Audience resonance:     PASS — Pulls the spectator into a historic moment.
4. Avoids anti-patterns:   PASS — No banned words; "be there when" replaces flat "don't miss."
5. Surface fit & impact:   PASS — Five sentences, builds, ends on a challenge.

SUMMARY: On brand and ready. Pair with the master tagline as a sign-off.
```

✅ Copy approved.

## Step 4 — Underlying image prompt (`image-art-director`)

The picture comes first. Take the concept's hero idea (a hero portrait of the robot) and build the
image-gen prompt. Surface = poster. Tool = Midjourney.

**Output (JSON):**

```json
{
  "subject": "Robot hero portrait for the Season 1 poster",
  "surface": "poster (portrait 2:3)",
  "tool": "Midjourney",
  "prompt": "Head-on hero portrait of a matte-black humanoid robot athlete, a horizontal camera-bar visor for a head (twin lenses, no face), exposed mechanical joints, heroic and still, near-white seamless backdrop. High-contrast black-and-white, matte surfaces, subtle photocopy grit, faint horizontal glitch at one edge. --ar 2:3 --style raw",
  "negative_prompt": "color, neon, glossy, chrome, human face, eyes, helmet head, cute, toy, esports gradient, clean corporate render, text, letters, logo",
  "attachments": [
    { "role": "character", "description": "robot-solo / robot-360 to lock the character" }
  ],
  "breakdown": { "palette": "greyscale only", "composition": "2:3, centered hero, room in lower third for the headline" }
}
```

*(Generate the image in the tool, attaching an approved reference. The picture has **no type** — the
headline is added later in Step 6.)*

## Step 5 — Govern the image (`image-reviewer` + `robot-fidelity-checker`)

Run both on the generated image. Illustrative verdicts:

**`image-reviewer`:**

```json
{ "verdict": "ON_BRAND", "score": 5, "max_score": 5, "summary": "Greyscale, on-model, matte with restrained glitch — poster-ready.", "fixes": [] }
```

**`robot-fidelity-checker`** (against approved reference images):

```json
{ "verdict": "ON_MODEL", "references_used": 3, "score": 5, "max_score": 5, "off_model_flags": [], "fixes": [] }
```

✅ Image approved.

## Step 6 — Compose the finished key-art (`key-art-composer`)

Now lay the type and design system **over the approved image**. Inputs: the approved image (Step 5),
the approved headline (from `brand-writer` at the `tagline` surface → **"WITNESS HISTORY"**), and the
surface = `poster`.

**Output (excerpt):** a JSON layout brief — the robot hero image, headline in the lower third
(British Inserat), telemetry at the margins, a single chevron cluster, greyscale + edge glitch.
(See `key-art-composer` for the full schema.)

```json
{
  "concept": "Witness History — the night the lab became an arena",
  "surface": "poster (A1, portrait 2:3)",
  "layout": { "focal_point": "the approved robot hero image, upper third", "headline_zone": "lower third, full width" },
  "type": { "headline": "WITNESS HISTORY", "placement": "Lower third, British Inserat, uppercase" },
  "attachments": [ { "role": "hero_image", "description": "the approved Step-5 robot image to compose over" } ]
}
```

✅ Finished key-art assembled → ship.

---

## What this demonstrates

- **One source of truth.** Every step reads the same `brand/` files — strategy, copy, and art can't drift.
- **Generate → govern.** Copy and image both pass a reviewer before shipping.
- **Clear handoffs.** Each skill's output is the next skill's input (the strategist even names the handoff).
- **Right tool per job.** `image-art-director` makes the picture; `key-art-composer` adds the type.
