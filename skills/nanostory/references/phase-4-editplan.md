# Phase 4 — Edit plan

**Goal:** Turn `script.md` into an editor-ready plan: the timeline order of every
shot, transitions, pacing, and a **coverage report** marking how well each
scripted moment matches the footage that exists. This is the last line of defense
before the editor opens the timeline.

## Timeline order

List every shot in `script.md` in final edit order. Each row names:

- the script row it comes from,
- the asset id and its in–out range,
- an **in/out cue** for the edit (where to trim, in seconds),
- the **transition** into this shot (cut, crossfade, match cut, etc.) and a note
  on why, and
- a pacing note (shot length, rhythm) derived from the Phase 0 mood.

Order follows the script's story arc — Climax shots peak mid-timeline, and the
final shot is the outro the conclusion lands on.

## Coverage report

For every scripted moment, judge how well the assigned asset actually delivers it.
Three levels:

| Level | Meaning |
|---|---|
| `good` | The asset clearly shows what the narration says. |
| `weak` | The asset is related but does not fully show it (narration overreaches). |
| `filler` | The asset covers the beat atmospherically but does not match its specifics. |

One row per script moment, with the level. `weak` and `filler` rows are the
footage-first truth the user must see — do not soften them.

## Gap report

After the coverage report, run the checks:

1. **Every visual row references a real asset** from `catalog.md`.
2. **Mood** — pacing and word choice match the Phase 0 mood.
3. **Angle** — the timeline argues the Phase 0 angle.
4. **Keyword** — the Phase 0 keyword appears where natural.
5. **Target duration** — the runtime line is within the target (off by >~10% with
   no explanation is a gap).
6. **Audience** — narration matches what the Phase 0 audience already knows.
7. **A/V completeness** — every row has both a visual cell and a word-for-word
   audio cell.
8. **Story structure** — the script delivers the Phase 0 `story_structure` arc.
9. **Foreshadowing payoff** (only if `on`) — the clue has a payoff row that
   references it.
10. **Universal value** — the conclusion pairs the chosen value with a concrete
    detail.

Report: **no gaps** or a numbered list, one gap per line, each naming the
preference it violates and the row in `script.md` where it shows. Do not silently
fix gaps — report them. The user decides whether to accept them, reword the
narration, or plan added footage.

## Assumption check

Check every `[ASSUMES:]` marker recorded in `meta/context.md` against the final
plan. Report each one that influenced the output — either as confirmed (the plan
honors it and the user accepted it) or as a gap (the assumption shaped a choice
the user never signed off on). See the `nanocrt` `references/asking.md`.

## Finalize

- Write `decisions.md` recording every confirmed or overridden choice.
- Set every phase `approved` in `meta/progress.json`.
- Append the final entry to `meta/execution-log.md`.

Do not silently fix gaps you find — report them. The user decides whether to
accept them, reword the narration, or plan added footage. **Ask which one.** Close
with the explicit question:

> Reply APPROVED to accept this edit plan as-is, or name the gap to fix and the
> phase to loop back to (Catalog, Outline, Script, or Edit plan).

## Checkpoint

Print this block, then stop. Do not continue until the user replies `APPROVED`.

```
PHASE 4 COMPLETE - Script is ready to edit.

<project>_story/
  catalog.md         Asset inventory + coverage assessment
  outline.md         Hook, beats, scene list anchored to assets
  script.md          Two-column A/V script referencing real files
  edit-plan.md       Timeline order + coverage report
  decisions.md       Confirmed choices and [ASSUMES:] outcomes
  meta/context.md    Preferences and manifest

Gaps: <count> (or none)

Reply APPROVED to accept, or tell me which gap to fix and I will loop back
to the phase that caused it.
```