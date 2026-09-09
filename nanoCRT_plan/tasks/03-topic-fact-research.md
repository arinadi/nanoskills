# 03 - Phase 1 topic/fact research

## Behavior

> "nanoCRT writes sourced topic facts to `research.md` when intake is approved."

**Atomic:** one behavior — topic/fact research with sources.
**Doable:** the capability check, the source requirement, and the template are
specified.

## Depends on

02

## Requirements

- `skills/nanocrt/references/phase-1-research.md` instructs the agent to research
  the topic's facts and accuracy, sharpened by the Phase 0 preferences (topic,
  angle, keyword).
- Every factual claim in `research.md` carries a source URL. No unsourced facts.
- The web-access capability check (from `architecture.md` §6) is documented in the
  reference file: try built-in fetch → escalate to crawl4ai → ask to install → flag
  unverified.
- `skills/nanocrt/templates/research.md` has two sections: **topic facts** (this
  task) and **audience/trend/keyword** (task 04).
- If search is unavailable, the agent records "research skipped: search
  unavailable" and marks claims unverified — never invents findings.
- Phase ends with a checkpoint block and stops for `APPROVED`.

## Data and API

Entities: `research.md` (topic-facts section only). Audience section is task 04's.

External integration (from `architecture.md` §6):

| Service | Use | Failure | Degradation |
|---|---|---|---|
| Web search | discover sources | unavailable | record "skipped", flag unverified |
| Built-in fetch | read a source URL | JS/blocked | escalate to crawl4ai |
| crawl4ai v0.9.x | deep crawl fallback | not installed | ask user to run `pip install -U crawl4ai && crawl4ai-setup` |

## Technical notes

- "Sharpened by preferences" is the PRD differentiator — the keyword and angle must
  visibly constrain what gets researched, not just be recorded.
- crawl4ai usage is documented in `reference/crawl4ai.md`; the skill's own
  reference file points to the capability-check order and commands.
- Never silently install packages — the capability check always asks the user first.

## Acceptance checks

- [ ] Research reference file documents the 4-step capability check
      Command: `grep -qi 'crawl4ai' skills/nanocrt/references/phase-1-research.md`
- [ ] Research template has a topic-facts section
      Command: `grep -qi 'topic' skills/nanocrt/references/phase-1-research.md && grep -qi 'facts' skills/nanocrt/templates/research.md`
- [ ] Source-per-claim requirement is stated
      Command: `grep -qiE 'source|url' skills/nanocrt/references/phase-1-research.md`
- [ ] "Never invent findings" degradation rule is stated
      Command: `grep -qiE 'never invent|skipped|unverified' skills/nanocrt/references/phase-1-research.md`

## Out of scope for this nanotask

- Audience/trend/keyword research — task 04 (same file, second section).
- Outline/script/handoff — tasks 05, 06, 07.
