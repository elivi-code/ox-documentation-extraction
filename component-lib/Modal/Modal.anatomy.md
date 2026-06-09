---
parent: "[[Modal]]"
section: anatomy
component: Modal
role: spoke
pipeline_stage: published
audit_verdict: partial
siblings:
  - "[[Modal]]"
  - "[[Modal.props]]"
  - "[[Modal.tokens]]"
  - "[[Modal.usage]]"
  - "[[Modal.accessibility]]"
  - "[[Modal.platform]]"
  - "[[Modal.composition]]"
tags:
  - oxygen
  - component/Modal
  - role/spoke
  - stage/published
---

## Visual reference

![Modal component variants — Custom Modal and Dialog Modal in light and dark mode, mobile and desktop](source/figma-screenshot-Modal.png)

> Screenshot captured from node `2625:167` (Modal canvas) in file `5YihJ5WuDvnvrlrRMC4sBp`.
> Shows: Custom Modal (top row) and Dialog Modal (bottom row), each in light/dark × mobile/desktop.

---

## Component set overview

The Modal Figma page (`2625:167`) contains two component sets and an Atoms section:

| Set | Node ID | Description |
|-----|---------|-------------|
| Custom Modal | `29083:47583` | Full-featured modal with swappable content Slot, optional scrollbar |
| Dialog Modal | `30172:50869` | Compact confirmation dialog with description text |
| Atoms | `30347:46293` | `_footer` and `_header` sub-components shown in isolation |

<!-- STUB:GAP-003 source="Enable Figma Desktop Bridge plugin and re-run figma_get_variables (resolveAliases=true) and figma_get_styles to obtain authoritative variable bindings; update Modal-figma.md with confirmed token coverage %" -->

---

## Anatomy

### Custom Modal (`29083:47583`)

| # | Layer name | Type | Role | Notes |
|---|-----------|------|------|-------|
| 1 | `_header` | Frame (instance) | Fixed sub-component | Always present; contains title + optional close icon |
| 1a | `Title` | Frame | Content element | Flex column; wraps title text |
| 1b | Title text | Text | Content element | Uses `heading01` type style |
| 1c | `Icon Button` | Instance | Optional slot | Close button; visible when `onClose` is wired |
| 2 | `Scroll content` | Frame | Structural | Horizontal flex; holds Content + optional Scrollbar |
| 2a | `Content` | Frame | Content element | Scrollable area; swap the `Slot` with actual content |
| 2b | `Slot` | Instance | Optional slot `(swappable)` | Placeholder — use instance swapper in Figma |
| 2c | `Scrollbar_Mac OS` | Frame | Optional slot `(hidden)` | Toggled by `scrollbar` boolean property |
| 3 | `_footer` | Frame (instance) | Fixed sub-component | Always present; contains button group + optional divider |

### Dialog Modal (`30172:50869`)

| # | Layer name | Type | Role | Notes |
|---|-----------|------|------|-------|
| 1 | `_header` | Frame (instance) | Fixed sub-component | Same as Custom Modal header |
| 2 | `Content` | Frame | Content element | Renders `message` text; no Slot — not swappable |
| 3 | `_footer` | Frame (instance) | Fixed sub-component | Same footer atom as Custom Modal |

### Atoms (`30347:46293`)

| Sub-component | Node ID | Variants |
|--------------|---------|---------|
| `_footer` | `29083:47566` | `mode` (light/dark) × `stacked?` (false/true) |
| `_header` | `43118:1490` | `mode` (light/dark) |

---

## Variant axes

### Custom Modal

| Property | Values | Notes |
|----------|--------|-------|
| `mode` | `light`, `dark` | Drives all color token switches |
| `breakpoint` | `mobile`, `desktop` | Controls width (`320px` mobile / `664px` desktop) |
| `scrollbar` | `true`, `false` | Boolean toggle; shows `Scrollbar_Mac OS` overlay |

### Dialog Modal

| Property | Values | Notes |
|----------|--------|-------|
| `mode` | `light`, `dark` | Drives all color token switches |
| `breakpoint` | `mobile`, `desktop` | Controls width (`320px` / `664px`) |
| `message` | string | Description text rendered in the content area |

### Footer atom (`_footer`)

| Property | Values | Notes |
|----------|--------|-------|
| `mode` | `light`, `dark` | — |
| `stacked?` | `false`, `true` | `true` stacks buttons vertically |
| `divider` | boolean | Shows a `1px` separator above the footer |
| `textButton` | boolean | Shows/hides the tertiary text button |
| `secondaryButton` | boolean | Shows/hides the secondary button |

---

## Interaction states

| State | Mechanism | Notes |
|-------|-----------|-------|
| Light mode | `mode=light` variant | Default |
| Dark mode | `mode=dark` variant | — |
| Mobile | `breakpoint=mobile` | Width `320px` |
| Desktop | `breakpoint=desktop` | Width `664px`; desktop dark adds a visible border |
| With scrollbar | `scrollbar=true` | Overlaid Mac OS scrollbar track on right edge |
| Stacked footer | `stacked?=true` (footer atom) | Buttons stack vertically; shown in Atoms section |

---

## Hardcoded structural values

| Property | Element | Value | Flag |
|----------|---------|-------|------|
| Corner radius | Modal container | `6px` | ⚠ not tokenised |
| Scrollbar width | Scrollbar track | `12px` | ⚠ not tokenised |
| Scrollbar thumb width | Scrollbar indicator | `8px` | ⚠ not tokenised |
| Scrollbar thumb border radius | Scrollbar indicator | `100px` | ⚠ not tokenised |

<!-- STUB:GAP-013 source="Run figma_get_component with enrich=true via Figma Desktop Bridge to obtain authoritative token coverage %; depends on GAP-003 (Desktop Bridge activation)" -->

_Source: Figma MCP (claude.ai) + figma-console MCP · Extracted 2026-05-01_
