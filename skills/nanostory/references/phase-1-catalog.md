# Phase 1 — Catalog

**Goal:** Produce `catalog.md` — a complete inventory of every asset in the
footage folder, with technical metadata and a content/quality assessment. This is
the footage-first equivalent of `nanocrt`'s research phase: instead of sourcing
facts about a topic, you source facts about the assets. Everything the script
will later reference starts here.

Two halves, both required:

1. **Asset inventory** — every file, one row, with ffprobe technical metadata and
   the user's manifest description.
2. **Quality & coverage assessment** — per asset: content summary, shot type,
   usable seconds, quality signal. Flag unusable assets with a reason.

Phase 1 is not complete until **both** halves are written.

---

## ffprobe availability check

Run this **before** cataloging, in this exact order. The goal is to know whether
technical metadata can be read, then work within it.

1. **ffprobe present?** Run `ffprobe -version`. If it works, use it for every
   video/audio file: duration, resolution, fps, aspect ratio, codec.
2. **ffprobe absent?** Do **not** silently install packages. Tell the user
   Phase 1 needs ffprobe (ships with ffmpeg) and give the exact install command
   for their platform, then wait:
   - Fedora/Debian: `sudo dnf install ffmpeg` / `sudo apt install ffmpeg`
   - macOS: `brew install ffmpeg`
3. **Still no metadata capability?** Record "catalog: technical metadata skipped"
   in `catalog.md`, fill the content/quality columns from the manifest alone, and
   mark duration/resolution rows `[unknown]`. **Never invent metadata.**

The order matters: prefer reading real metadata, ask before installing, and never
fabricate a value.

---

## Pass 1 — Asset inventory

For each file in the footage folder:

- Assign an **asset id** in a stable scheme the later phases reuse, e.g.
  `A01`, `A02`, ... or `01_wide_market`, ... Pick one scheme, keep it consistent,
  and reuse the exact ids in Phase 2/3/4.
- Record the **path** relative to the project so the editor can find the file.
- Record **type**: video or photo.
- Run `ffprobe` and record duration, resolution, fps, aspect ratio, codec. For
  photos, ffprobe still reports resolution; duration is `N/A`.
- Attach the **manifest description** the user gave in Phase 0, verbatim.

Rules:

- Every file in the folder appears exactly once. If a file cannot be read,
  record it with a reason — do not drop it silently.
- Do not merge clips. One file, one row, even if it looks like a montage already.
- File names are facts; do not guess content from a filename alone.

## Pass 2 — Quality & coverage assessment

For each asset, assess what it can contribute to the video. This is where the
footage-first thinking starts:

- **Content summary** — one line synthesising the manifest: what the viewer sees.
- **Shot type** — classify using standard travel-doc vocabulary: wide /
  establishing, medium, close-up, POV, detail, cutaway, aerial, walk-through.
  Where unclear, prefer the user's manifest over your guess.
- **Usable seconds** — for video, the range that is genuinely usable (skip
  fumbling, horizon-tilt start, camera-down ending). Record as `in–out @ mm:ss`
  or a count.
- **Quality signal** — sharp / ok / soft; camera motion; whether audio is speech,
  ambient, or silent. Note any defect (blurry, over/underexposed, wind noise).
- **Unusable flag** — if a file contributes nothing (corrupt, fully blurry,
  redundant duplicate), mark it `UNUSABLE` with a one-line reason. Unusable assets
  stay in the inventory but are excluded from the coverage count.

End this pass with a **coverage note**: one or two sentences on what the footage
as a whole can support — e.g. "strong establishing and wide shots across 3
locations; almost no close-ups of people; audio mostly ambient". This is the
factual base the Phase 2 story must respect.

---

## Write

Write `catalog.md` using `templates/catalog.md`.

## Record

Update `meta/progress.json` and append to `meta/execution-log.md`.

## Checkpoint

Print this block, then stop. Do not continue until the user replies `APPROVED`.

```
PHASE 1 COMPLETE - Catalog written to <project>_story/catalog.md

  Assets:       <count> file(s)
  Usable:       <count> | Unusable: <count>
  Coverage:     <one-line note on what the footage can support>

Confirm: the catalog and coverage assessment match the footage you know.
Reply APPROVED to continue, or tell me which asset row to change.
```