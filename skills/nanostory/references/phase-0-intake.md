# Phase 0 — Intake and preferences

**Goal:** Capture the user's preferences before touching the assets, and record
them on disk. Preferences captured here are what make the catalog sharp instead
of generic.

**Load the `nanocrt` skill's `references/asking.md` first.** The asking discipline
governs this phase: confirm understanding, then ask, then record.

Five steps, in this order. The order is the point: confirming the job and reading
references before asking means you ask only what is genuinely undecided.

---

## Step 0 — Confirm you understood the job

Before any inventory or questions, restate the user's request back in one or two
sentences and ask:

> "To confirm I understood: you want a <duration> narrated video from the footage
> in <folder>, for <audience>, told from <angle> — is that right?"

Wait for a yes. If the user corrects it, incorporate the correction. A run that
starts from a wrong understanding produces a perfect script for the wrong video.

## Step 1 — Record the request verbatim

Write the user's initial request exactly as given. Not your paraphrase — the
original wording carries intent a summary loses.

## Step 2 — Inventory the footage folder and reference material

Establish what exists on disk. List the footage folder (or the file list the user
gave) so the manifest in Step 3 is complete — you should not ask about a file you
have not seen.

Also record every other reference the user pointed at (notes, a previous edit, a
mood board, an old script). Read each one. For each, record one line: what it
contributes and what it settles.

| Reference | Contributes | Settles |
|---|---|---|
| `raw/` | 47 clips, 2 days of travel | Asset pool for the whole project |

A question already answered by a reference is not asked again. State what you took
from the file and ask the user to confirm it instead of re-asking.

## Step 3 — Collect the asset manifest

You cannot watch video or inspect photos. The user can. Collect a per-file
description of every asset in the footage folder — this is the bridge that lets
you "see" the footage. For each file ask for:

- **What it shows** — subject, place, moment (e.g. "sunset on the beach, waves,
  golden light")
- **People** — who is in it, what they are doing (or "none")
- **Movement** — is the camera still, panning, walking, drone, handheld
- **Rough quality** — sharp/ok/soft; audio with speech vs ambient vs none (video)
- **Moment value** — is this a must-use, filler, or maybe-unusable?

Record the manifest verbatim into the context. If the user does not want to
describe every file, accept a folder-level description and mark the asset-level
rows as `[needs description]` in Phase 1 — but be explicit that Phase 3 cannot
anchor a visual row to an undescribed asset.

## Step 4 — Ask the preferences

Ask all of them, as one numbered message so the user sees the whole shape of what
is undecided. Mark each answer clearly.

### Mandatory

| # | Field | What a usable answer looks like |
|---|---|---|
| 1 | **Footage location** | "The folder `raw/` — 47 videos, 12 photos" or an explicit file list |
| 2 | **Mood** | "Documentary, calm and nostalgic" or "Energetic and upbeat travel" |
| 3 | **Angle / story goal** | "This trip taught me to slow down" — the position, not the topic |
| 4 | **Keyword** | The search phrase the video targets, e.g. "japan trip vlog" |
| 5 | **Language** | The language the final narration is written in. Defaults to **English**; choose Indonesian or any other only if the user explicitly asks |
| 6 | **Target duration** | "8 minutes" — drives scene count and runtime checks later |
| 7 | **Audience** | "Travel vlog viewers 20-35, mobile, want atmosphere not itinerary" |

### Storytelling (optional, three)

Asked with the seven above. Each may legitimately be **"unset"**, meaning "the
catalog or a later phase decides". See the `nanocrt` skill's
`references/storytelling.md` for the vocabulary.

| # | Field | A usable answer | Default when unset |
|---|---|---|---|
| 8 | **Story structure** | `five-part` \| `on-a-day` \| `none` | `on-a-day` (simplest, most flexible) |
| 9 | **Universal value** | `zero-to-hero` \| `underdog` \| `transformation` \| `redemption` \| `none` | Let Phase 1/2 infer from the assets |
| 10 | **Foreshadowing** | `on` \| `off` | `off` unless the trip has a natural reveal |

If a mandatory answer is missing or unusable, ask for that one again specifically.
Do not proceed with five answers when you have seven.

Wait for the answers. If a preference is genuinely not known by the user (e.g. they
have no keyword yet), record it as "unset" rather than inventing one — Phase 4 will
check against it as a gap.

When a preference stays unknown and the run needs it, mark it as an assumption
instead of silently defaulting:

```
[ASSUMES: keyword = "japan trip vlog" until user provides one]
```

Each assumption is recorded in `context.md` with the reason it is assumed, and is
listed in the Phase 0 checkpoint so the user can override it. See the `nanocrt`
`references/asking.md`.

## Step 5 — Write

Default the language to English if none was chosen (the user's explicit choice
always wins; never assume a non-English default). Then write:

```
<project>_story/meta/context.md
<project>_story/meta/progress.json
<project>_story/meta/execution-log.md
```

The working folder is `<project>_story/` — create it if it does not exist.

`progress.json` phase shape (mirrors nanoCRT, phases 0–4):

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

- The initial request, verbatim
- The confirmed understanding (Step 0), and any correction the user made
- Footage folder / file list
- Reference inventory: file, contributes, settles
- The asset manifest (per-file descriptions), verbatim
- The seven preferences and their answers, verbatim
- The three storytelling preferences and their answers (story_structure,
  universal_value, foreshadowing)
- The chosen language, explicitly
- Every `[ASSUMES:]` marker and why it was assumed
- Phase flow record (5 phases)

## Record

Update `meta/progress.json` (Phase 0 in_progress -> written) and append to
`meta/execution-log.md`.

## Checkpoint

Print this block, then stop. Do not continue until the user replies `APPROVED`.

```
PHASE 0 COMPLETE - Preferences recorded.

  Footage:     <folder or file list>
  Mood:        <mood>
  Angle:       <angle / story goal>
  Language:    <language>
  Duration:    <target duration>
  Structure:   <story_structure, or unset>
  Manifest:    <count> asset description(s)
  Assumptions: <count> [ASSUMES:] marker(s), if any

Written to <project>_story/meta/context.md

Confirm: the settings above match what you want, and each assumption is one
you accept. Reply APPROVED, or tell me which one to change.
```