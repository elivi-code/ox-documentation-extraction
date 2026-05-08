---
component: Tabs
package: "@8x8/oxygen-tabs"
category: layout_overlay
role: figma
role_description: "Figma design spec — anatomy, variant axes, token bindings, and spacing extracted from Figma"
pipeline_stage: spec_complete
pipeline_note: "Canonical spec written — pipeline complete"
audit_verdict: YES
siblings:
  - "[[Tabs/props]]"
  - "[[Tabs/examples]]"
  - "[[Tabs/tokens]]"
  - "[[Tabs/accessibility]]"
  - "[[Tabs/Tabs-pui]]"
  - "[[Tabs/Tabs-audit]]"
  - "[[Tabs/Tabs-spec]]"
tags:
  - oxygen
  - component/Tabs
  - role/figma
  - stage/spec_complete
  - category/layout_overlay
---
# Tabs — Figma Reference

> **See also:** [props.md](props.md) · [examples.md](examples.md) · [tokens.md](tokens.md) · [accessibility.md](accessibility.md)

**File:** `UI components` (`5YihJ5WuDvnvrlrRMC4sBp`)
**Last modified:** 2026-04-30

---

## Pages

| Page | Node ID | Description |
|------|---------|-------------|
| Tabs (component page) | `2406:2` | Houses component set and atoms |
| ↳ Tabs examples | `85697:271849` | How-to, accessibility, and prototype atoms |

---

## Components on the Tabs page

### `tabs` — COMPONENT_SET

