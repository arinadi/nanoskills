# Acceptance Contract: nanoCRT

> Written by nanoPRD Phase 4. This file decides whether the work is accepted.
>
> The implementing agent does not edit this file. An agent that can edit its own
> acceptance criteria has no acceptance criteria.

Every entry below is pass or fail. No entry says "review manually" without stating
what the reviewer is looking for and what makes it a failure.

## How to run everything

```bash
# from the repo root /workspace/nanoCRT
claude plugin validate .                                    # manifests
./install.sh && test -e ~/.claude/skills/nanocrt/SKILL.md   # install path
grep -E '^name:[[:space:]]*nanocrt$' skills/nanocrt/SKILL.md # name matches folder
# forbidden frontmatter keys (expect no output)
grep -nE '^(argument-hint|context|agent|disable-model-invocation|user-invocable|model|effort|paths|hooks|when_to_use|shell|disallowed-tools|background):' skills/nanocrt/SKILL.md
# forbidden body syntax (expect no output)
grep -nE '!\`|\$ARGUMENTS|\$\{CLAUDE_SKILL_DIR\}|\$\{CLAUDE_PLUGIN_ROOT\}' skills/nanocrt/SKILL.md
```

## Whole-system checks

Must pass regardless of which nanotask was last touched.

| Check | Command | Pass condition |
|---|---|---|
| Plugin manifests valid | `claude plugin validate .` | exit 0 |
| `name` equals folder | `grep -E '^name:[[:space:]]*nanocrt$' skills/nanocrt/SKILL.md` | one match |
| Forbidden frontmatter keys absent | grep above | no output |
| Forbidden body syntax absent | grep above | no output |
| SKILL.md under 500 lines | `test "$(wc -l < skills/nanocrt/SKILL.md)" -lt 500` | exit 0 |
| All five phases named | `grep -cE 'Phase [0-4]' skills/nanocrt/SKILL.md` | ≥ 5 |
| install.sh executable | `test -x install.sh` | exit 0 |

## Per-nanotask checks

**Not listed here.** Each nanotask's acceptance checks live in its own file under
`tasks/`, written once. Their pass/fail state lives in the ledger at
`meta/progress.json`. Copying them into this file would create a second set that
drifts from the first, and no reviewer could tell which one was current.

To review nanotask state:

```bash
# what is still failing
python3 -c "import json;d=json.load(open('nanoCRT_plan/meta/progress.json'));print([t['id'] for t in d['nanotasks'] if t['status']!='passing'])"
```

The chain is linear with no minors, so `00`–`07` should read `passing` in order.

## Non-functional checks

The measurable requirements from `PRD.md` §7.

| Requirement | Target | Command | Pass condition |
|---|---|---|---|
| Spec-only frontmatter | only the six fields | `claude plugin validate .` + forbidden-key grep | exit 0 / no output |
| Portability (no tool-specific syntax) | zero forbidden body syntax | body-syntax grep above | no output |
| Installs in both tools | symlink resolves to dir with SKILL.md | `./install.sh && test -e ~/.claude/skills/nanocrt/SKILL.md` | exit 0 |
| Self-contained repo | no `../` cross-skill references | `grep -rn '\.\./' skills/` | no output |

## Regression checks

Greenfield — no prior system exists. Nothing to regress. This section is
intentionally empty.

## Sign-off

The project is accepted when every check above passes and the success criterion in
`PRD.md` §8 is met: a shootable script with ≤ 5 manual edits from one idea +
preferences. That criterion is exercised by running the skill on a real idea
(after the repo is installed), not by any static check above.

| | |
|---|---|
| Checks passing | / |
| Success criteria met | |
| Accepted by | |
| Date | |
