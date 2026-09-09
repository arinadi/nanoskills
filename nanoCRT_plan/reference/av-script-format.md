# Reference — Two-column A/V script format

Source of truth for the `script.md` output format. The A/V (audio-visual) layout is
the industry standard for explainer/corporate/long-form video.

## Layout

Two columns, one row per shot/scene:

| Visual | Audio |
|---|---|
| what the viewer sees | what the viewer hears |

- **Visual (left):** camera angle, on-screen text, graphics, B-roll notes. Written
  in terms the editor can act on: "Close-up of user clicking the Export button",
  not "Show the product".
- **Audio (right):** word-for-word narration/voiceover, dialogue, music cues, sound
  effects. Narration is complete — no ellipses, no "ad-lib here".

Each row is one shot. The two columns tell the same story at the same moment — if
the narration describes a feature, the visual column shows that feature.

## Structure rules

- Break the video into scenes; each scene covers one idea or one step.
- A 60-second explainer = ~4–6 scenes. Longer videos scale accordingly.
- List scenes in order; each carries a one-sentence summary (the skeleton from
  `outline.md`).

## Runtime

Estimated runtime = narration word count ÷ 150 wpm (standard pacing), plus seconds
for pauses/transitions. Compute it as a single line under the title:

```
Estimated runtime: ~N min Ns (total audio words ÷ 150 wpm + transitions)
```

This is a computed field, not a separate UI feature.

## Definition of done

A script is "shootable with ≤5 edits" when every row has a populated visual cell and
a complete word-for-word audio cell, scenes are ordered, and the runtime line is
present and correct.
