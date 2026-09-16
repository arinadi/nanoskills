# Phase 1 — Research

**Goal:** Produce `research.md` — grounded facts plus audience/trend/keyword
findings, all sharpened by the Phase 0 preferences. This is the "research" half of
nanoCRT and the gap no comparable tool fills.

Two passes, both driven by `meta/context.md`:

1. **Topic facts** — accuracy and substance of the topic.
2. **Audience / trend / keyword** — who watches, what trends, what they search,
   and what that means for the angle.

The two halves are independently verifiable: topic facts are sourced claims; the
audience/trend half ends in an angle-implication note that Phase 2 consumes.
Phase 1 is not complete until **both** halves are written.

---

## Web-access capability check

Run this **before** any research, in this exact order. The goal is to know what
the host agent can actually retrieve, then work within it.

1. **Built-in fetch present and working?** Try the URL fetch tool on a source you
   already found. If it returns usable content, use it — no extra dependency.
2. **Built-in fetch present but blocked?** The page is JS-rendered, paywalled, or
   the tool returns empty/error. Escalate to crawl4ai.
3. **crawl4ai not installed?** Do **not** silently install packages. Tell the user
   research needs it and give the exact commands, then wait:
   `pip install -U crawl4ai && crawl4ai-setup`.
4. **No crawl capability at all?** Record "research skipped: no web-crawl
   capability" in `research.md`, mark affected claims unverified, and continue
   with lower-confidence output. **Never invent findings.**

The order matters: prefer the built-in tool (zero cost), escalate only when it
fails, and always ask before installing anything on the user's machine.

---

## Pass 1 — Topic facts

Research the topic's accuracy and substance, constrained by the Phase 0 keyword
and angle. Do not research the whole world around the topic — research what the
angle needs.

Rules:

- **Every factual claim carries a source URL.** No unsourced facts. A claim whose
  source cannot be retrieved is marked `[unverified]` — never silently dropped and
  never restated as certain.
- Prefer primary or authoritative sources; for a factual explainer, a source that
  can be checked beats one that is merely popular.
- Record what the viewer must know, in dependency order — earlier facts support
  later ones.
- If search itself is unavailable, write "research skipped: search unavailable"
  at the top of the section and flag every claim as unverified.

## Pass 2 — Audience / trend / keyword

Research who watches this, what is trending in the niche, and what the audience
actually searches, using the Phase 0 keyword as the seed.

- Who is the audience for this topic (age, context, what they already know)?
- What is trending in the niche right now, and what does the audience already
  believe or ask about?
- Which keywords/phrases does the audience actually search? Record them with their
  source (search tool or fetched page).

End this pass with one **angle implication** note: what this research means for the
video's angle. One or two sentences the Phase 2 outline can act on directly. If the
Phase 0 keyword conflicts with what the audience actually searches, say so here —
that is a finding, not a problem to hide.

### Storytelling implication (feeds the storytelling preferences)

When `story_structure`, `universal_value`, or `foreshadowing` is `unset` in
Phase 0, this research decides them. Record a short note the outline can consume:

- **Universal value** — which of `zero-to-hero` / `underdog` / `transformation` /
  `redemption` (or `none`) this topic and audience most naturally support, and one
  concrete detail that anchors it. Base it on the facts found, not a guess.
- **Foreshadowing fit** — whether the topic has a natural early-clue/late-reveal
  (e.g. a surprising result worth hinting at) or whether forcing one would distort
  the facts. `on` only when a clean payoff is plausible.
- **Structure fit** — whether the facts can fill a Rising Action and a single
  climax (`five-part` / `on-a-day`) or the topic is purely instructional
  (`none`).

**These decisions are not final until the user confirms them.** Follow
`references/asking.md`: at the Phase 1 checkpoint, name each field research
resolved, state the evidence, and ask the user to confirm or override. Record the
outcome in `decisions.md`. Do not carry an inferred value into Phase 2 as if the
user had chosen it.

If a value is already set in Phase 0, confirm or correct it here with evidence
rather than restating it.

---

## Write

Write `research.md` using `templates/research.md`, then update
`meta/progress.json` and append to `meta/execution-log.md`.

## Checkpoint

Phase 1 output must be reviewed and approved by the user before Phase 2 begins.
