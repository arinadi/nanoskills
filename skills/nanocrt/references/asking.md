# Asking discipline

**Goal:** asking is how you prove you understood the job before you do it. A
script, a plan, or a task list built on an unconfirmed understanding is guesswork
with formatting. This file is loaded by Phase 0 of every run and by any checkpoint
that needs to close an open question.

Source: `handbook_asking.md` (distilled; the full argument lives in the reference
inventory).

---

## The one rule

> **Ask before you decide, decide before you write.** If a preference, a choice,
> or a fact that changes the output has not been confirmed by the user, it is
> still open — even if the clock is running. An assumption written into a
> document becomes a wrong output one or two phases later, and the user pays for
> the rework, not the question.

Asking is not a weakness. It is the difference between a deliverable that is
*correct for this user* and one that is merely *plausible for anyone*.

---

## Three kinds of question

| Kind | When | Example |
|---|---|---|
| **Clarify** | The input is ambiguous or missing — you cannot proceed honestly | "Is the keyword 'kopi nusantara' a search phrase or a brand name?" |
| **Confirm** | You inferred something from evidence or a reference and want to lock it | "The research points to `underdog` as the universal value — confirm?" |
| **Choose** | Two or more options are all valid and the user has a stake | "Structure: five-part, on-a-day, or none?" |

Use the cheapest kind that closes the gap. Do not ask a *choose* question when a
*confirm* question will do — presenting options the user does not care about is
noise.

---

## When to ask, when to proceed

Ask when the answer **changes the output in a way the user would care about**:

- A preference that shapes tone, scope, or structure (mood, angle, duration,
  audience, language).
- A decision with real alternatives (story structure, universal value, keyword).
- Anything you are about to claim as fact that you have not verified.

Do **not** ask when:

- The answer is already recorded in a reference file or an earlier answer —
  confirm instead of re-asking.
- The decision is reversible and cheap (file naming, minor formatting).
- The answer is genuinely "unset" and the user explicitly delegated it.

When in doubt, ask. The cost of one question is a sentence; the cost of a wrong
assumption is a phase of rework.

---

## The confirm loop

Every inference you make must be surfaced for confirmation, not buried:

1. **State what you inferred** and the evidence for it.
2. **Ask for confirmation or an override.**
3. **Wait.** A silent assumption is an unconfirmed one.
4. **Record the outcome** (confirmed or overridden) in `decisions.md` or the
   execution log.

This applies to the three storytelling fields (story_structure, universal_value,
foreshadowing) when they were left `unset` in Phase 0, and to any preference the
research resolves on the user's behalf.

---

## The `[ASSUMES:]` marker

When a preference is genuinely unknown and cannot wait — the user has no keyword
yet, no duration, no audience — record it explicitly rather than quietly carrying
a guess forward:

```
[ASSUMES: keyword = "kopi nusantara" until user provides one]
```

Rules:

- Mark the assumption at the point it is first needed (usually `context.md`).
- Never let an assumption silently become a fact in a later deliverable.
- Phase 4 must check each `[ASSUMES:]` marker against the final output and report
  any that influenced the script as a gap or a confirmation.
- If the user later answers, replace the assumption, do not keep both.

---

## Checkpoints are question points

Every phase checkpoint is also a question point. Do not just print the checkpoint
block and wait for `APPROVED` — end it with the specific thing you need
confirmed:

```
PHASE 0 COMPLETE - Preferences recorded.

  Topic:       ...
  Mood:        ...

Confirm: the settings above match what you want? Reply APPROVED, or tell me
which one to change.
```

If there are open `[ASSUMES:]` markers or unresolved storytelling fields, name
them here. The user cannot approve what they have not been shown.

---

## The approval gate

- `APPROVED` means every item shown in the checkpoint block is accepted as-is.
- Anything else — a comment, a "looks good", a thumbs up — is **not** approval.
- If the user answers something other than `APPROVED`, treat it as revision
  instructions: record the change, update the file, and re-present the checkpoint.
- Never present a checkpoint and continue in the same turn. The gate is a hard
  stop, not a formality.