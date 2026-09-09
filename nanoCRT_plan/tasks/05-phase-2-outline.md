# 05 - Phase 2 outline

## Behavior

> "nanoCRT writes a hook, beats, and ordered scene list to `outline.md` when research is approved."

**Atomic:** one behavior — the script skeleton.
**Doable:** the outline structure is specified.

## Depends on

04

## Requirements

- `skills/nanocrt/references/phase-2-outline.md` instructs the agent to build the
  skeleton from `research.md`, honoring the Phase 0 mood, angle, and audience.
- `skills/nanocrt/templates/outline.md` defines the structure: **hook** (first 10
  seconds), **beats** (the story/argument steps), and an **ordered scene list**
  where each scene has a one-sentence summary.
- Scene count is guided by target duration (from Phase 0) — roughly 4–6 scenes per
  60 seconds of final video (see `reference/av-script-format.md`).
- Each scene covers exactly one idea or step; no scene mixes two beats.
- Phase ends with a checkpoint block and stops for `APPROVED`.

## Data and API

Entities: `outline.md` (hook, beats, ordered scene list).

Consumes `research.md` (task 03/04) and `meta/context.md` (task 02). Feeds
`script.md` (task 06).

## Technical notes

- The outline is the bridge between research and script — it is where the angle
  implication from task 04 becomes a concrete structure. If the angle implication
  is missing, the outline cannot be grounded; flag it rather than inventing one.
- Runtime is *not* computed here; the word-count estimate belongs to the script
  phase (task 06), where narration actually exists.

## Acceptance checks

- [ ] Outline reference requires hook + beats + ordered scene list
      Command: `grep -qiE 'hook' skills/nanocrt/references/phase-2-outline.md && grep -qiE 'beat' skills/nanocrt/references/phase-2-outline.md && grep -qiE 'scene' skills/nanocrt/references/phase-2-outline.md`
- [ ] Outline template has a scene-list section with one-sentence summaries
      Command: `grep -qiE 'scene' skills/nanocrt/templates/outline.md`
- [ ] Reference ties scene count to target duration
      Command: `grep -qiE 'duration|second|minute' skills/nanocrt/references/phase-2-outline.md`

## Out of scope for this nanotask

- Script (two-column A/V) — task 06.
- Handoff self-check — task 07.
- Runtime calculation — task 06 (it belongs to the script where narration exists).
