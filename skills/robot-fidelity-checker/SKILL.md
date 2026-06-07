---
name: robot-fidelity-checker
description: Checks whether the Neo Premier League robot mascot is rendered on-model in an image by comparing it against a set of approved reference images (image-to-image, not against any text description), returning a JSON verdict (ON_MODEL / BORDERLINE / OFF_MODEL). Use when the user has an image of the robot and wants to confirm the character matches approved versions. Multimodal — the user attaches the image under test plus one or more approved reference images. Narrower than image-reviewer, which judges the whole image.
---

# Neo Premier League Robot Fidelity Checker

A focused multimodal check: is the robot in this image **on-model**? It compares the robot **only
against a set of approved reference images** — visual ground truth. It deliberately does **not** read
the written character spec; fidelity here is **image-to-image**. It judges the character only — not
palette, composition, or treatment (that's `image-reviewer`). Outputs JSON so a deterministic
evaluator can gate on it.

## Reference images (the approved set) — required

The robot has **many approved versions** (different looks: archetype, hoodie, kit, …). This skill is
image-to-image: it needs the approved robot **images** as ground truth and compares the render under
test to them. On-model means consistent with the established character across the approved versions,
allowing for legitimate look changes.

- **Claude Code:** the approved set lives in `assets/robot/` (e.g. `archetype.png`, `hoodie.png`,
  `pose-uniform.png`).
- **Web chatbot:** the user **attaches** the approved reference image(s) alongside the image under
  test. More references = a more reliable check.

If no reference images are supplied, **ask for them** — this check does not run against a text
description.

## Inputs from the user

- **Image** (required) — attached; the render to check.
- **Approved references** (required, one or more) — attached in a web chatbot, or taken from
  `assets/robot/` in Claude Code.

## The checks (visual comparison to the approved images)

Compare the robot under test to the approved reference images. Score each PASS or FAIL with a
one-sentence reason:

1. **Head match** — the head matches the approved character's horizontal camera-bar visor (twin
   lenses, ribbed neck, no face). *(load-bearing — the signature)*
2. **Finish match** — same matte-black, greyscale finish as the references (no color, no chrome/gloss).
3. **Proportion match** — same lean, athletic build as the references (not bulky, boxy, or toy).
4. **Articulation match** — same mechanical detailing: exposed joints, gloved hands, sneaker-style feet.
5. **Overall consistency** — reads as the same character as one of the approved versions (a look
   change like a hoodie or kit is fine; a different character is not).

## Verdict thresholds

- **`ON_MODEL`** — all five PASS.
- **`BORDERLINE`** — exactly one FAIL, and it is **not** check 1 (head).
- **`OFF_MODEL`** — check 1 (head) FAILs, or two or more checks FAIL.

Check 1 is load-bearing: the camera-bar head is the brand's face; getting it wrong is off-model
regardless of the rest.

## Output format

Return **only a JSON object** in this shape (no prose around it):

```json
{
  "image": "string — one-line description of the robot in the image",
  "references_used": 0,
  "verdict": "ON_MODEL | BORDERLINE | OFF_MODEL",
  "score": 0,
  "max_score": 5,
  "checks": [
    { "id": 1, "name": "head_match", "result": "PASS | FAIL", "load_bearing": true, "reason": "string" },
    { "id": 2, "name": "finish_match", "result": "PASS | FAIL", "load_bearing": false, "reason": "string" },
    { "id": 3, "name": "proportion_match", "result": "PASS | FAIL", "load_bearing": false, "reason": "string" },
    { "id": 4, "name": "articulation_match", "result": "PASS | FAIL", "load_bearing": false, "reason": "string" },
    { "id": 5, "name": "overall_consistency", "result": "PASS | FAIL", "load_bearing": false, "reason": "string" }
  ],
  "off_model_flags": ["string — each failed check, named"],
  "fixes": ["string — concrete fix", "..."]
}
```

`references_used` = how many approved reference images the check compared against. `score` = count of
PASS; `off_model_flags` and `fixes` are empty when the verdict is `ON_MODEL`.

## Examples

**User input:** *(under test: a cute round robot with two big glowing eyes and a smiling face, chrome
finish. References: 3 approved images of the matte-black camera-bar robot.)*

```json
{
  "image": "Cute round robot with two glowing eyes, a smiling face, and a chrome finish",
  "references_used": 3,
  "verdict": "OFF_MODEL",
  "score": 0,
  "max_score": 5,
  "checks": [
    { "id": 1, "name": "head_match", "result": "FAIL", "load_bearing": true, "reason": "Has a face with eyes and a mouth; the approved character's head is a horizontal camera-bar visor, no face." },
    { "id": 2, "name": "finish_match", "result": "FAIL", "load_bearing": false, "reason": "Chrome/glossy; the references are matte black, greyscale." },
    { "id": 3, "name": "proportion_match", "result": "FAIL", "load_bearing": false, "reason": "Round and cute, not the references' lean athletic build." },
    { "id": 4, "name": "articulation_match", "result": "FAIL", "load_bearing": false, "reason": "No exposed joints, gloved hands, or sneaker feet like the references." },
    { "id": 5, "name": "overall_consistency", "result": "FAIL", "load_bearing": false, "reason": "Doesn't match any approved version of the character." }
  ],
  "off_model_flags": ["head_match", "finish_match", "proportion_match", "articulation_match", "overall_consistency"],
  "fixes": [
    "Regenerate from an approved reference image as a character anchor (image-art-director, reference attached).",
    "Match the matte-black greyscale finish and the camera-bar visor head; drop the face and chrome."
  ]
}
```

---

**User input:** *(under test: the matte-black robot in a hoodie, camera-bar visor head, exposed
mechanical legs, greyscale. References: 3 approved images including the hoodie look.)*

```json
{
  "image": "Matte-black robot in a hoodie with the camera-bar visor head and exposed mechanical legs, greyscale",
  "references_used": 3,
  "verdict": "ON_MODEL",
  "score": 5,
  "max_score": 5,
  "checks": [
    { "id": 1, "name": "head_match", "result": "PASS", "load_bearing": true, "reason": "Camera-bar visor with twin lenses on a ribbed neck, matching the references; no face." },
    { "id": 2, "name": "finish_match", "result": "PASS", "load_bearing": false, "reason": "Matte black, greyscale, no chrome — matches the references." },
    { "id": 3, "name": "proportion_match", "result": "PASS", "load_bearing": false, "reason": "Lean athletic build consistent with the references." },
    { "id": 4, "name": "articulation_match", "result": "PASS", "load_bearing": false, "reason": "Exposed knee/limb joints and mechanical legs match the references." },
    { "id": 5, "name": "overall_consistency", "result": "PASS", "load_bearing": false, "reason": "Matches an approved version (the hoodie look); same character." }
  ],
  "off_model_flags": [],
  "fixes": []
}
```
