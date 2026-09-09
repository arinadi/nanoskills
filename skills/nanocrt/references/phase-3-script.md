# Phase 3 — Script

**Goal:** Expand each outline scene into one or more shots and write the
two-column A/V script — the shootable deliverable.

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

## Rules

- Expand each outline scene into one or more shots; a scene that needs many shots
  is fine, but each row is one shot.
- Narration is written in the **language chosen in Phase 0** — not the language of
  this skill, not the language of the source material.
- Every factual statement in the narration traces back to a sourced claim in
  `research.md`. Unverified claims must not become confident narration.
- Honor the Phase 0 mood (pace, word choice) and audience (what they already know).

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