**Node:** `85651:78740`
**Figma link:** [Open in Figma](https://www.figma.com/design/5YihJ5WuDvnvrlrRMC4sBp/UI-components?node-id=85651-78740)

#### Variants (4)

| Variant name | isSelected | isDisabled | state | Bottom border |
|-------------|-----------|-----------|-------|--------------|
| `state=rest, isSelected=false, isDisabled=false` | false | false | rest | 1px, light gray (`#EBEAE1`) |
| `state=rest, isSelected=false, isDisabled=true` | false | true | rest | 1px, muted gray (`#C8C7BD`) |
| `state=hover, isSelected=false, isDisabled=false` | false | false | hover | 1px, near-black (`#26253A`) |
| `state=rest, isSelected=true, isDisabled=false` | true | false | rest | **2px**, interactive blue (`#0057E0`) |

#### Layout

| Property | Value |
|----------|-------|
| Layout mode | VERTICAL (auto-layout) |
| Padding | 16px all sides |
| Sizing | HUG (width and height) |
| Default size | ~68px wide × 52px tall |
| Transition | SMART_ANIMATE, 70ms, cubic-bezier(0.2, 0, 0.38, 0.9) |

#### Design properties

| Property | Type | Default |
|----------|------|---------|
| `state` | Variant | `rest` |
| `isSelected` | Variant | `false` |
| `isDisabled` | Variant | `false` |
| `tabLabel` | Text | `"Label"` |
| `icon` | Boolean | `false` |
| `selectIcon` | Instance swap | chevron icon |
| `badge` | Boolean | `false` |
| `isFocus` | Boolean | `false` |
| `hasDropdown` | Boolean | `false` |

---

### `tabsDisclosure` — COMPONENT

**Node:** `85651:78793`
**Figma link:** [Open in Figma](https://www.figma.com/design/5YihJ5WuDvnvrlrRMC4sBp/UI-components?node-id=85651-78793)

The overflow "more" trigger button. Shown when not all tabs fit in the container.

| Property | Value |
|----------|-------|
| Layout mode | VERTICAL (auto-layout) |
| Padding | 6px all sides |
| Size | 52 × 52px |
| Contains | `Icon Button` (chevron-down) + optional badge frame |
| Bottom border | 1px, same token as rest state |

#### Design properties

| Property | Type | Default |
|----------|------|---------|
| `badge` | Boolean | `false` |

#### States (inherited from Icon Button)

`rest` · `hover` · `active` · `focus/selected` · `disabled` · `badge`

---

### `.Tabs Popover` — COMPONENT (Atom)

**Node:** `86115:3520`
**Section:** Atom (`86754:680`)
**Size:** 296 × 200px

The popover/dropdown menu that renders overflow tabs. Shown in the Atom section of the examples page.

---

## Examples page sections

| Section | Node ID | Dimensions | Description |
|---------|---------|------------|-------------|
| 📜 How to use `<tabs />` in prototypes | `86013:1449` | 972 × 6368 | Design usage guide: states, properties, progressive overflow, active tab visibility, last visible tab behaviour |
| 🦽 Accessibility for `<tabs />` | `86302:721` | 972 × 2577 | Keyboard navigation, focus indicators, WCAG checklist |
| Atom | `86754:680` | 404 × 346 | `.Tabs Popover` atom component |

---

## Visual snapshots

### `tabs` component set — all variants

![tabs component set showing rest, hover, selected, disabled states](figma-tabs-variants.png)

> States visible (top to bottom): rest/unselected · hover · selected (2px blue underline, bold label) · disabled

### `tabsDisclosure` — overflow button

![tabsDisclosure chevron-down button](figma-tabs-disclosure.png)

### `.Tabs Popover` — overflow menu atom

![Tabs Popover atom showing Section 1–5 list items](figma-tabs-popover-atom.png)

---

## Color & token bindings

Token values resolved via `figma_execute` + `getVariableByIdAsync` alias chain traversal on node `85651:78740` (UI-components → UI-Foundations library). All values confirmed from Figma.

<!-- COLOR STRATEGY B: states as columns, elements as rows (4 variants × 2 modes > 3 threshold) -->

### Tab item — color tokens by state

| Element | Semantic token | Primitive (Light) | Hex (Light) | Primitive (Dark) | Hex (Dark) |
|---------|---------------|-------------------|-------------|------------------|------------|
| Bottom border — rest/unselected | `ui/ui01` | `color/offWhite/offWhite09` | `#ebeae1` | `color/gray/gray05` | `#666666` |
| Bottom border — selected (2px) | `actions/action01` | `color/blue/blue05` | `#0056e0` | `color/blue/blue07` | `#4687ed` |
| Label text — rest | `text/textColor01` | `color/offWhite/offWhite02` | `#26252a` | `color/pure/white` | `#ffffff` |
| Label text — disabled | `interactive/disabled02` | `color/offWhite/offWhite08` | `#c8c8bd` | `color/gray/gray05` | `#666666` |
| Icon fill | `icon/icon01` | `color/offWhite/offWhite02` | `#26252a` | `color/pure/white` | `#ffffff` |
| Focus ring | `interactive/focus01` | `color/blue/blue05` | `#0056e0` | `color/blue/blue10` | `#d7e3f9` |
| Notification badge | `notification/notification01` | `color/turqouise/turqouise05` | `#048284` | `color/turqouise/turqouise10` | `#78cdcf` |

> The `text/textColor02` token (`#6c6862` Light / `#c2c2c2` Dark) was also found bound in the component set — likely used for secondary/muted label context (e.g. the tab group label or tab count text, not the primary tab label).

### `tabsDisclosure` — overflow button tokens

The `tabsDisclosure` uses the same tokens as the `tabs` component set (inherits from `Icon Button`). Bottom border in rest state uses `ui/ui01`.

### Typography tokens

| Element | Token family | Size | Weight | Line-height | Letter-spacing |
|---------|-------------|------|--------|-------------|----------------|
| Tab label (unselected) | `typography/body01/` | `14px` | `400` | `20px` | `-0.06px` |
| Tab label (selected — bold) | `typography/bodyBold01/` | `14px` | `600` | `20px` | `-0.06px` |
| Tab disclosure label | `typography/labelBold01/` | `12px` | `600` | `16px` | `0px` |

---

## Legacy / hidden components

The following components are present on the Tabs page but are marked `visible: false` and are not part of the current design system:

| Name | Node ID | Note |
|------|---------|------|
| `Fixed width tabs` | `5178:4112` | COMPONENT_SET, hidden — legacy variant |
| `Rectangle 2` | `5178:4145` | RECTANGLE, hidden — design artifact |

---

_Source: Figma (file `5YihJ5WuDvnvrlrRMC4sBp`, pages `2406:2` and `85697:271849`) · Extracted 2026-04-30_
