# Phase 2 — Story outline

**Goal:** Turn `catalog.md` into a skeleton the script phase can expand: a hook,
beats, and an ordered scene list where every scene is anchored to assets that
actually exist. This is where the footage-first constraint bites: you build the
arc the footage can carry, not the arc you would ideally write.

**Load the `nanocrt` skill's `references/storytelling.md` before writing.** The
Phase 0 storytelling preferences (story_structure, universal_value,
foreshadowing) are mandatory inputs here.

## Build order

1. **Hook** — the first ~10 seconds. One line that states the viewer's problem or
   the most striking moment the footage actually contains. Not a greeting. When
   foreshadowing is `on`, the hook or an early scene plants the clue/promise.
2. **Beats** — the story steps, in order. Each beat is one move. Derive beats from
   the strongest assets in `catalog.md`, not from an abstract ideal.
3. **Scene list** — map beats to scenes. Each scene gets a one-sentence summary,
   a story-structure label, and an **asset anchor**: the specific asset id(s) the
   scene will draw from.

## Story structure mapping

Label each scene with the part of the chosen structure it plays, using the tables
in the `nanocrt` `references/storytelling.md`:

- `five-part` → Introduction / Rising Action / Climax / Resolution / Conclusion
- `on-a-day` → Dulu / Setiap hari / Tetapi suatu hari / Maka / Sejak saat itu
- `none` → beats stay a plain sequence; no arc labels

Rules:

- **Climax exists and is single.** Exactly one scene is the peak, and it must be
  anchored to an asset that can actually carry it (the trip's most striking
  footage). No plateau, no climax-less structure.
- **Rising Action escalates.** With `five-part`, ≥2 escalating beats. With
  `on-a-day`, the routine beat repeats before the pivot.
- **Universal value is named.** When `universal_value` is set (or inferred), state
  where it surfaces and anchor it to a concrete asset — never a generic claim.
- **Foreshadowing is paid off.** When `on`, the clue is in an early scene and the
  payoff is anchored to a later asset that can deliver it. If the footage cannot
  pay it off, drop foreshadowing and say why.

**Inferred storytelling fields are not final until confirmed.** If the outline
resolves a `story_structure`, `universal_value`, or `foreshadowing` that Phase 0
left `unset`, name it in the Phase 2 checkpoint, state the evidence, and ask the
user to confirm or override before Phase 3. Record the outcome in `decisions.md`.
Follow the `nanocrt` `references/asking.md`.

## Footage gaps are first-class output

The outline must contain a **gap list**: every scene or beat the story wants but
the footage cannot supply. For each gap, name:

- the desired shot (what the beat needs), and
- the honest options: reword the narration to fit available assets, use a
  substitute asset already in the catalog, or plan to add footage/stock.

Never write a scene whose anchor is an asset that does not exist. A gap is a
finding, not a failure — the user decides how to close it.

## Rules

- Scene count is guided by the Phase 0 target duration and the usable footage:
  roughly **4–6 scenes per 60 seconds** of final video, but never more scenes than
  the footage can fill. Fewer, stronger scenes beat padding.
- Every scene traces to an asset id in `catalog.md` or is explicitly listed as a
  gap — no scene floats on an unstated assumption.
- The mood and audience from Phase 0 shape the hook and beat order; the angle is
  the spine.
- If the footage cannot support the Phase 0 angle at all, **stop and flag it** —
  do not invent an angle the assets cannot tell. That is the single most important
  finding this phase can produce.

## Write

Write `outline.md` using `templates/outline.md`.

## Record

Update `meta/progress.json` and append to `meta/execution-log.md`.

## Checkpoint

Print this block, then stop. Do not continue until the user replies `APPROVED`.
If this phase resolved any `unset` storytelling fields, name them here and ask
the user to confirm or override before Phase 3.

```
PHASE 2 COMPLETE - Outline written to <project>_story/outline.md

  Scenes:     <count>
  Hook:       <one line>
  Gaps:       <count> footage gap(s)
  Decided:    <storytelling fields the outline resolved, if any>

Confirm: the outline, its asset anchors, and any inferred storytelling
choices are correct. Reply APPROVED to continue, or tell me what to change.
```