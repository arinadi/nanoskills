# Phase 4 — Handoff and verify

**Goal:** Check the finished `script.md` against every Phase 0 preference and
report gaps. This is the last line of defense before the user starts shooting.

## Checks

Run each check against `script.md`, comparing to the preferences recorded in
`meta/context.md`. Every check is binary — pass or gap.

| # | Check | Failure looks like |
|---|---|---|
| 1 | **Language** — the script is written in the Phase 0 language | Any narration row in a different language |
| 2 | **Mood** — pace and word choice match the Phase 0 mood | Narration reads opposite to the stated mood |
| 3 | **Angle** — the script argues the Phase 0 angle | The script wanders off-angle |
| 4 | **Keyword** — the Phase 0 keyword appears where natural, and the content serves it | Keyword never appears; content targets a different search intent |
| 5 | **Target duration** — the runtime line is within the target | Runtime off by more than ~10% with no explanation |
| 6 | **Audience** — explanations match what the Phase 0 audience already knows | Script explains basics the audience knows, or skips basics they do not |
| 7 | **A/V completeness** — every row has both a visual cell and a word-for-word audio cell | A row with an empty or placeholder column |
| 8 | **Story structure** — the script delivers the Phase 0 `story_structure` arc | `five-part`/`on-a-day` chosen but climax missing, flat Rising Action, or no conclusion takeaway |
| 9 | **Foreshadowing payoff** (only if `foreshadowing` = `on`) — the early clue has a payoff row that references it | Clue planted, no payoff row; or payoff exists but never connects to the clue |
| 10 | **Universal value** — the conclusion pairs the chosen `universal_value` with a concrete detail | Conclusion is a generic statement ("and that matters") with no named value or detail |

## Unsourced-claim flag

Scan the narration for factual statements that do not trace to a sourced claim in
`research.md`. If an `[unverified]` claim from research survived into the narration
as a confident statement, flag it — the user must know the script leans on an
unverified fact.

## Report

Produce the gap report as the phase's chat output (not a new document file):

- **No gaps** — state it plainly.
- **Gaps found** — a numbered list, one gap per line, each naming the preference it
  violates and the row in `script.md` where it shows.

The gap report is the final stop. Then finalize state:

- Set every phase `approved` in `meta/progress.json`.
- Append the final entry to `meta/execution-log.md`.

Do not silently fix gaps you find — report them. The user decides whether to
accept them or loop back to the phase that caused them.

## Checkpoint

```
PHASE 4 COMPLETE - Script is ready to shoot.

<project>_crt/
  research.md         Research, all claims sourced
  outline.md          Hook, beats, scene list
  script.md           Two-column A/V script
  meta/context.md     Preferences and reference inventory

Gaps: <count> (or none)
```
