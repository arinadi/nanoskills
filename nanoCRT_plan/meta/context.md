# nanoCRT — Phase 0 context

nanoCRT = **nano Content Research Tool**.

## Initial idea (verbatim)

> "saya mau membuat repo skill baru, gunakan nanoPRD sebagai pondasi. nanoCRT adalah nano content research tool. tujuannya adalah untuk melakukan research ide konten video. outputnya adalah naskah video. mirip naskah film kata perkata, shoot diperlukan dan lain2. research formatnya."

## Reference inventory

| Reference | Contributes | Settles |
|---|---|---|
| `nanoPRD/SKILL.md` | 5-phase protocol, approval gates, checkpoint blocks | Workflow shape nanoCRT mirrors |
| `nanoPRD/skill_repo.md` | Repo layout, 6-field frontmatter, install mechanics | Repo structure, naming, portability rules |
| `nanoPRD/README.md` | Install commands for Claude Code + OpenCode | How nanoCRT ships and is documented |
| `nanoPRD/install.sh` | Symlink/copy install script | Installer template |
| `nanoPRD/opencode.json.example` | OpenCode V1/V2 config | OpenCode registration shape |
| `nanoPRD/templates/*`, `references/*` | Document skeletons + phase references | Template and reference-file pattern |

## Research findings

### Comparable products — research-only family

- **vidIQ** (Daily Ideas, Keyword Research): analyzes channel/niche/trends, surfaces ideas and keywords scored by potential. Strong at *picking* what to make. Stops at ideas — never produces a script.
- **TubeBuddy** (Video Topic Planner, Keyword Explorer, Next Video Ideas): keyword + trend + idea research with scoring. Same gap: output is ideas/keywords, not a shootable script.

### Comparable products — script-only family

- **Boords**: two-column A/V script editor with runtime counting, script→storyboard. Does the script well; is a SaaS app with a login; does no research.
- **StudioBinder**: professional A/V script + shot-list generator. Same pattern — no research, login-walled.
- **Commodo**: AI script + shot-list generator for YouTube storytelling. Produces scripts, but no research phase and no disk-first workflow.
- **Avey**: A/V script editor with brand scanning, scene table. Same gap.

### The gap nanoCRT fills

Nobody chains **research → word-for-word two-column A/V script with shot list** inside a single agent skill that writes deliverables to the user's project folder. Research-only tools stop at ideas; script-only tools skip research and are login-walled SaaS.

### Domain constraint noted

The two-column A/V format is the industry standard for explainer/corporate video: left column = visuals/shots/camera, right column = audio/narration word-for-word, one row per shot. Runtime ≈ word count / 150 wpm (standard narration pacing). This is the format nanoCRT will target.

## Five mandatory questions and answers

1. **Why does this exist?** — Manual research + scripting takes hours per video. Cost of inaction: hours of manual work per video, time the user would rather spend shooting/editing.
2. **Who is the specific user?** — A solo YouTuber making long-form explainer/educational videos (10+ minutes), shooting alone.
3. **What is the one feature that makes this viable?** — (verbatim) "saya mau ada beberapa phase seperti nanoPRD. user ditanya kelengkapan prefrensi sebelum research. topic, mood, angle, keyword dan lain2. reserch konten prefrensi agar hasil reserch tajam." → A phase-gated workflow like nanoPRD: the user is asked for their preferences (topic, mood, angle, keyword, etc.) *before* research, and research is sharpened by those preferences. The single viable capability is the preference-gated research→script pipeline.
4. **Landscape?** — Greenfield. Nothing exists. nanoCRT reuses only nanoPRD's repo *pattern* (layout, frontmatter, install) as a scaffold, not its code.
5. **How do we know it worked?** — A shootable script with ≤ small manual edits: the user hands it one idea + preferences and gets a script they can shoot from with minimal edits.

## Project-specific questions and answers

6. **Video type & script output layout?** — Long-form explainer/educational. Two-column A/V script (visuals/shots + word-for-word narration).
7. **What does research cover?** — Both (a) topic/fact research for accuracy, and (b) audience/trend/keyword research to ground the idea and angle.
8. **Output language?** — Configurable per run (asked during intake).
9. **Deliverable of this run?** — Full nanoPRD plan (PRD → architecture → nanotasks), then a coding agent builds the nanoCRT skill repo from AGENT.md.

## Phase flow (confirmed)

Five phases, approval gate between each, mirroring nanoPRD:

| Phase | Name | Output to disk |
|---|---|---|
| 0 | Intake & preferences | `meta/context.md` |
| 1 | Research | `research.md` |
| 2 | Outline | `outline.md` |
| 3 | Script | `script.md` (two-column A/V) |
| 4 | Handoff & verify | final self-check against preferences |

## Selected project mode

**`cli-tool`** — nanoCRT is an agent skill with no user interface; it writes markdown deliverables to disk. This is the closest of the five modes. Deviation note: nanoCRT is a *skill*, not a binary, so "distribution check" maps to `claude plugin validate` + the SKILL.md frontmatter/structure CI job, and "integration tests" map to a fresh-session trigger test. `design_doc` is false (no UI).

## Constraints

- Budget: none stated. Timeline: none stated. Team: solo (user + coding agent).
- Regulatory: none.
- Portability: must work in Claude Code, OpenCode, and claude.ai — six spec frontmatter fields only, no Claude Code-only body syntax.
- Distribution: `.claude-plugin/` manifests + `install.sh` symlink path, following `skill_repo.md`.

## Asset audit

Greenfield — nothing to preserve or integrate. nanoPRD is a pattern source, not a runtime dependency.

## Deferred features

| Feature | Reason |
|---|---|
| SEO title/description/tag generation | vidIQ/TubeBuddy territory; user needs a script, not channel metadata |
| Storyboard image generation | Boords/Avey territory; script + shot list is the deliverable |
| Multi-user collaboration / review links | Solo creator; no second seat |
| Platform adaptation (Shorts/TikTok/Reels) | Long-form only |
| Runtime/timing calculator UI | No UI; timing is a computed field in the script if needed |
