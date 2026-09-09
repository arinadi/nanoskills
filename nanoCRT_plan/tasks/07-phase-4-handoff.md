# 07 - Phase 4 handoff

## Behavior

> "nanoCRT checks the script against the user's preferences and reports gaps when the script is approved."

**Atomic:** one behavior — the final self-check and gap report.
**Doable:** the check list and report shape are specified.

## Depends on

06

## Requirements

- `skills/nanocrt/references/phase-4-handoff.md` instructs the agent to verify the
  finished `script.md` against every Phase 0 preference: mood, angle, keyword,
  language, target duration, audience.
- Checks include: language matches, mood/angle are honored, keyword coverage is
  present, runtime is within the target duration, and every A/V row has both
  columns populated (risk chain from `architecture.md` §5).
- Any unsourced claim from `research.md` that survived into the script is flagged
  (risk chain: research quality).
- Output is a gap report (list of mismatches) — either "no gaps" or a specific,
  numbered list. This is the final stop of the workflow.
- The phase updates `meta/progress.json` and `meta/execution-log.md` to complete.

## Data and API

Entities: `meta/progress.json` (finalize), `meta/execution-log.md` (final entry).

Reads `script.md` (task 06) and `meta/context.md` (task 02). Writes the gap report.

## Technical notes

- This is the "≤5 edits" success criterion's last line of defense (PRD §8): the
  self-check catches gaps before the user finds them mid-shoot.
- The gap report is not a new document file — it is the phase's chat output plus a
  short block appended to `execution-log.md`. No new entity.

## Acceptance checks

- [ ] Handoff reference lists a check against each Phase 0 preference
      Command: `grep -qiE 'mood|angle|keyword|language|duration|audience' skills/nanocrt/references/phase-4-handoff.md`
- [ ] Handoff reference requires flagging unsourced claims
      Command: `grep -qiE 'unsourced|unverified' skills/nanocrt/references/phase-4-handoff.md`
- [ ] Handoff reference specifies the two-column completeness check
      Command: `grep -qiE 'column|visual|audio' skills/nanocrt/references/phase-4-handoff.md`
- [ ] Handoff reference marks it as the final stop
      Command: `grep -qiE 'final|complete|done' skills/nanocrt/references/phase-4-handoff.md`

## Out of scope for this nanotask

- Nothing. This is the final task; every deferred feature stays in
  `meta/context.md` / `progress.json`.
