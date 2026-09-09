# Decisions — nanoCRT

Architectural decision records. One entry per decision that was genuinely
contested, or that a future reader would otherwise reverse by accident.

## D1 — Two-column A/V script over screenplay format

- **Decided:** `script.md` uses the two-column A/V layout (visual column + audio
  column, one row per shot), per `reference/av-script-format.md`.
- **Considered:** screenplay/film format (sluglines, action, dialogue) and a
  narration-only script with inline shot notes.
- **Why this won:** the user picked "long-form, two-column AV" in discovery, and it
  is the industry standard for explainer video — the exact niche the user creates in.
- **Cost:** film-style screenplay conventions (INT./EXT. slugs, dialogue centering)
  are not available; a user who later wants true screenplay format needs a new
  template, not an edit.

## D2 — Working folder is `<project>_crt/`, not `<project>_plan/`

- **Decided:** the skill writes its runtime output to `<project>_crt/`.
- **Considered:** reusing nanoPRD's `<project>_plan/` naming.
- **Why this won:** nanoPRD and nanoCRT can run in the same project folder; distinct
  suffixes keep the two outputs from colliding. `crt` is the tool's own name.
- **Cost:** it diverges from the nanoPRD pattern the user knows, so the README must
  state the folder name explicitly.

## D3 — crawl4ai as the fetch fallback, not the default

- **Decided:** research prefers the built-in URL fetch tool; it escalates to
  crawl4ai v0.9.x only when fetch cannot read a page.
- **Considered:** making crawl4ai the primary research fetch mechanism.
- **Why this won:** crawl4ai needs `pip install` + a browser setup on the user's
  machine — an install the skill must never do silently. Built-in fetch is zero-cost
  and covers most sources.
- **Cost:** JS-heavy or bot-blocked news portals need the fallback path, so research
  can be slower or require user action for those sources.

## D4 — Runtime is a computed line, not a phase or feature

- **Decided:** the script computes `narration words ÷ 150 wpm + transitions` as a
  single line under the title; no separate timing phase and no UI.
- **Considered:** a dedicated timing step between outline and script.
- **Why this won:** runtime needs the actual narration text to be meaningful, so it
  belongs to the script phase; a separate phase would compute from a skeleton and be
  wrong. This was a scope challenge the user accepted (PRD §10).
- **Cost:** timing accuracy depends on the 150 wpm constant being stated in the
  script reference, which is now a maintenance point.

## D5 — Research split into two nanotasks (topic facts / audience-trends)

- **Decided:** Phase 1 decomposes into `03` (topic facts) and `04`
  (audience/trend/keyword), both writing to the one `research.md`.
- **Considered:** one "do the research" nanotask covering both.
- **Why this won:** the two halves are independently verifiable — sourced claims on
  one side, an angle-implication note on the other — and the user explicitly
  answered "both" when asked what research covers.
- **Cost:** `research.md` is written in two passes, so task 04 must re-open the file
  task 03 created rather than writing it fresh — a coordination point.

## D6 — Skill name `nanocrt`, not `nanoCRT`

- **Decided:** the skill folder and frontmatter `name` are lowercase `nanocrt`; the
  display name "nanoCRT" appears only in prose.
- **Considered:** mixed-case folder name matching the brand.
- **Why this won:** the spec constrains `name` to lowercase `[a-z0-9-]`, and the
  folder name must equal `name` or the skill silently fails to load.
- **Cost:** the repo/brand name and the skill ID differ in casing; documentation
  must be explicit about the distinction.
