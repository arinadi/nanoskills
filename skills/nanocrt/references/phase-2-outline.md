# Phase 2 — Outline

**Goal:** Turn `research.md` into a skeleton the script phase can expand: a hook,
beats, and an ordered scene list. This is the bridge where the angle implication
from research becomes a concrete structure.

**Load `references/storytelling.md` before writing.** The Phase 0 storytelling
preferences (story_structure, universal_value, foreshadowing) are mandatory
inputs here — beats are mapped onto the chosen story arc, not just listed.

## Build order

1. **Hook** — the first ~10 seconds. One line that states the viewer's problem or
   the most surprising fact. Not a greeting. When foreshadowing is `on`, the hook
   or an early scene plants the clue/promise.
2. **Beats** — the story or argument steps, in order. Each beat is one move: one
   claim made, one question raised, one turn. No beat mixes two moves.
3. **Scene list** — map beats to scenes. Each scene gets a one-sentence summary and
   covers exactly one idea or step.

## Story structure mapping

After listing the beats, label each scene with the part of the chosen structure it
plays, using the tables in `references/storytelling.md`:

- `five-part` → Introduction / Rising Action / Climax / Resolution / Conclusion
- `on-a-day` → Dulu / Setiap hari / Tetapi suatu hari / Maka / Sejak saat itu
- `none` → beats stay a plain argument sequence; no arc labels

Rules:

- **Climax exists and is single.** Exactly one scene is the peak (or one
  "Tetapi suatu hari" pivot) — the outline must name it explicitly. No plateau,
  no climax-less structure.
- **Rising Action escalates.** With `five-part`, there are ≥2 escalating problem
  beats, each a step up from the last. With `on-a-day`, the routine beat is
  painful/recurring before the pivot.
- **Universal value is named.** When `universal_value` is set (or inferred), the
  outline states where the value surfaces (typically the Conclusion / "Sejak saat
  itu") and pairs it with a concrete, specific detail — never a generic claim.
- **Foreshadowing is paid off.** When `foreshadowing` is `on`, the clue is in an
  early scene, the payoff is in or after the climax scene, and the payoff scene
  explicitly references the clue. If no clean payoff exists, say so and recommend
  dropping foreshadowing rather than planting a forgotten clue.

## Rules

- Scene count is guided by the Phase 0 target duration: roughly **4–6 scenes per
  60 seconds** of final video. A 10-minute target implies ~40–60 scenes; if that
  feels large, revisit the beats before increasing depth.
- Every scene traces back to a sourced claim in `research.md` or to a stated
  narrative choice — no scene floats on an unstated assumption.
- The mood and audience from Phase 0 shape how the hook is phrased and how the
  beats are ordered; the angle is the spine the beats hang on.
- If the angle implication from `research.md` is missing or weak, **stop and flag
  it** — do not invent an angle in the outline.
- The structure labels must not distort facts into a better arc. If the truth of
  the topic cannot fill a Rising Action or a climax, the outline says so and the
  structure is downgraded to `none` with a note — never fabricate tension to fit
  the arc.

## Runtime is NOT computed here

The word-count runtime estimate belongs to Phase 3, where the narration actually
exists. Scene count is the only duration-driven quantity at this stage.

## Write

Write `outline.md` using `templates/outline.md`.

## Record

Update `meta/progress.json` and append to `meta/execution-log.md`.

## Checkpoint

Print this block, then stop. Do not continue until the user replies `APPROVED`.

```
PHASE 2 COMPLETE - Outline written to <project>_crt/outline.md

  Scenes:   <count>
  Hook:     <one line>
  Structure:<the arc delivered, if not `none`>

Confirm: the outline and its story-structure mapping match what you want.
Reply APPROVED to continue, or tell me which scene or beat to change.
```
