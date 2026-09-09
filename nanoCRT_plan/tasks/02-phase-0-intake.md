# 02 - Phase 0 intake

## Behavior

> "User answers preference questions and nanoCRT writes them to `meta/context.md`."

**Atomic:** one behavior — intake captures preferences and records them.
**Doable:** the mandatory preference fields, the reference file, and the template
are specified.

## Depends on

01

## Requirements

- `skills/nanocrt/references/phase-0-intake.md` instructs the agent to ask the
  preference questions before doing anything else.
- Mandatory preference fields: **topic**, **mood**, **angle**, **keyword**,
  **language** (configurable per run), **target duration**, **audience**.
- The intake also records any reference material the user points at, read and
  summarized one line each (what it contributes, what it settles) — mirroring
  nanoPRD's intake step.
- The intake writes `meta/context.md` to `<project>_crt/meta/context.md`, creating
  `<project>_crt/` if needed. Working folder name is `<project>_crt/` (from
  `architecture.md`).
- `skills/nanocrt/templates/context.md` defines the document skeleton: idea
  verbatim, preference answers verbatim, reference inventory, research findings
  (filled later), phase flow.
- Questions are asked before research — this is the Phase 0 core from the PRD.
- Phase ends with a checkpoint block and stops for `APPROVED`.

## Data and API

Entities (see `architecture.md` §2 for the full model):

| Entity | Written here |
|---|---|
| `meta/context.md` | Yes — intake writes preference answers + idea verbatim |
| `meta/progress.json` | Yes — initialized with phase status |
| `meta/execution-log.md` | Yes — first entry |

Preference fields stored in `context.md`: topic, mood, angle, keyword, language,
duration, audience.

## Technical notes

- This is the whole point of the product (PRD §4, core feature 1): preferences
  captured *before* research make research sharp. Do not fold research into this
  phase.
- Language selection happens here so Phase 3 knows what language to write in.
- `angle` and `keyword` are intake fields that *narrow* research — they are not SEO
  title features (deferred, `meta/context.md`).

## Acceptance checks

- [ ] Reference file exists and lists all seven preference fields
      Command: `grep -cE 'topic|mood|angle|keyword|language|duration|audience' skills/nanocrt/references/phase-0-intake.md` (expect coverage of all 7)
- [ ] Template file exists with a preference-answers section
      Command: `test -f skills/nanocrt/templates/context.md && grep -qi 'preference' skills/nanocrt/templates/context.md`
- [ ] Intake writes to `<project>_crt/meta/` (not `<project>_plan/`)
      Command: `grep -q '_crt' skills/nanocrt/references/phase-0-intake.md`
- [ ] Checkpoint + APPROVED gate is described in the reference file
      Command: `grep -qi 'APPROVED' skills/nanocrt/references/phase-0-intake.md`

## Out of scope for this nanotask

- Research execution — task 03 and 04.
- Outline/script/handoff — tasks 05, 06, 07.
- `templates/` for research/outline/script — those tasks own their templates.
