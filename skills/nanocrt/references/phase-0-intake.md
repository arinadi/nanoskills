# Phase 0 — Intake and preferences

**Goal:** Capture the user's preferences before any research, and record them on
disk. Preferences captured here are what make Phase 1 research sharp instead of
generic.

Four steps, in this order. The order is the point: reading references before
asking means you ask only what is genuinely undecided.

---

## Step 1 — Record the idea verbatim

Write the user's initial idea exactly as given. Not your paraphrase — the original
wording carries intent a summary loses.

## Step 2 — Inventory reference material

Every file or link the user pointed at, plus anything already in the project
folder that bears on the idea: a previous script, a competitor's video, notes, a
mood board.

Read each one. For each, record one line: what it contributes and what it settles.

| Reference | Contributes | Settles |
|---|---|---|
| `old-script.md` | Existing structure and tone | Scene format for this channel |

A question already answered by a reference is not asked again. State what you took
from the file and ask the user to confirm it instead of re-asking.

## Step 3 — Ask the seven preferences

Ask all seven, as one numbered message so the user sees the whole shape of what is
undecided. Mark each answer clearly.

| # | Field | What a usable answer looks like |
|---|---|---|
| 1 | **Topic** | "The history of coffee in Indonesia", not "something about coffee" |
| 2 | **Mood** | "Documentary, calm and trustworthy" or "Energetic and punchy" |
| 3 | **Angle** | "Why local farmers lost the value chain" — a position, not the topic again |
| 4 | **Keyword** | The search phrase the video targets, e.g. "kopi nusantara" |
| 5 | **Language** | The language the final script is written in. Defaults to **English**; choose Indonesian or any other only if the user explicitly asks |
| 6 | **Target duration** | "10 minutes" — drives scene count and runtime checks later |
| 7 | **Audience** | "Indonesian coffee enthusiasts, 18–35, watch on mobile" |

If a mandatory answer is missing or unusable, ask for that one again specifically.
Do not proceed with five answers when you have seven.

### Storytelling preferences (optional, three)

Ask these with the seven above — one numbered message. Unlike the mandatory
fields, each of these may legitimately be answered **"unset"**, meaning "the
research or a later phase decides". See `references/storytelling.md` for the
vocabulary these answers draw on.

| # | Field | A usable answer | Default when unset |
|---|---|---|---|
| 8 | **Story structure** | `five-part` \| `on-a-day` \| `none` (pure argument, no arc) | `on-a-day` (simplest, most flexible) |
| 9 | **Universal value** | `zero-to-hero` \| `underdog` \| `transformation` \| `redemption` \| `none` | Let Phase 1/2 infer from the topic; `none` only if the topic is purely instructional |
| 10 | **Foreshadowing** | `on` \| `off` | `off` unless the topic has a natural reveal |

Wait for the answers. If a preference is genuinely not known by the user (e.g. they
have no keyword yet), record it as "unset" rather than inventing one — Phase 4 will
check against it as a gap.

## Step 4 — Write

Default the language to English if none was chosen (the user's explicit choice
always wins; never assume a non-English default). Then write:

```
<project>_crt/meta/context.md
<project>_crt/meta/progress.json
<project>_crt/meta/execution-log.md
```

The working folder is `<project>_crt/` — create it if it does not exist.

`progress.json` phase shape (mirrors nanoPRD, phases 0–4):

```json
{
  "project": "<project>",
  "current_phase": 0,
  "phases": {
    "0": { "status": "in_progress", "completed_at": null },
    "1": { "status": "pending", "completed_at": null },
    "2": { "status": "pending", "completed_at": null },
    "3": { "status": "pending", "completed_at": null },
    "4": { "status": "pending", "completed_at": null }
  }
}
```

---

## What `context.md` must contain

- The initial idea, verbatim
- Reference inventory: file, contributes, settles
- The seven preferences and their answers, verbatim
- The three storytelling preferences and their answers (story_structure,
  universal_value, foreshadowing)
- The chosen language, explicitly
- Phase flow record (5 phases)

## Checkpoint

Phase 0 output must be reviewed and approved by the user before Phase 1 begins.
