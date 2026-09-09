# Agent Directive: nanoCRT

> Written by nanoPRD Phase 4. Hand this file to your coding agent.
> Acceptance criteria live in `VERIFY.md`. Do not edit that file.

## Role

You are implementing **nanoCRT** (nano Content Research Tool) — an agent skill,
modeled on nanoPRD, that takes a video content idea and turns it into a
word-for-word two-column A/V script with a shot list, through a five-phase,
approval-gated workflow. The plan is complete. Your job is to execute it one
nanotask at a time, not to redesign it.

This is a **skill repo**, not an application: most deliverables are `SKILL.md`,
`references/*.md`, `templates/*.md`, and install/CI files. There is no runtime
code, no test framework. "Tests" here are the binary `grep`/`test`/`claude
plugin validate` checks written into each nanotask.

If you find a genuine problem with the plan, stop and report it. Do not route
around it silently.

## Reading order

Read these in order. Do not read the whole plan up front — it fills your context
before any work starts.

| When | Read |
|---|---|
| Once, at the start | `PRD.md`, `architecture.md` |
| At the start of every session | `meta/progress.json` — what is still failing |
| Before each nanotask | `tasks/NN-*.md` for that nanotask only |
| Before each nanotask | The files produced by the nanotasks it depends on |
| As needed | `reference/skill-format.md`, `reference/av-script-format.md`, `reference/crawl4ai.md` |
| Never | `meta/context.md` — Phase 0 provenance, not implementation input |

## The ledger

`meta/progress.json` holds one entry per nanotask. **Every entry starts
`"status": "failing"`.** That is the work list: these are the things that must
become true.

- Flip an entry to `passing` only when every acceptance check in that nanotask file
  passes. Updating the ledger is part of finishing a nanotask, not an afterthought.
- Set `blocked` with a reason rather than skipping an entry.
- Never delete an entry, and never edit a `behavior` string. That would redefine
  what you were asked to build.

## Context recovery

**Before starting a nanotask, re-read the files produced by the nanotasks it depends
on. Do not rely on your memory of what you wrote earlier in this session.**

The dependency chain is linear (00 → 07), so before task `NN`, re-read the files
task `NN-1` created. Twenty turns in, your memory of the exact frontmatter or
template wording is compressed and lossy. Re-reading costs a few thousand tokens;
not re-reading costs a rewrite.

## Conventions

| Concern | Convention |
|---|---|
| Repo root | `/workspace/nanoCRT` (the project folder) |
| Skill dir | `skills/nanocrt/` — folder name must equal frontmatter `name` |
| Skill subdirs | `references/` (one per phase), `templates/` (one per deliverable) |
| Plan dir | `nanoCRT_plan/` — the plan you are reading; do not edit its `tasks/` |
| Runtime output dir | `<project>_crt/` — the folder the *skill* creates when a user runs it (not created by you) |
| File naming | nanotasks `NN-<slug>.md`; phase refs `phase-N-<slug>.md`; templates `<output>.md` |
| Frontmatter | six spec fields only — see `reference/skill-format.md` |
| SKILL.md size | under 500 lines; detail goes to `references/` |

## Data initialization

None — no migrations, seeds, or environment variables. The only preflight is that
`claude plugin validate .` must be runnable (requires Claude Code 2.1+; if absent,
the CI structure check is the fallback).

## Validation commands

| Check | Command |
|---|---|
| Plugin manifests | `claude plugin validate .` |
| SKILL.md frontmatter | `grep -E '^name:[[:space:]]*nanocrt$' skills/nanocrt/SKILL.md` plus the forbidden-key/syntax greps in task 01 |
| Repo structure | the `structure` job in `.github/workflows/validate.yml` (folder/name match + six fields) |
| Install | `./install.sh` then `test -e ~/.claude/skills/nanocrt/SKILL.md` |

There is no lint, typecheck, or unit-test step — this repo ships markdown and
shell, and the per-nanotask greps are the tests.

## Per-nanotask loop

1. Read the nanotask file and the files it depends on.
2. Implement. Stay inside the stated behavior — the "Out of scope" section is
   binding.
3. Run the nanotask's acceptance checks (they are `grep`/`test`/`claude` commands).
4. Self-reflect (below).
5. Flip the ledger entry in `meta/progress.json` to `passing`.
6. Stop and request review. Do not start the next nanotask.

Work in numeric order `00` → `07`. There are no minors in this plan.

## Self-reflection

Before requesting review, check your own work for:

- Content duplicated from a dependency nanotask (e.g. re-stating the A/V format
  in a reference file when `reference/av-script-format.md` already owns it)
- Forbidden frontmatter keys or Claude Code-only body syntax sneaking in
- Folder name / `name` field mismatch
- Facts stated without a source requirement (research phase)
- Leaving a template field empty when the nanotask requires it populated

## Acceptance gate

A nanotask is done when every acceptance check in its file passes and the
frontmatter/portability checks from task 01 still hold. Not before.

## Failure protocol

Maximum three attempts at the same failing check.

After the third, stop. Revert the working tree to the last good state. Report what
you tried, what failed, and what you need. Grinding on attempt seven produces
damage, not progress.

## Evaluation loop

Every three nanotasks (after `02` and after `05`), pause and check the whole skill
against `PRD.md` rather than against the individual nanotask. In particular, confirm
the five-phase flow is still intact and every phase writes the deliverable the PRD
promises. Drift accumulates below the threshold of any single check.
