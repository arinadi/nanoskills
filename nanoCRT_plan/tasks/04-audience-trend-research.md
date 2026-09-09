# 04 - Phase 1 audience/trend/keyword research

## Behavior

> "nanoCRT writes audience, trend, and keyword findings to `research.md` when topic facts are approved."

**Atomic:** one behavior — the audience/trend/keyword half of research.
**Doable:** the section, sources, and how it feeds the outline are specified.

## Depends on

03

## Requirements

- The audience/trend/keyword section of `research.md` is specified and populated by
  the research phase (same `references/phase-1-research.md`, second half).
- Research covers: who the audience is for this topic, what is trending in the
  niche, and which keywords/phrases the audience actually searches — this grounds
  the idea and angle (PRD §4, core feature 2).
- Same source-per-claim and capability-check rules as task 03 apply.
- The section ends with a short "angle implication" note: what this research means
  for the video's angle, so Phase 2 (outline) can act on it directly.
- Phase 1's checkpoint is not reached until *both* sections (03 + 04) are complete.

## Data and API

Entities: `research.md` (audience/trend/keyword section + angle implication).

Feeds `outline.md` (task 05) via the angle-implication note.

## Technical notes

- This is the "audience/trends" half of the user's Q7 answer ("both"). It is split
  from topic facts (03) because each is independently verifiable: topic facts are
  verifiable as sourced claims; audience/trend is verifiable as the angle note that
  Phase 2 consumes.
- vidIQ/TubeBuddy do this well — but only this half. The differentiator is that
  nanoCRT chains it into a script; do not let this phase balloon into a full SEO
  suite (deferred).

## Acceptance checks

- [ ] Research template has an audience/trend/keyword section
      Command: `grep -qiE 'audience|trend|keyword' skills/nanocrt/templates/research.md`
- [ ] Research reference requires an "angle implication" note feeding the outline
      Command: `grep -qiE 'angle' skills/nanocrt/references/phase-1-research.md`
- [ ] Reference states Phase 1 completes only when both research halves are done
      Command: `grep -qiE 'topic|facts' skills/nanocrt/references/phase-1-research.md && grep -qiE 'audience|trend' skills/nanocrt/references/phase-1-research.md`

## Out of scope for this nanotask

- Topic/fact research — task 03.
- Outline — task 05.
- SEO title/description/tag generation — deferred (`meta/context.md`).
