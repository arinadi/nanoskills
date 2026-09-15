# nanoskills

A bundle of **nano skills** — disk-first, five-phase, approval-gated workflows
that turn an idea (or a folder of footage) into a structured deliverable. Three
skills, one format:

| Skill | Direction | Input | Output |
|---|---|---|---|
| **nanocrt** | idea-first | a video content idea | `script.md` (two-column A/V, word-for-word narration + shot list) |
| **nanostory** | footage-first | a folder of travel footage/photos | `script.md` (A/V referencing real files) + `edit-plan.md` |
| **nanoprd** | idea-first (code) | a product idea | `PRD.md`, `architecture.md`, `tasks/` (nanotasks) + `AGENT.md` handoff |

All three model the same discipline: capture preferences before doing work,
write every deliverable to disk, stop at a hard approval gate between phases, and
never invent facts. They work in Claude Code, OpenCode, and claude.ai.

---

## The shared shape

```
Phase 0  Intake & preferences  -> meta/context.md   (preferences sharpened before any work)
Phase 1  Research / catalog    -> research.md | catalog.md
Phase 2  Outline               -> outline.md        (hook, beats, ordered scenes)
Phase 3  Script / plan         -> script.md | PRD.md + architecture.md
Phase 4  Handoff & verify      -> gap report against preferences
```

- **nanocrt** — content research: video idea → shootable script.
  `research.md` (topic facts + audience/trend/keyword), `outline.md`,
  `script.md`.
- **nanostory** — footage-first sibling. The footage you already have decides
  what story can be told. `catalog.md` (asset inventory via ffprobe + manifest),
  `outline.md` (scenes anchored to real assets + footage gaps), `script.md`,
  `edit-plan.md` (timeline order + coverage report).
- **nanoprd** — product planning: idea → nanotasks. `PRD.md`, `architecture.md`,
  `design.md`, `tasks/` (atomic, dependency-ordered), `AGENT.md` + `VERIFY.md`
  for the implementing agent.

nanocrt and nanostory share `references/storytelling.md` so every video script
follows a Five-Part or On-a-Day arc, with optional foreshadowing and universal
value. nanostory reuses that file via a relative path and therefore must be
installed alongside nanocrt.

---

## What it produces

Working folders keep the skills' outputs apart: `<project>_crt/`,
`<project>_story/`, `<project>_plan/` (nanoprd owns `_plan`).

```text
<project>_crt/
├── research.md         Phase 1: topic facts + audience/trend/keyword, all sourced
├── outline.md          Phase 2: hook, beats, ordered scene list
├── script.md           Phase 3: two-column A/V script with runtime estimate
└── meta/               context.md, progress.json, execution-log.md

<project>_story/
├── catalog.md          Phase 1: asset inventory + content/quality assessment
├── outline.md          Phase 2: hook, beats, scenes anchored to real assets + gaps
├── script.md           Phase 3: two-column A/V script referencing [asset-id @ timecode]
├── edit-plan.md        Phase 4: timeline order, transitions, coverage report
└── meta/               context.md, progress.json, execution-log.md

<project>_plan/
├── PRD.md              Problem, user, differentiation, features, success criteria
├── architecture.md     Stack, data model, components, dependency graph
├── design.md           Design system                          (UI modes only)
├── tasks/              Nanotasks, dependency-ordered, NN or NN.M
├── AGENT.md            Directive for the implementing coding agent
├── VERIFY.md           Acceptance contract — the agent does not edit this
└── meta/               context.md, decisions.md, progress.json, execution-log.md
```

---

## Install

### Fastest: hand this to your agent

Already have an agent session open? Paste this and it will work out the right path
for whichever tool it's running in:

```text
Install the nanoskills bundle from https://github.com/arinadi/nanoskills

Important: the repo root is NOT a skill. The skills live at skills/nanocrt/,
skills/nanostory/, and skills/nanoprd/. Cloning the repo directly into a skills
directory installs broken skills.

1. Work out which agent you are. Check for ~/.claude, ~/.config/opencode,
   .cursor, .codex, .windsurf, or .gemini.

2. If you are Claude Code, use the plugin marketplace:
       claude plugin marketplace add arinadi/nanoskills
       claude plugin install nanoskills@nanoskills
   Then skip to step 4.

3. Otherwise, clone once and install the skill directories only:
       git clone --depth 1 https://github.com/arinadi/nanoskills.git ~/src/nanoskills
   Link ~/src/nanoskills/skills/* into your agent's skills directory. The repo
   ships install.sh which does this for ~/.claude/skills (all skills in one run).

4. Verify: <skills dir>/nanocrt/SKILL.md, nanostory/SKILL.md, and
   nanoprd/SKILL.md must exist, and each frontmatter `name:` must match its
   folder. nanostory needs nanocrt installed alongside it (it reuses the
   storytelling reference).

Report which path you took and where it landed. Do not touch my other skills.
```

### OpenCode — one command, works on V1 and V2

```bash
git clone https://github.com/arinadi/nanoskills.git ~/src/nanoskills
cd ~/src/nanoskills && ./install.sh
```

`install.sh` symlinks every `skills/*/` into `~/.claude/skills`, which both Claude
Code and OpenCode read. On Windows without Developer Mode it copies instead —
re-run after updates.

### OpenCode V2 — via config instead of symlinks

```bash
git clone https://github.com/arinadi/nanoskills.git ~/src/nanoskills
```

Then add to `~/.config/opencode/opencode.json`:

```jsonc
{ "skills": ["~/src/nanoskills/skills"] }
```

See `opencode.json.example` for the permission syntax (V1 vs V2).

### claude.ai and Cowork

Zip each skill folder (`skills/nanocrt/`, `skills/nanostory/`,
`skills/nanoprd/`) separately and upload in skills settings.

---

## Use it

From inside your project folder:

**nanocrt** (video idea → script):
- "buat script video tentang sejarah kopi indonesia"
- "research konten video untuk topik kebiasaan belajar"
- "naskah video untuk menjelaskan cara kerja blockchain"

**nanostory** (footage → script + edit plan):
- "buat script dari footage liburan di folder raw/"
- "bikin naskah narasi dari video dan foto perjalanan"
- "edit plan dari footage yang sudah ada"

**nanoprd** (product idea → nanotasks):
- "I have an idea for a subscription tracker. Here are my notes in notes.md."
- "Rencanakan proyek untuk aplikasi absensi."
- "help me architect this" / "turn this into tickets"

Each starts at Phase 0 and works down to its final deliverable.

---

## Repository layout

```text
nanoskills/
├── .claude-plugin/
│   ├── marketplace.json
│   └── plugin.json
├── skills/
│   ├── nanocrt/
│   │   ├── SKILL.md
│   │   ├── references/       # one per phase + storytelling
│   │   └── templates/
│   ├── nanostory/
│   │   ├── SKILL.md
│   │   ├── references/       # one per phase
│   │   └── templates/
│   └── nanoprd/
│       ├── SKILL.md
│       ├── references/       # one per phase + state-files
│       └── templates/
├── install.sh                # symlinks every skill into ~/.claude/skills
├── opencode.json.example
├── skill_repo.md             # the rules this repo is built to
└── .github/workflows/validate.yml
```

Each `SKILL.md` uses only the six spec frontmatter fields and no Claude Code-only
body syntax, so the same files work in all three targets.

## License

MIT — see [LICENSE](LICENSE).