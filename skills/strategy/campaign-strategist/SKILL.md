---
name: campaign-strategist
description: Generates on-brand marketing campaign ideas for the Neo Premier League given an objective. Use when the user wants campaign concepts, marketing ideas, a go-to-market angle, or ways to promote the league, a season, a match, or a moment — and wants strategic concepts (big idea, audience, channels, activations) rather than finished copy.
---

# Neo Premier League Campaign Strategist

Turn an objective into on-brand campaign concepts. Each concept is a strategy, not finished copy:
a big idea, who it's for, where it runs, and the signature moments that make it land. Hand the
chosen concept to `brand-writer` for copy and `image-art-director` for visuals.

## Brand inputs

Read these brand files before strategizing (by filename — they live in `brand/`; in a web chatbot,
attach them):

- `foundation.md` — mission, vision, positioning (what the league actually is).
- `audience.md` — the segments to target and what each rewards/punishes.
- `messaging.md` — pillars and key messages (anchor every concept to a pillar).
- `voice.md` — so hooks and directions sound on brand.
- `anti-patterns.md` — strategic and tonal traps to avoid.

## Inputs from the user

- **Objective** (required) — the goal (e.g. "drive Season 1 ticket sales", "grow on TikTok",
  "build hype for the championship final", "recruit new builder teams").
- **Context** (optional) — constraints: timeline, budget level, priority channels, target segment,
  region, or what's been tried.
- **Count** (optional) — number of concepts (default 3; keep to 2–4 so each is distinct).

If the objective is vague, ask one sharpening question before generating.

## How to strategize

1. **Read the brand.** Load the inputs above.
2. **Pick the audience.** From `audience.md`, choose the segment(s) the objective should target —
   different concepts can target different segments.
3. **Anchor to a pillar.** Tie each concept to a `messaging.md` pillar; the pillar is the strategic
   spine.
4. **Find the idea.** Build each concept around one sharp insight or tension — not a tactic list.
5. **Make it real.** Give each concept signature activations / hero moments that only this brand
   could do (lean on the spectacle, the builders, the clash).
6. **Make it measurable.** Name a success signal tied to the objective.
7. **Stay on brand.** Concepts must avoid `anti-patterns.md`. Don't write final copy — give hook
   *directions* and hand off.

## Output format

```
OBJECTIVE: [restated]
[For each concept:]

CONCEPT [n]: [Campaign name]
Big idea:     [the one-sentence concept / insight]
Pillar:       [messaging pillar it ladders to]
Audience:     [target segment]
Hook direction: [the angle for copy — not final copy]
Channels:     [where it runs]
Signature activations: [1–3 hero moments only this brand could do]
Success signal: [how you'd know it worked]

HANDOFF: [which concept to develop, and the next skills — brand-writer / image-art-director]
```

## Example

**User input:** Objective: "Drive ticket sales for Season 1's opening match." Context: limited
budget, social-first. Count: 2.

```
OBJECTIVE: Drive ticket sales for the Season 1 opening match (social-first, limited budget)

CONCEPT 1: Witness History
Big idea:     You can tell people you were there when a new sport was born.
Pillar:       A new sport is being born
Audience:     The Spectators (casual, future-curious)
Hook direction: Frame the opener as a historic first — the night the lab became an arena.
Channels:     Short-form video (TikTok/Reels/Shorts), a countdown, paid social retargeting.
Signature activations: A daily "build reveal" counting down to kickoff; a livestreamed first walk-out; a "first 1,000 fans" founding-member ticket tier.
Success signal: Opening-match ticket conversions from social; sell-through of the founding tier.

CONCEPT 2: Pick Your Titan
Big idea:     Choose a team before kickoff and you've got a dog in the fight.
Pillar:       Real stakes, real spectacle
Audience:     The Sport Fans (want a rival to root for)
Hook direction: Make people pick a side; rivalry copy that dares them to commit.
Channels:     An interactive "pick your team" social unit; team-rivalry video; creator partners per team.
Signature activations: Team allegiance filters/badges; a head-to-head hype reel; ticket bundles by team section.
Success signal: Allegiance picks converting to seat-section ticket sales.

HANDOFF: Develop Concept 1 first (broadest reach on a small budget). Next: brand-writer for the
teaser + ticket-CTA copy, image-art-director for the countdown key-art.
```

Be strategic and specific. Every concept must be something only the Neo Premier League could run —
if it would work for any sport or any tech launch, push it further.
