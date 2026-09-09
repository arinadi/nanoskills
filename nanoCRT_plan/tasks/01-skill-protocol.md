# 01 - SKILL.md protocol

## Behavior

> "nanoCRT triggers on a content-research request and runs a five-phase workflow."

**Atomic:** one behavior — the skill exists, has correct frontmatter, and defines
the phase protocol.
**Doable:** the six frontmatter fields, the five phases, and the operating rules
are all specified.

## Depends on

00

## Requirements

- `skills/nanocrt/SKILL.md` exists with frontmatter using only the six spec fields
  (`name`, `description`, `license`, `compatibility`, `metadata`, `allowed-tools`).
- `name: nanocrt` matches the folder name `nanocrt`.
- `description` names the concrete user phrases that should trigger it:
  "buat script video", "research konten video", "naskah video", "video script",
  "content research", plus English equivalents.
- Body defines the five phases and the checkpoint/approval-gate pattern, mirroring
  the nanoPRD protocol structure but adapted to content (not software) deliverables.
- Body contains zero Claude Code-only syntax (`!`cmd``, `$ARGUMENTS`,
  `${CLAUDE_SKILL_DIR}`, `${CLAUDE_PLUGIN_ROOT}`) and none of the forbidden
  frontmatter keys listed in `reference/skill-format.md`.
- SKILL.md stays under 500 lines; per-phase detail lives in `references/` (tasks 02–07).
- Base directory note: SKILL.md states relative paths resolve against the skill
  directory (`skills/nanocrt/`).

## Data and API

Phases (defined here, detailed in `references/` later):

| Phase | Name | Output |
|---|---|---|
| 0 | Intake & preferences | `meta/context.md` |
| 1 | Research | `research.md` |
| 2 | Outline | `outline.md` |
| 3 | Script | `script.md` |
| 4 | Handoff & verify | self-check report |

## Technical notes

- Copy nanoPRD's operating rules that transfer cleanly (write-to-disk, checkpoint
  stop, approval gate, keep state current) but rewrite the product-specific ones.
- The trigger description is the load-bearing field: agents under-trigger skills,
  so make it slightly pushy and name real phrases.
- `allowed-tools`: the research phase needs web search + fetch + Bash (for optional
  crawl4ai). List them; leave the field out if uncertain is acceptable, but
  specifying keeps the handoff honest.

## Acceptance checks

- [ ] Frontmatter `name` is `nanocrt` and equals the folder name
      Command: `grep -E '^name:[[:space:]]*nanocrt$' skills/nanocrt/SKILL.md`
- [ ] No forbidden frontmatter keys present
      Command: `grep -nE '^(argument-hint|context|agent|disable-model-invocation|user-invocable|model|effort|paths|hooks|when_to_use|shell|disallowed-tools|background):' skills/nanocrt/SKILL.md; test $? -ne 0`
- [ ] No Claude Code-only body syntax present
      Command: `grep -nE '!\`|\$ARGUMENTS|\$\{CLAUDE_SKILL_DIR\}|\$\{CLAUDE_PLUGIN_ROOT\}' skills/nanocrt/SKILL.md; test $? -ne 0`
- [ ] SKILL.md is under 500 lines
      Command: `test "$(wc -l < skills/nanocrt/SKILL.md)" -lt 500`
- [ ] The five phases are named in the body
      Command: `grep -cE 'Phase [0-4]' skills/nanocrt/SKILL.md` (expect ≥5)

## Out of scope for this nanotask

- Actual content of `references/` files — tasks 02–07.
- Actual content of `templates/` files — tasks 02–07.
- `README.md` install commands — task 00.
