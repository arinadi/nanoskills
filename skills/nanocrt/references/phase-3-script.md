# Phase 3 — Script

**Goal:** Expand each outline scene into one or more shots and write the
two-column A/V script — the shootable deliverable.

**Load `references/storytelling.md` before writing.** The Phase 2 structure labels
survive into the narration: the script must deliver the arc the outline promised,
word-for-word.

## The two-column A/V format

Industry standard for explainer/long-form video. Two columns, one row per shot:

| Visual | Audio |
|---|---|
| what the viewer sees | what the viewer hears, word-for-word |

- **Visual (left):** camera angle, on-screen text, graphics, B-roll. Specific and
  actionable: "Close-up of the roaster pouring green beans" — never "show coffee".
- **Audio (right):** complete narration, word-for-word. No ellipses, no
  "ad-lib here", no "something like this". The audio column is the script.

The two columns tell the same story at the same moment. If the narration says
"the price dropped", the visual shows a falling price.

## Storytelling in the narration

Honor the Phase 0 `story_structure` and `universal_value` (tables in
`references/storytelling.md`), and the structure labels in `outline.md`:

- **Climax is the peak, not the middle.** The row(s) labelled Climax (or the
  "Tetapi suatu hari" pivot) carry the highest tension — the most surprising or
  most tense narration in the script. Narration before it builds; narration after
  it releases.
- **Tension escalates, word by word.** In Rising Action / "Setiap hari", each
  problem row is a step up from the previous one. Avoid flat enumeration that
  reads like a list.
- **Conclusion lands a takeaway.** The final narration row states the lesson or
  new status, paired with the universal value and a concrete detail — never a
  generic closer like "and that's why it matters".
- **Foreshadowing is seeded and paid off.** When Phase 0 `foreshadowing` is `on`:
  the early clue row and the payoff row both exist, and the payoff row explicitly
  references the clue so the viewer connects them ("ingat tadi yang ..."). A clue
  without a payoff row is a defect, not an option.
- **Emotion and pace track the mood.** The Phase 0 mood dictates sentence rhythm
  and word choice (punchy and short for energetic; longer and calmer for
  documentary) while the arc stays intact.

## Rules

- Expand each outline scene into one or more shots; a scene that needs many shots
  is fine, but each row is one shot.
- Narration is written in the **language chosen in Phase 0** — not the language of
  this skill, not the language of the source material.
- Every factual statement in the narration traces back to a sourced claim in
  `research.md`. Unverified claims must not become confident narration.
- Honor the Phase 0 mood (pace, word choice) and audience (what they already know).
- **The arc never overrides the facts.** If a tension beat requires an unsourced
  claim to hold, cut the tension and keep the fact — the ethics boundary in
  `references/storytelling.md` outranks the structure.

## Runtime line

Under the title, compute:

```
Estimated runtime: ~N min Ns (total audio words ÷ 150 wpm + transitions)
```

Count the audio-column words, divide by 150 (standard narration pace), add a few
seconds per scene for transitions. This is a computed field, not a UI feature.

## Write

Write `script.md` using `templates/script.md`, then update `meta/progress.json`
and append to `meta/execution-log.md`.

## Checkpoint

Phase 3 output must be reviewed and approved by the user before Phase 4 begins.
