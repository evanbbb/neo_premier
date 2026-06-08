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

## How to run it (web app — ChatGPT, Gemini, etc.)

This skill is **image-to-image**: it compares the render against approved reference images, not a
text description. In your chat:

1. Paste this `SKILL.md`.
2. **Attach the approved reference images** (the list below).
3. **Attach the image to check** (the candidate render).
4. Send.

**Which image is the candidate — the odd-one-out rule.** You do **not** need to rely on attachment
order. The approved reference images carry their **filename printed on the image as a visible label**
— `robot_model_360.png` and `robot_model_solo.png`. So:

- An attached image **with one of those labels** is a **reference** — read the label to know which one.
- The attached image **without such a label** (a fresh render) is the **candidate**.

Identify the candidate as the image that is **not** one of the labelled references, then read each
reference's label to populate the `references` list. **If you cannot tell which image is the
unlabelled candidate (e.g. none or more than one lack a label), ask before scoring** — never guess.
If no reference images are attached at all, ask for them (this check does not run against a text
description).

## The reference set (attach these)

Pull these from the public **media library** and attach them — each carries its filename as an
on-image label so the skill can read it. Both together are ideal; `robot_model_360.png` alone is a
strong minimum.

| Attach | On-image label | Why |
| --- | --- | --- |
| **360 turnaround** | `robot_model_360.png` | Five angles of the bare robot — the single best reference. |
| **Solo front** | `robot_model_solo.png` | Clean front view of the bare robot. |

These bare-robot references carry the labels, so the unlabelled new render is unambiguously the
candidate. If the candidate wears a team kit, you may also attach that team's kit-on-robot 360 as an
extra reference — but it is **not** labelled, so tell the model it's a reference (otherwise there are
two unlabelled images and the skill will ask which to check).

On-model means consistent with the established character across these references, allowing a
legitimate look change (a different team kit).

## The checks (visual comparison to the approved images)

Compare the robot under test to the approved reference images. Score each PASS or FAIL with a
one-sentence reason:

1. **Head match** — the head matches the approved character's horizontal camera-bar visor (twin
   lenses, ribbed neck, no face). *(load-bearing — the signature)*
2. **Finish match** — same matte-black, greyscale finish as the references (no color, no chrome/gloss).
3. **Proportion match** — same lean, athletic build as the references (not bulky, boxy, or toy).
4. **Articulation match** — same mechanical detailing: exposed joints, gloved hands, sneaker-style feet.
5. **Overall consistency** — reads as the same character as one of the approved versions (a look
   change like a different team kit is fine; a different character is not).

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
  "candidate": "string — the unlabelled candidate image + a one-line description of the robot in it",
  "references": ["string — each reference used, by the label read from its image, e.g. robot_model_360.png"],
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

`candidate` echoes which attachment was judged (so you can catch a mix-up). `references` lists the
reference images used and `references_used` is their count. `score` = count of PASS;
`off_model_flags` and `fixes` are empty when the verdict is `ON_MODEL`.

## Examples

**User input:** *(two labelled reference images — `robot_model_360.png`, `robot_model_solo.png` —
plus one unlabelled render to check: a cute round robot with two big glowing eyes, a smiling face,
chrome finish.)*

```json
{
  "candidate": "The unlabelled render — cute round robot with two glowing eyes, a smiling face, and a chrome finish",
  "references": ["robot_model_360.png", "robot_model_solo.png"],
  "references_used": 2,
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

**User input:** *(two labelled reference images — `robot_model_360.png`, `robot_model_solo.png` —
plus one unlabelled render to check: the matte-black robot in a team kit, camera-bar visor head,
exposed mechanical legs, greyscale.)*

```json
{
  "candidate": "The unlabelled render — matte-black robot in a team kit with the camera-bar visor head and exposed mechanical legs, greyscale",
  "references": ["robot_model_360.png", "robot_model_solo.png"],
  "references_used": 2,
  "verdict": "ON_MODEL",
  "score": 5,
  "max_score": 5,
  "checks": [
    { "id": 1, "name": "head_match", "result": "PASS", "load_bearing": true, "reason": "Camera-bar visor with twin lenses on a ribbed neck, matching the references; no face." },
    { "id": 2, "name": "finish_match", "result": "PASS", "load_bearing": false, "reason": "Matte black, greyscale, no chrome — matches the references." },
    { "id": 3, "name": "proportion_match", "result": "PASS", "load_bearing": false, "reason": "Lean athletic build consistent with the references." },
    { "id": 4, "name": "articulation_match", "result": "PASS", "load_bearing": false, "reason": "Exposed knee/limb joints and mechanical legs match the references." },
    { "id": 5, "name": "overall_consistency", "result": "PASS", "load_bearing": false, "reason": "Matches an approved version (a team-kit look); same character." }
  ],
  "off_model_flags": [],
  "fixes": []
}
```
