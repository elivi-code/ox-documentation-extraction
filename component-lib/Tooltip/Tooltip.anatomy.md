---
parent: "[[Tooltip]]"
section: anatomy
---

## Visual reference

![Tooltip Figma screenshot](source/figma-screenshot-tooltip.png)

<!-- source: figma-only -->

---

## Anatomy

The Tooltip canvas (`1797:0`) contains two primary frames and one atom section.

### Frame: `Tooltip` (3174:0)

The main tooltip body — text content plus optional directional arrow tip. The canvas renders a grid of all orientation × mode combinations.

| # | Type | Name | Role | Notes |
|---|------|------|------|-------|
| 1 | frame | Content | Structural container | `px-8px py-4px`, `rounded-6px`, `max-w-320px` |
| 2 | text | Text (140 chars max) | Content element | Body01 typography; fills container width |
| 3 | instance | _Tip (arrow) | Optional slot | Directional arrow; controlled by `enableArrow` prop |

### Frame: `Icon tooltip` (1956:11221)

A variant of the tooltip that includes an icon alongside the text.

| # | Type | Name | Role | Notes |
|---|------|------|------|-------|
| 1 | frame | Content | Structural container | Same padding as main tooltip |
| 2 | text | Text | Content element | Body01 typography |
| 3 | instance | Icon | Optional slot | Toggled by `Icon` variant axis |

<!-- STUB:GAP-016 source="Run get_design_context on node 1956:11221 to extract Icon tooltip dimensions and icon token bindings; update Icon tooltip anatomy table" -->

### Sub-component: `_Tip` (7987:8235) — Arrow/pointer atom

Located in the `Atoms` section (29870:42882).

| # | Type | Name | Role | Notes |
|---|------|------|------|-------|
| 1 | symbol | _Tip | Structural/decorative | Small arrow rendered below, above, left, or right of container |

---

## Variant axes

| Property | Values | Default | Notes |
|----------|--------|---------|-------|
| Mode | `Light`, `Dark` | `Light` | Background inverts between modes — see Color & tokens |
| Horizontal direction | `Bottom`, `Top`, `Left`, `Right` | `Bottom` | Figma variant axis; maps to `orientation` prop |
| Vertical direction | `Center`, `Left`, `Right` | `Center` | Figma sub-axis for alignment; maps to `-start`/`-end` suffixes |
| Icon _(Icon tooltip only)_ | `True`, `False` | `False` | Toggles icon slot |

### Figma → Oxygen `orientation` prop mapping

| Figma: Horizontal / Vertical | Oxygen `orientation` |
|------------------------------|---------------------|
| Bottom / Center | `bottom` |
| Bottom / Left | `bottom-start` |
| Bottom / Right | `bottom-end` |
| Top / Center | `top` |
| Top / Left | `top-start` |
| Top / Right | `top-end` |
| Right / Center | `right` |
| Left / Center | `left` |

> **Note on defaults:** Figma's default showcase variant is `Bottom / Center` (`orientation="bottom"`). The runtime component default is `orientation="top"` — see [[Tooltip.props]] and audit GAP-002 (resolved).

<!-- STUB:GAP-014 source="Re-run figma-extract with Desktop Bridge active to retrieve enriched component metadata from figma_get_component_details (enriched variant key map, full token coverage %). Update variant axes table when available." -->

---

## Boolean toggles

No boolean toggle properties are present in Figma. The `Icon` axis is a variant property, not a boolean toggle.

---

## Instance swap slots

No instance swap slots found in the Figma component response.

---

## Interaction states

| State | Trigger | Visual change |
|-------|---------|---------------|
| Default (visible) | — | Tooltip body rendered with `--ui/ui07` background |

Hover / focus / pressed states are not represented in Figma — Tooltip is a display-only component. Its trigger element carries interaction states. The Oxygen component handles show/hide via the `showOn` prop and `delay`.

---

## Structure & spacing

### Container

| Property | Token | Value | Notes |
|----------|-------|-------|-------|
| Max width | — (hardcoded) | `320px` | `326px` for Left/Right orientation — see WARN-002 in audit |
| Min width | — (hardcoded) | `24px` | |
| Padding horizontal | — (hardcoded) | `8px` | No token binding found |
| Padding vertical | — (hardcoded) | `4px` | No token binding found |
| Border radius | — (hardcoded) | `6px` | No token binding found |

### Auto-layout

- Direction: vertical (`flex-col`) for Top/Bottom orientations; horizontal (`flex-row`) for Left/Right
- Alignment: `items-center` (Center), `items-start` (Left), `items-end` (Right)

### Density / size variants

Only one size (`Small`) observed on the `_Tip` arrow atom. No size axis on the main Tooltip body.

---

## Design decisions

- **Color inversion:** The Light mode tooltip uses a dark background (`--ui/ui07 = #26252a`) and the Dark mode tooltip uses a light background (`--ui/ui07 = #f1f1f1`). This is intentional — tooltip backgrounds are always inverted relative to the page mode to create contrast.
- **Shadow implementation:** Light mode uses `drop-shadow` (CSS filter); Dark mode uses `box-shadow`. Both resolve to `--ui/shadow01` but the rendering approach differs. See [[Tooltip.tokens]] GAP-012.
- **Max character limit:** Placeholder text in Figma demonstrates the 320px max-width at 140 characters. The canonical limit is 140 (English) — see [[Tooltip.usage]].

---

## Accessibility annotations (Figma)

No ARIA role, focus order, or keyboard interaction annotations are present in the Figma component.

<!-- STUB:GAP-019 source="Request designer to add ARIA role, focus behaviour, and keyboard interaction annotations to the Tooltip Figma component." -->

See [[Tooltip.accessibility]] for full WAI-ARIA Tooltip pattern documentation.
