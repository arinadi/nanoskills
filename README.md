# nanoCRT

Turn a video content idea into a **shootable script** — word-for-word narration
and a shot list, in the two-column A/V format — through a five-phase, approval-gated
workflow.

nanoCRT = **nano Content Research Tool**.

The repo also ships **nanostory** — the same discipline, but **footage-first**:
turn a folder of existing travel footage and photos into a word-for-word narrated
script plus an editor-ready timeline plan.

Both are Agent Skills, modeled on [nanoPRD](https://github.com/arinadi/nanoPRD):
same disk-first, checkpoint-gated structure, aimed at content instead of code.
Works in Claude Code, OpenCode, and claude.ai.

| Skill | Direction | Input | Output |
|---|---|---|---|
| **nanocrt** | idea-first | a video idea | script.md (A/V) — shots you will shoot |
| **nanostory** | footage-first | a folder of footage/photos | script.md (A/V referencing real files) + edit-plan.md |

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

## nanostory — footage-first sibling

`nanostory` flips the constraint direction: instead of a script that decides what
to shoot, the footage you already have decides what story can be told.

```
Phase 0  Intake            -> meta/context.md    (footage folder, asset manifest, mood, angle, language, duration, audience)
Phase 1  Catalog           -> catalog.md         (asset inventory: ffprobe metadata + content/quality assessment)
Phase 2  Outline           -> outline.md         (hook, beats, scenes anchored to real assets + footage gaps)
Phase 3  Script            -> script.md          (two-column A/V, visual column references [asset-id @ timecode])
Phase 4  Edit plan         -> edit-plan.md       (timeline order, transitions, coverage report good/weak/filler)
```

Key difference: the agent cannot watch video, so Phase 0 collects a per-file
manifest from the user, and Phase 1 reads technical metadata with ffprobe. Both
skills share `references/storytelling.md` (from nanocrt) so every script follows a
Five-Part or On-a-Day arc, with optional foreshadowing and universal value.

Preferences are captured *before* research, so the research is sharp — not generic.
The script comes out word-for-word, so you can shoot from it with minimal edits.

---

## What it produces

**nanocrt** writes into `<project>_crt/`; **nanostory** writes into
`<project>_story/` (neither uses `_plan` — nanoPRD owns that suffix):

```text
<project>_crt/
├── research.md         Phase 1: topic facts + audience/trend/keyword, all sourced
├── outline.md          Phase 2: hook, beats, ordered scene list
├── script.md           Phase 3: two-column A/V script with runtime estimate
└── meta/
    ├── context.md         Phase 0 record: idea, preferences, reference inventory
    ├── progress.json      phase state
    └── execution-log.md   sequential narrative

<project>_story/
├── catalog.md          Phase 1: asset inventory + content/quality assessment
├── outline.md          Phase 2: hook, beats, scenes anchored to real assets + gaps
├── script.md           Phase 3: two-column A/V script referencing [asset-id @ timecode]
├── edit-plan.md        Phase 4: timeline order, transitions, coverage report
└── meta/
    ├── context.md         Phase 0 record: request, preferences, asset manifest
    ├── progress.json      phase state
    └── execution-log.md   sequential narrative
```

---

## Install

### Fastest: hand this to your agent

Already have an agent session open? Paste this and it will work out the right path
for whichever tool it's running in:

```text
Install the nanoCRT skills from https://github.com/arinadi/nanoCRT

Important: the repo root is NOT a skill. The skills live at skills/nanocrt/ and
skills/nanostory/. Cloning the repo directly into a skills directory installs a
broken skill.

1. Work out which agent you are. Check for ~/.claude, ~/.config/opencode,
   .cursor, .codex, .windsurf, or .gemini.

2. If you are Claude Code, use the plugin marketplace:
       claude plugin marketplace add arinadi/nanoCRT
       claude plugin install nanocrt@nanocrt
   Then skip to step 4.

3. Otherwise, clone once and install the skill directories only:
       git clone --depth 1 https://github.com/arinadi/nanoCRT.git ~/src/nanoCRT
   Link ~/src/nanoCRT/skills/nanocrt and ~/src/nanoCRT/skills/nanostory into
   your agent's skills directory. The repo ships install.sh which does this for
   ~/.claude/skills (both skills in one run).

4. Verify: <skills dir>/nanocrt/SKILL.md and <skills dir>/nanostory/SKILL.md
   must exist, and each frontmatter `name:` must match its folder. nanostory
   needs nanocrt installed alongside it (it reuses the storytelling reference).

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

Zip `skills/nanocrt/` (and, separately, `skills/nanostory/`) and upload each in
skills settings.

---

## Use it

From inside your project folder:

**nanocrt** (idea-first):
- "buat script video tentang sejarah kopi indonesia"
- "research konten video untuk topik kebiasaan belajar"
- "naskah video untuk menjelaskan cara kerja blockchain"

**nanostory** (footage-first):
- "buat script dari footage liburan di folder raw/"
- "bikin naskah narasi dari video dan foto perjalanan"
- "edit plan dari footage yang sudah ada"

Each starts at Phase 0 and works down to its final deliverable.

---

## Repository layout

```text
nanoCRT/
├── .claude-plugin/
│   ├── marketplace.json
│   └── plugin.json
├── skills/
│   ├── nanocrt/
│   │   ├── SKILL.md
│   │   ├── references/       # loaded on demand, one per phase + storytelling
│   │   └── templates/        # document skeletons
│   └── nanostory/
│       ├── SKILL.md
│       ├── references/       # loaded on demand, one per phase
│       └── templates/        # document skeletons
├── install.sh
├── opencode.json.example
└── .github/workflows/validate.yml
```

Each `SKILL.md` uses only the six spec frontmatter fields and no Claude Code-only
body syntax, so the same files work in all three targets.

## License

MIT — see [LICENSE](LICENSE).
