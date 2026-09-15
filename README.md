# nanoskills

## Quick install (hand to your agent)

Paste this into any agent session — it fetches the install guide and follows it:

```text
Read https://raw.githubusercontent.com/arinadi/nanoskills/master/install-by-agent.md and install nanoskills following it.
```

Or fetch it yourself first:

```bash
curl -sL https://raw.githubusercontent.com/arinadi/nanoskills/master/install-by-agent.md
```

---

## The problem

You already know what you want. The hard part is getting it out of your head and
into something a camera, an editor, or a coding agent can act on.

So you type a prompt. You get something plausible. You type it again tomorrow and
get something plausible and *different* — because nothing was decided, and nothing
was written down.

The failure is not the model. It is the missing process:

- **Preferences are never captured**, so the output is generic.
- **Decisions live in chat history**, so the next session re-invents them.
- **There is no stop-and-check**, so you approve work you have not actually read.

## The fix

nanoskills is a set of agent skills that run on one shared discipline:

> Decide first. Write it to disk. Stop until you reply `APPROVED`.

Every phase leaves a file behind. Every fact is written once, in the earliest
document that needs it. Nothing important lives only in a scrollback you will
never find again.

The skills, one shape:

| Skill | Start with | End with |
|---|---|---|
| **nanocrt** | a video content idea | `script.md` — two-column A/V, word-for-word narration + shot list |
| **nanostory** | a folder of travel footage/photos | `script.md` referencing real files + `edit-plan.md` |
| **nanoprd** | a product idea | `PRD.md`, `architecture.md`, `tasks/` (nanotasks) + `AGENT.md` |

They work in Claude Code, OpenCode, and claude.ai.

---

## The shared shape

Every skill walks the same five phases, and stops at a hard gate between each one:

```
Phase 0  Intake & preferences  -> meta/context.md   (preferences sharpened before any work)
Phase 1  Research / catalog    -> research.md | catalog.md
Phase 2  Outline               -> outline.md        (hook, beats, ordered scenes)
Phase 3  Script / plan         -> script.md | PRD.md + architecture.md
Phase 4  Handoff & verify      -> gap report against preferences
```

What changes is the direction of the work:

- **nanocrt** is *idea-first*. You bring a topic; it researches the facts and the
  audience, then writes a script you can shoot. `research.md` (topic facts +
  audience/trend/keyword), `outline.md`, `script.md`.
- **nanostory** is *footage-first*. You bring a folder, and the footage you
  already have decides what story can be told. `catalog.md` (asset inventory via
  ffprobe + your manifest), `outline.md` (scenes anchored to real assets +
  footage gaps), `script.md`, `edit-plan.md` (timeline order + coverage report).
- **nanoprd** is *idea-first for code*. You bring a product idea; it produces
  `PRD.md`, `architecture.md`, `design.md`, and `tasks/` — atomic,
  dependency-ordered nanotasks — plus `AGENT.md` + `VERIFY.md` for the
  implementing agent.

nanocrt and nanostory share `references/storytelling.md`, so every video script
follows a Five-Part or On-a-Day arc, with optional foreshadowing and universal
value. nanostory reuses that file by relative path and must be installed
alongside nanocrt.

---

## What it produces

Each skill writes into its own folder, so several projects can sit side by side
without colliding: `<project>_crt/`, `<project>_story/`, `<project>_plan/`
(nanoprd owns `_plan`).

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
for whichever tool it's running in — the same text lives in
[`install-by-agent.md`](install-by-agent.md):

```text
Read https://raw.githubusercontent.com/arinadi/nanoskills/master/install-by-agent.md and install nanoskills following it.
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

From inside your project folder, just describe what you have:

**nanocrt** — a video idea:
- "script a video about the history of coffee in Indonesia"
- "research video content on study habits"
- "write a video script explaining how blockchain works"

**nanostory** — footage you already shot:
- "script from the trip footage in raw/"
- "write a narration from my travel videos and photos"
- "edit plan from the footage I already have"

**nanoprd** — a product to build:
- "I have an idea for a subscription tracker. Here are my notes in notes.md."
- "plan a project for an attendance app"
- "help me architect this" / "turn this into tickets"

Each one starts at Phase 0 and walks down to its final deliverable. When it stops,
read the file it wrote, then reply `APPROVED` — or send it back with a change.

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

---

## Why it sticks

Plenty of tools can write you a script once. The difference here is where the
work lands: on disk, in your project folder, in files you can read, diff, and
keep. The next session picks up from those files instead of starting over — and
you stay the one who approves each step.

MIT — see [LICENSE](LICENSE).
