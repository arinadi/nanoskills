# Phase 3 — Script

**Goal:** Expand each outline scene into one or more shots and write the
two-column A/V script — the deliverable, with narration written against the
footage that exists.

**Load the `nanocrt` skill's `references/storytelling.md` before writing.** The
Phase 2 structure labels and anchors survive into the narration: the script must
deliver the arc the outline promised, word-for-word, using real files.

## The two-column A/V format

Two columns, one row per shot:

| Visual | Audio |
|---|---|
| what the viewer sees | what the viewer hears, word-for-word |

- **Visual (left):** the real asset, then the camera/on-screen note. Format:
  `[asset-id @ in–out]` followed by the action — e.g.
  `[A01 @ 0:00–0:06] wide of empty beach at golden hour; on-screen title "Day 1"`.
  For a photo: `[A07] Ken Burns push-in on the market stall`. Never a shot that
  is not in `catalog.md` — an unavailable shot is a gap, written as a gap.
- **Audio (right):** complete narration, word-for-word. No ellipses, no
  "ad-lib here", no "something like this". The audio column is the script.

The two columns tell the same story at the same moment: if the narration says
"the beach was empty", the visual shows the empty beach.

## Storytelling in the narration

Honor the Phase 0 `story_structure` and `universal_value` (tables in the `nanocrt`
`references/storytelling.md`) and the structure labels in `outline.md`:

- **Climax is the peak.** The row(s) labelled Climax (or the "Tetapi suatu hari"
  pivot) carry the highest tension, and they use the trip's strongest footage.
- **Tension escalates, word by word.** In Rising Action / "Setiap hari", each beat
  is a step up from the last. Avoid flat enumeration.
- **Conclusion lands a takeaway.** The final narration states the lesson or new
  status, paired with the universal value and a concrete detail from the trip —
  never a generic closer.
- **Foreshadowing is seeded and paid off.** When `on`: the early clue row and the
  payoff row both exist, and the payoff explicitly references the clue. A clue
  without a payoff is a defect.
- **Emotion and pace track the mood.** Phase 0 mood dictates sentence rhythm and
  word choice while the arc stays intact.

## Runtime line

Under the title, compute:

```
Estimated runtime: ~N min Ns (total audio words ÷ 150 wpm + transitions)
```

Count the audio-column words, divide by 150 (standard narration pace), add a few
seconds per scene for transitions. This is a computed field, not a UI feature.

## Rules

- Expand each outline scene into one or more shots; each row is one shot.
- Narration is written in the **language chosen in Phase 0** — not the language of
  this skill, not the language of the source material.
- Every factual statement in the narration must be supported by what the footage
  shows or by what the user stated in the manifest. Do not narrate an event the
  footage does not contain.
- **The footage is the ground truth.** When narration and footage disagree, reword
  the narration — or write the shot as a gap. Never script a shot that does not
  exist.
- The arc never overrides the assets: if a tension beat needs footage you do not
  have, cut the beat or mark the gap.

## Write

Write `script.md` using `templates/script.md`, in the language chosen in Phase 0.

## Record

Update `meta/progress.json` and append to `meta/execution-log.md`.

## Checkpoint

Print this block, then stop. Do not continue until the user replies `APPROVED`.

```
PHASE 3 COMPLETE - Script written to <project>_story/script.md

  Shots:      <count>
  Runtime:    <estimate>

Confirm: the script reads as you expect in the chosen language, and every
visual row points at a real asset. Reply APPROVED to continue, or tell me
which row to change.
```