---
name: image-art-director
description: Builds a structured, on-brand image-generation prompt for the Neo Premier League (for Midjourney, DALL·E, Firefly, etc.) from a subject. Use when the user wants to generate an image of the robot/league and needs a prompt — covering subject, character fidelity, style/treatment, greyscale palette, composition, and a negative prompt.
---

# Neo Premier League Image Art Director

Turn a subject into a ready-to-paste image-generation prompt that produces the **underlying image**
(e.g. robots playing soccer): the right character, the greyscale look, the glitch/grit treatment,
and a negative prompt that keeps the model away from off-brand results.

**Scope:** this skill makes the *picture only*. It does **not** add headlines, logos, or laid-out
copy — image generators render type poorly, and that's a design step. To place the headline and the
HUD/telemetry/shape system over an image, use `key-art-composer`.

## Brand inputs

Read these brand files before writing the prompt (by filename — they live in `brand/visual/`; in a
web chatbot, attach them):

- `identity.md` — the look and the shape/overlay language.
- `color.md` — the **greyscale** palette (no color, ever).
- `typography.md` — British Inserat for any in-image headline; mono for telemetry.
- `robot-character.md` — the **character fidelity rules** (the camera-bar head, matte black, etc.).
- `treatment.md` — glitch / HUD / grit finishing.
- `anti-patterns.md` (visual section) — what to push into the **negative prompt**.

**Reference images are attachments, not paths.** This skill builds prompts to paste into a web
image generator. When the user wants to guide the model with reference images (a character ref, a
treatment ref), they **attach** those images in the generator. The output describes what to attach
by role and description — it never emits file paths.

## Inputs from the user

- **Subject** (required) — what to depict (e.g. "the robot doing a bicycle kick in a packed
  stadium", "hooded robot portrait, hero shot").
- **Surface** (optional) — where it will be used (poster / social / thumbnail / key-art); sets
  aspect ratio and composition. If given, also consult the relevant `surfaces/` spec.
- **Tool** (optional) — Midjourney / DALL·E / Firefly / generic. Adjust syntax + params (default:
  a clean natural-language prompt plus Midjourney-style params).
- **Notes** (optional) — mood, action, extra constraints.

## How to direct

1. **Read the visual brand.** Load the inputs above.
2. **Compose the prompt** with these layers, in order:
   - **Subject & action** — the moment, posed like sport.
   - **Character** — restate the on-model essentials from `robot-character.md` (matte-black
     humanoid athlete, **horizontal camera-bar visor head**, exposed mechanical joints) so the
     model renders the right robot.
   - **Style & treatment** — greyscale/black-and-white, matte not glossy, plus glitch/HUD/grit
     from `treatment.md` as the subject warrants.
   - **Composition** — framing for the surface (aspect ratio, negative space, and where type will
     later be placed — leave room for it, but don't render type in the image).
3. **Write the negative prompt** from `anti-patterns.md` + off-model rules: no color, no face/eyes,
   no humanoid/helmet head, no chrome/gloss, no toy/cute proportions, no neon esports look — and
   no rendered text/letters/logos (type is added later by `key-art-composer`).
4. **Tune for the tool** — add the right params (e.g. `--ar`, `--style raw` for Midjourney).
5. **List attachments** — describe any reference images the user should attach (by role +
   description), never as file paths.
6. **Deliver as JSON** in the format below.

## Output format

Return **only a JSON object** in this shape (no prose around it):

```json
{
  "subject": "string — restated subject",
  "surface": "string — surface + aspect ratio, or 'unspecified'",
  "tool": "string — target generator",
  "prompt": "string — the full ready-to-paste prompt, including tool params",
  "negative_prompt": "string — comma-separated things to avoid",
  "attachments": [
    { "role": "character | treatment | pose | other", "description": "what to attach and why" }
  ],
  "breakdown": {
    "subject_action": "string",
    "character": "string",
    "style_treatment": "string",
    "palette": "greyscale only",
    "composition": "string"
  }
}
```

`attachments` describes images the user adds in the generator — by role and description, never as
paths. If the user has no reference images, return `"attachments": []`.

## Example

**User input:** Subject: "the robot scoring a bicycle kick." Surface: social key-art. Tool: Midjourney.

```json
{
  "subject": "The robot scoring a bicycle kick",
  "surface": "social key-art (square, 1:1)",
  "tool": "Midjourney",
  "prompt": "A matte-black humanoid robot athlete mid bicycle-kick, body inverted in the air, striking a soccer ball — lean athletic build, exposed mechanical knee and limb joints, gloved mechanical hands, and a horizontal camera-bar visor for a head (rounded sensor slot with twin lenses, no face). Shot like a sports photograph, dramatic low angle, on a seamless mid-grey backdrop. High-contrast black-and-white, matte surfaces, with horizontal glitch/datamosh streaks trailing the motion and small monospace HUD telemetry marks at the edges. Gritty photocopy texture. --ar 1:1 --style raw",
  "negative_prompt": "color, colour, vibrant, neon, glossy, chrome, reflective, human face, eyes, mouth, helmet head, cute, toy, chibi, bulky mech suit, esports gradient, clean corporate render, text, letters, words, typography, watermark, logo",
  "attachments": [
    { "role": "character", "description": "the matte-black robot archetype — camera-bar visor head, exposed joints — to lock the character" },
    { "role": "treatment", "description": "a high-contrast B&W glitch key-art frame to guide the finish" }
  ],
  "breakdown": {
    "subject_action": "bicycle kick, airborne, striking the ball",
    "character": "matte-black humanoid athlete, camera-bar visor head, exposed joints (on-model)",
    "style_treatment": "high-contrast B&W, glitch streaks, HUD marks, grit",
    "palette": "greyscale only",
    "composition": "1:1, low dramatic angle, room at edges for type/telemetry"
  }
}
```

Always restate the camera-bar head and matte-black, greyscale essentials in `prompt` — they keep
the render on-model. If the subject would pull off-brand (color, a real human face), steer it back.
