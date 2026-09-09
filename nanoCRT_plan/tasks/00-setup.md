# 00 - Repo scaffold

## Behavior

> "The nanoCRT repo installs and validates in Claude Code and OpenCode."

**Atomic:** one behavior — the repo shell exists and is installable.
**Doable:** every file, field, and command is specified below.

## Depends on

none

## Requirements

- Repo root contains `.claude-plugin/marketplace.json`, `.claude-plugin/plugin.json`,
  `install.sh`, `opencode.json.example`, `LICENSE`, `README.md`,
  `.github/workflows/validate.yml`, and an empty `skills/nanocrt/` directory.
- `install.sh` is executable (`chmod +x`) and links every `skills/*/` dir that has a
  `SKILL.md` into `~/.claude/skills` (symlink, fall back to copy).
- `marketplace.json` and `plugin.json` match the shapes in
  `reference/skill-format.md`, with `name`/`source`/`homepage` set to `nanocrt`.
- `README.md` carries the install commands for Claude Code, OpenCode, and claude.ai.

## Data and API

Files created (see `reference/skill-format.md` for exact shapes):

| File | Purpose |
|---|---|
| `.claude-plugin/plugin.json` | Plugin manifest: name `nanocrt`, license MIT |
| `.claude-plugin/marketplace.json` | Catalog; `source: "./"`, category `content` |
| `install.sh` | Symlink skills into `~/.claude/skills` |
| `opencode.json.example` | `skills` + `permissions` for OpenCode V1/V2 |
| `.github/workflows/validate.yml` | CI: plugin validate + structure check |
| `LICENSE` | MIT |
| `README.md` | Install commands for all three targets |
| `skills/nanocrt/` | Empty dir; SKILL.md arrives in task 01 |

## Technical notes

- Omit `version` in `plugin.json` during active development — it falls back to
  commit SHA and updates flow automatically.
- `install.sh` mirrors nanoPRD's: `--copy` flag and `--uninstall` support; skip a
  skill dir that lacks `SKILL.md`.
- The `structure` CI job (not the CLI) validates SKILL.md frontmatter, because
  `claude plugin validate ./skills` fails on current CLI with "No manifest found".

## Acceptance checks

- [ ] `marketplace.json` and `plugin.json` validate
      Command: `claude plugin validate .`
- [ ] `install.sh` links `nanocrt` into the skills dir
      Command: `./install.sh && test -e ~/.claude/skills/nanocrt/SKILL.md` (create a placeholder `SKILL.md` first, or assert the link target resolves to the repo dir)
- [ ] Every skill dir name matches its intended `name` (empty `nanocrt` placeholder)
      Command: `test -d skills/nanocrt`
- [ ] `install.sh` is executable
      Command: `test -x install.sh`

## Out of scope for this nanotask

- `SKILL.md` content — task 01.
- Any phase reference/template files — tasks 02–07.
- Marketplace naming that avoids Anthropic-reserved words is assumed done; no
  renaming map needed (first release).
