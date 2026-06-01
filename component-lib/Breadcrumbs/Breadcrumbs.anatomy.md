---
parent: "[[Breadcrumbs]]"
section: anatomy
---

> Source: Figma file `5YihJ5WuDvnvrlrRMC4sBp`, node `21927:40413`. See [[Breadcrumbs]] `figma` URL for the live reference.

<!-- STUB:GAP-005 source="Export the Breadcrumbs component set from Figma (node 21927:40413, file 5YihJ5WuDvnvrlrRMC4sBp) and save as figma-screenshot-Breadcrumbs.png in component-lib/Breadcrumbs/." -->
> **Visual reference (GAP-005):** Screenshot was captured by the MCP as an embedded image but not saved to disk. No `figma-screenshot-Breadcrumbs.png` exists. The component set displays 6 variants: light/dark × (no collapse · collapsed menu-closed · collapsed menu-open).

## Anatomy

Element structure extracted from the Figma layer tree (node `21927:40413`).

| # | Type | Name | Role | Notes |
|---|------|------|------|-------|
| 1 | frame | Page (× N) | Structural group | Repeating group: one `_Text link breadcrumb` + one separator text. N items shown depending on collapse state. |
| 2 | sub-component | `_Text link breadcrumb` | Fixed sub-component | Clickable link item; states: rest / hover / active / focus × light / dark (atom at node `20648:30062`). |
| 3 | text | `/` (separator) | Content / decorative | Bound to `--text/textcolor01`. Rendered as plain `<p>`. |
| 4 | frame | Menu | Structural group (optional) | Present only when `collapse?=yes`. Contains `_Text link elipsis` + trailing separator. |
| 5 | sub-component | `_Text link elipsis` | Fixed sub-component (conditional) | Ellipsis indicator; states: rest / hover / active / focus × light / dark (atom at node `22076:37746`). When `↪ menu?=yes` renders as a `<button>` that opens the overflow menu. |
| 6 | frame | Overflow Menu | Optional slot | Absolutely positioned dropdown; visible when `↪ menu?=yes`. Contains a `Slot` placeholder for custom content. Width: 160 px, radius: 6 px. |
| 7 | frame | Current page | Content element | Non-link current-page label. Text bound to `--text/textcolor01`. Controlled by the text property below. |

<!-- STUB:GAP-011 source="Ask the Figma component owner to rename the text property from 'curent page' to 'current page' in component node 21927:40413; re-extract after correction." -->
> **Figma typo (GAP-011):** The current-page text property/layer is named `curent page#20679:3` (one `r`) in Figma. This is an upstream Figma-side typo — **do not** replicate it in code prop names or copy.

### Sub-component: `_Text link breadcrumb` (node `20648:30062`)

| # | Type | Name | Role | Notes |
|---|------|------|------|-------|
| 1 | text | Link label | Content element | Body01 typography; `--actions/action08` for link colour. |
| — | — | States | — | rest / hover / active / focus; light mode and dark mode rows. |

### Sub-component: `_Text link elipsis` (node `22076:37746`)

| # | Type | Name | Role | Notes |
|---|------|------|------|-------|
| 1 | text / button | `...` label | Content element | Renders as `<p>` when `↪ menu?=no`; as `<button>` when `↪ menu?=yes`. `--actions/action08` (rest) / `--interactive/active07` (pressed/menu open). |
| 2 | frame | Overflow Menu | Optional slot (hidden) | Present only in `state=active` / `↪ menu?=yes` variants. |

## Variant axes

| Property | Values | Default |
|----------|--------|---------|
| `mode` | `light`, `dark` | `light` |
| `collapse?` | `no`, `yes` | `no` |
| `↪ menu?` | `no`, `yes` | `no` |

**Variant key map (6 components):**

| mode | collapse? | ↪ menu? | Node ID |
|------|-----------|---------|---------|
| light | no | no | `21927:40414` |
| dark | no | no | `22088:43533` |
| light | yes | no | `21984:40606` |
| dark | yes | no | `22088:43560` |
| light | yes | yes | `21984:42427` |
| dark | yes | yes | `22088:43590` |

> `collapse?=no, ↪ menu?=yes` is not a valid combination — the menu can only appear when collapsed.

No boolean toggles, persistent states (e.g. disabled), or size/density variants exist in this set.

## Interaction states

States visible in the Figma atom sub-components (`_Text link breadcrumb`, `_Text link elipsis`). Only rest-state token bindings are resolved — see [[Breadcrumbs.tokens]].

| State | Trigger | Visual change |
|-------|---------|---------------|
| rest | default | Link: `--actions/action08` |
| hover | pointer over | Distinct hover style present in atom (token binding unresolved — GAP-003) |
| active | pointer down | Distinct active style present in atom (token binding unresolved — GAP-003) |
| focus | keyboard Tab | Distinct focus ring present in atom (token binding unresolved — GAP-003) |
| menu open | click on `…` button | Ellipsis colour switches from `--actions/action08` to `--interactive/active07`; Overflow Menu becomes visible |

## Structure & spacing

| Property | Value | Notes |
|----------|-------|-------|
| Container height | 20 px | Driven by `body01` line-height; no explicit constraint |
| Container width | `fit-content` / `content-stretch` | Grows with trail length |
| Container padding | None | No padding on the root container |
| Gap (between Page groups) | 8 px | Hardcoded |
| Gap (link ↔ separator) | 8 px | Hardcoded |
| Overflow Menu gap (item rows) | 4 px | Hardcoded; applies when `↪ menu?=yes` |
| Overflow Menu width | 160 px | Hardcoded |
| Overflow Menu padding-y / -x | 9 px / 1 px | Hardcoded |
| Overflow Menu border-radius | 6 px | Hardcoded |
| Overflow Menu top offset | 24 px | Absolute position below ellipsis button |

- **Auto-layout:** horizontal, `items-center` (vertically centred).
- **Overflow:** no wrap — the trail never wraps to a second line (by design).

<!-- SKIP:WARN-003 manual="Confirm overflow-menu slot design intent with the Oxygen team before describing the slot API in the spec." -->
> **Overflow menu slot intent (WARN-003):** The overflow menu (`↪ menu?=yes`) shows a generic `Slot` placeholder in Figma annotated _"swap me with your content"_. It is unclear whether this is a designer composition hook (Figma-only) or a real runtime dropdown that consumers populate — `props.md` documents no API for overflow-menu content. Confirm with the Oxygen team before relying on it.

_Source: [[Breadcrumbs/Breadcrumbs-figma]] · Figma MCP · figma-console MCP · Extracted 2026-04-30_
