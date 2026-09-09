# Reference — Agent Skills format (portable skill repo)

Source of truth for how the nanoCRT skill repo must be structured so it installs in
Claude Code, OpenCode, and claude.ai. Condensed from `skill_repo.md` in the nanoPRD
repo (the pattern source).

## Frontmatter — six fields only

```yaml
---
name: nanocrt
description: <what it does and when to use it>
license: MIT
compatibility: Requires OpenCode v1.0.190+ or Claude Code for native skills.
metadata:
  version: "1.0.0"
  author: <name>
allowed-tools: <optional>
---
```

- `name` must equal the folder name (`skills/nanocrt/`), lowercase, matching
  `^[a-z0-9]+(-[a-z0-9]+)*$`, no leading/trailing hyphen, no `--`, and must not
  contain `anthropic` or `claude`.
- `description` is the trigger. 1–1024 chars. State what AND when, using the
  user's own phrasing ("buat script video", "research konten video", "naskah
  video"). Slightly pushy — agents under-trigger skills.
- `compatibility` max 500 chars.

## Forbidden (spec-portability hard error)

Forbidden frontmatter keys: `argument-hint`, `context`, `agent`,
`disable-model-invocation`, `user-invocable`, `model`, `effort`, `paths`, `hooks`,
`when_to_use`, `shell`, `disallowed-tools`, `background`.

Forbidden body syntax: `` !`cmd` `` (shell injection), `$ARGUMENTS`,
`${CLAUDE_SKILL_DIR}`, `${CLAUDE_PLUGIN_ROOT}`.

Error at claude.ai upload if violated:

```
Unexpected key(s) in SKILL.md frontmatter: argument-hint.
Allowed properties are: allowed-tools, compatibility, description, license, metadata, name
```

## Layout

```
nanoCRT/
├── .claude-plugin/
│   ├── marketplace.json      # catalog, read by /plugin marketplace add
│   └── plugin.json           # plugin manifest
├── skills/
│   └── nanocrt/
│       ├── SKILL.md
│       ├── references/       # loaded on demand, one level deep
│       └── templates/
├── install.sh                # symlinks skills into ~/.claude/skills
├── opencode.json.example
├── .github/workflows/validate.yml
├── LICENSE
└── README.md
```

Non-negotiable:

- SKILL.md under 500 lines; detail goes to `references/`.
- Only three subdirs in a skill: `scripts/`, `references/`, `assets/`. No top-level
  `bin/` (claude.ai rejects it).
- No `../` cross-skill references — the plugin dir is copied to a cache.
- `marketplace.json` must live at `.claude-plugin/` in repo root. Relative plugin
  `source` must start with `./`.

## plugin.json

```json
{
  "name": "nanocrt",
  "description": "Content research to video script",
  "author": { "name": "<author>" },
  "homepage": "https://github.com/<user>/nanoCRT",
  "license": "MIT"
}
```

Omit `version` during active development so it falls back to commit SHA.

## marketplace.json

```json
{
  "$schema": "https://anthropic.com/claude-code/marketplace.schema.json",
  "name": "nanocrt",
  "owner": { "name": "<author>" },
  "description": "nano Content Research Tool",
  "plugins": [
    {
      "name": "nanocrt",
      "source": "./",
      "description": "nano Content Research Tool",
      "category": "content"
    }
  ]
}
```

## Validation

```bash
claude plugin validate .          # marketplace.json + plugin.json
claude plugin validate ./skills   # SKILL.md frontmatter (older CLI)
```

Note: current CLI fails on `validate ./skills` with "No manifest found" — the
`structure` CI job checks folder/name match + six fields + forbidden syntax instead.
