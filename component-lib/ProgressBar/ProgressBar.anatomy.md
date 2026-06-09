---
parent: "[[ProgressBar]]"
section: anatomy
component: ProgressBar
pipeline_stage: spec_ready
tags:
  - oxygen
  - component/ProgressBar
  - role/spoke
  - section/anatomy
---

## Anatomy

Element structure extracted from the Figma layer tree of the `Bar` component set (node `30880:55942`). All 4 variants share this structure.

| # | Type | Name | Role | Notes |
|---|------|------|------|-------|
| 1 | frame | `bar` | structural | Track background; full width, 8px height, 8px border-radius |
| 2 | frame | `linear-bar-indicator` | optional slot | Loading fill inside the track; visible when `status=loading` |
| 3 | frame | `linear-bar-bg-complete` | optional slot | Complete fill covering full track width; visible when `status=complete` |
| 4 | text | text label | optional slot | Supporting text below the bar; toggled by `text?` boolean property |

## Variants

| Axis | Values | Default | Oxygen mapping |
|------|--------|---------|----------------|
| `status` | `loading`, `complete` | `loading` | Derived from `value`: 0–99 → loading, 100 → complete |
| `mode` | `light`, `dark` | `light` | Set via `ThemeProvider` — no component prop |

See [[ProgressBar.props]] for the `value`-to-status mapping and theming note.

## States

| State | Trigger | Visual change |
|-------|---------|---------------|
| Loading | `value` is 0–99 | Blue/indigo fill (`--actions/action04`) covers partial track width |
| Complete | `value` reaches 100 | Green fill (`--success/success01`) covers full track width |

ProgressBar is a passive display component — no hover, focus, or pressed states exist.

## Structure & spacing

### Container

| Property | Value | Token |
|----------|-------|-------|
| Direction | vertical (flex-col) | — |
| Alignment | items-start (left-aligned) | — |
| Gap (bar → text label) | 8px | — (hardcoded; see GAP-012) |

### Bar track

| Property | Value | Token |
|----------|-------|-------|
| Height | 8px | — (hardcoded; see GAP-012) |
| Border-radius | 8px (full pill) | — |
| Width | 100% of container | — |

> **Figma demo artifacts (not real values):** container width `184px` is a Figma placeholder; runtime width is controlled by `size` / `fullWidth` props. Loading fill right-inset `41.85%` is a demo percentage; runtime fill width is driven by `value`.

<!-- STUB:GAP-011 source="Run figma_get_component_details with componentName='Progress bar' when Desktop Bridge is available; record the Figma component key in ProgressBar-figma.md for downstream Code Connect use" -->
<!-- STUB:GAP-012 source="Flag to design: should bar-track height (8px) and bar-to-label gap (8px) be spacing tokens? Confirm intent and update ProgressBar-figma.md once decided" -->
