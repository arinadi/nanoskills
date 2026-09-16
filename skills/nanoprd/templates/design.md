# Design: [Project Name]

> Written by nanoPRD Phase 2, for every project mode. The shape of this document
> follows the mode, but the file always exists.
>
> - `web-app` / `mobile` — design system: tokens, components, states, screens.
> - `cli-tool` — command surface, output streams, color, help layout, prompts,
>   TUI layout where the tool is interactive.
> - `data-pipeline` / `ml-service` — output contract: log shape, metrics, result
>   format, error shape, dashboard or config surface.
>
> Preferences came from the Phase 2 questions; the raw answers live in
> `meta/decisions.md`. Do not restate them here - carry the conclusion.

## 1. Design direction

*The user's stated direction in two or three sentences: mood, what it must feel
like, what it must NOT look like. If any answer is missing, it was confirmed or
overridden in `decisions.md`.*

- Mood / aesthetic:
- Reference products:
- Anti-patterns:
- Theme: light / dark / both
- Brand color:
- Information density: dense / spacious

## 2. [mode] - what this design describes

*One paragraph naming the surface this design covers: for web-app/mobile the
screens and components; for cli-tool the commands, output, help, and prompts;
for data-pipeline/ml-service the log shape, metrics, result format, and error
shape. If the mode spans two surfaces (a CLI with a TUI, a pipeline with a
dashboard), list them here.*

## 3. Tokens

*Mode-appropriate tokens. For web-app/mobile: semantic color, typography, spacing,
elevation. For cli-tool: semantic ANSI colors, monospace, spacing in `ch`. For
headless modes: the fields and types of the output contract, and how failures are
represented.*

| Token | Value | Role |
|---|---|---|
| | | |

## 4. Layout and components

*The structural rules: grids, spacing, alignment for web/mobile; stdout/stderr
split, pipe safety, help layout for a CLI; stream or record framing for headless.
List the components with their states (default, focus, loading, error, empty for
UI; success, partial, failure for output contracts).*

## 5. ASCII wireframes

*One wireframe per core interface, 60-80 columns wide, box-drawing characters,
labelled regions, interaction notes beneath. A wireframe is the interface made
visible - without one the implementing agent rebuilds the layout from prose.*

### Wireframe: [interface name]

```
┌───────────────────────────────────────────────────────────┐
│                                                           │
│                                                           │
│                                                           │
│                                                           │
│                                                           │
└───────────────────────────────────────────────────────────┘
```

- Region 1 (top): what it holds, why it leads
- Region 2 (left): ...
- Region 3 (centre): ...
- Interaction: what happens on each primary action, including empty and error
  states

### Wireframe: [interface name]

```
┌───────────────────────────────────────────────────────────┐
│                                                           │
└───────────────────────────────────────────────────────────┘
```

- ...

## 6. Accessibility floor

*The non-negotiable minimum. For web/mobile: contrast, focus visibility, keyboard
reachability, motion preference. For cli-tool: NO_COLOR, TTY detection, keyboard
reachability. For headless: machine-readability of output. These become
acceptance checks in Phase 3.*

| Requirement | Target | Checked by |
|---|---|---|
| | | |