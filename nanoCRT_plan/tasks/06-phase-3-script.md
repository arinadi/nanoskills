# 06 - Phase 3 script

## Behavior

> "nanoCRT writes a two-column A/V script to `script.md` when the outline is approved."

**Atomic:** one behavior — the shootable script.
**Doable:** the two-column format, the runtime line, and language handling are
specified.

## Depends on

05

## Requirements

- `skills/nanocrt/references/phase-3-script.md` instructs the agent to expand each
  outline scene into one or more shots, writing word-for-word narration.
- `skills/nanocrt/templates/script.md` defines the two-column A/V layout per
  `reference/av-script-format.md`: visual column (camera, on-screen text, B-roll)
  and audio column (complete narration), one row per shot.
- Narration is complete — no ellipses, no "ad-lib here". Visual directions are
  specific ("Close-up of user clicking Export"), not generic ("show the product").
- Script is written in the language chosen in Phase 0.
- A runtime line is computed: total audio word count ÷ 150 wpm + transitions.
- Phase ends with a checkpoint block and stops for `APPROVED`.

## Data and API

Entities: `script.md` (two-column A/V table + runtime line).

Consumes `outline.md` (task 05). Checked by Phase 4 (task 07).

## Technical notes

- The A/V format is the industry standard (Boords/StudioBinder use it); the exact
  layout is in `reference/av-script-format.md`, not restated here.
- Runtime is a computed field, not a UI feature (scope-challenge outcome, PRD §10).
- Word-for-word narration is the PRD's definition of done — it is what makes the
  script "shootable with ≤5 edits" (PRD §8).

## Acceptance checks

- [ ] Script template defines the two-column visual/audio layout
      Command: `grep -qiE 'visual|audio' skills/nanocrt/templates/script.md`
- [ ] Script reference requires word-for-word narration (no ad-lib)
      Command: `grep -qiE 'word-for-word|ad-lib|ellips' skills/nanocrt/references/phase-3-script.md`
- [ ] Runtime line (÷150 wpm) is specified
      Command: `grep -qE '150' skills/nanocrt/references/phase-3-script.md`
- [ ] Script reference honors Phase 0 language choice
      Command: `grep -qiE 'language' skills/nanocrt/references/phase-3-script.md`

## Out of scope for this nanotask

- Handoff self-check — task 07.
- Storyboard image generation — deferred (`meta/context.md`).
- Runtime as a UI calculator — deferred (`meta/context.md`).
