# nanoCRT

Turn a video content idea into a **shootable script** — word-for-word narration
and a shot list, in the two-column A/V format — through a five-phase, approval-gated
workflow.

nanoCRT = **nano Content Research Tool**.

It is an Agent Skill, modeled on [nanoPRD](https://github.com/arinadi/nanoPRD):
same disk-first, checkpoint-gated structure, but aimed at content instead of code.
Works in Claude Code, OpenCode, and claude.ai.

---

## The problem it solves

You research a video idea by hand — browsing, fact-checking, guessing what the
audience wants — then write the script however it comes out that day. Hours per
video, no repeatable process, and the script isn't always shootable as written.

nanoCRD fixes this with a fixed five-phase path:

```
Phase 0  Intake & preferences  -> meta/context.md     (topic, mood, angle, keyword, language, duration, audience)
Phase 1  Research              -> research.md          (topic facts + audience/trend/keyword)
Phase 2  Outline               -> outline.md           (hook, beats, ordered scene list)
Phase 3  Script                -> script.md            (two-column A/V, word-for-word narration + shot list)
Phase 4  Handoff & verify      -> gap report against your preferences
```

Preferences are captured *before* research, so the research is sharp — not generic.
The script comes out word-for-word, so you can shoot from it with minimal edits.

---

## What it produces

The working folder is `<project>_crt/` (not `_plan` — nanoPRD owns that suffix):

```text
<project>_crt/
├── research.md         Phase 1: topic facts + audience/trend/keyword, all sourced
├── outline.md          Phase 2: hook, beats, ordered scene list
├── script.md           Phase 3: two-column A/V script with runtime estimate
└── meta/
    ├── context.md         Phase 0 record: idea, preferences, reference inventory
    ├── progress.json      phase state
    └── execution-log.md   sequential narrative
```

---

## Install

### Fastest: hand this to your agent

Already have an agent session open? Paste this and it will work out the right path
for whichever tool it's running in:

```text
Install the nanoCRT skill from https://github.com/arinadi/nanoCRT

Important: the repo root is NOT the skill. The skill lives at skills/nanocrt/.
Cloning the repo directly into a skills directory installs a broken skill.

1. Work out which agent you are. Check for ~/.claude, ~/.config/opencode,
   .cursor, .codex, .windsurf, or .gemini.

2. If you are Claude Code, use the plugin marketplace:
       claude plugin marketplace add arinadi/nanoCRT
       claude plugin install nanocrt@nanocrt
   Then skip to step 4.

3. Otherwise, clone once and install the skill directory only:
       git clone --depth 1 https://github.com/arinadi/nanoCRT.git ~/src/nanoCRT
   Link ~/src/nanoCRT/skills/nanocrt into your agent's skills directory as
   'nanocrt'. The repo ships install.sh which does this for ~/.claude/skills.

4. Verify: <skills dir>/nanocrt/SKILL.md must exist, and its frontmatter `name:`
   must read exactly `nanocrt`.

Report which path you took and where it landed. Do not touch my other skills.
```

### OpenCode — one command, works on V1 and V2

```bash
git clone https://github.com/arinadi/nanoCRT.git ~/src/nanoCRT
cd ~/src/nanoCRT && ./install.sh
```

`install.sh` symlinks into `~/.claude/skills`, which both Claude Code and OpenCode
read. On Windows without Developer Mode it copies instead — re-run after updates.

### OpenCode V2 — via config instead of symlinks

```bash
git clone https://github.com/arinadi/nanoCRT.git ~/src/nanoCRT
```

Then add to `~/.config/opencode/opencode.json`:

```jsonc
{ "skills": ["~/src/nanoCRT/skills"] }
```

See `opencode.json.example` for the permission syntax (V1 vs V2).

### claude.ai and Cowork

Zip `skills/nanocrt/` and upload it in skills settings.

---

## Use it

From inside your project folder:

- "buat script video tentang sejarah kopi indonesia"
- "research konten video untuk topik kebiasaan belajar"
- "naskah video untuk menjelaskan cara kerja blockchain"

nanoCRT starts at Phase 0 and works down to the script.

---

## Repository layout

```text
nanoCRT/
├── .claude-plugin/
│   ├── marketplace.json
│   └── plugin.json
├── skills/
│   └── nanocrt/
│       ├── SKILL.md
│       ├── references/       # loaded on demand, one per phase
│       └── templates/        # document skeletons
├── install.sh
├── opencode.json.example
└── .github/workflows/validate.yml
```

The `SKILL.md` uses only the six spec frontmatter fields and no Claude Code-only
body syntax, so the same files work in all three targets.

## License

MIT — see [LICENSE](LICENSE).
