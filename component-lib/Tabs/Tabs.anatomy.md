---
parent: "[[Tabs]]"
section: anatomy
pipeline_stage: doc_rewrite
tags:
  - oxygen
  - component/Tabs
  - role/spoke
  - section/anatomy
---

## Anatomy

The Tabs design system exposes three Figma components that assemble the full tabs experience:

| Component | Type | Node | Role |
|-----------|------|------|------|
| `tabs` | COMPONENT_SET | `85651:78740` | Individual tab item — all variant/state combinations |
| `tabsDisclosure` | COMPONENT | `85651:78793` | Overflow "more" trigger button |
| `.Tabs Popover` | COMPONENT (Atom) | `86115:3520` | Dropdown menu that lists overflow tabs |

---

### `tabs` component set — elements

| Element | Description |
|---------|-------------|
| Tab label | Text: `body01` (unselected) / `bodyBold01` (selected) |
| Bottom border | 1px all states except selected (2px); token varies by state |
| Icon slot | Optional leading icon; shown when `icon=true` |
| Badge frame | Optional notification indicator; shown when `badge=true` |
| Dropdown chevron | Shown when `hasDropdown=true`; transforms tab into popover trigger |
| Focus ring | 2px solid `interactive/focus01`; shown on keyboard focus (`isFocus=true`) |

---

### Variants

| Variant name | `state` | `isSelected` | `isDisabled` |
|-------------|---------|-------------|-------------|
| Default (rest/unselected) | `rest` | `false` | `false` |
| Hover | `hover` | `false` | `false` |
| Selected | `rest` | `true` | `false` |
| Disabled | `rest` | `false` | `true` |

> The COMPONENT_SET exposes only `rest` and `hover` variant axes. A press/active state on `tabsDisclosure` is inherited from Icon Button but is not represented as an explicit variant axis (WARN-003).

---

### States

| State | Bottom border | Label style | Label color |
|-------|--------------|-------------|-------------|
| Rest (unselected) | 1px `ui/ui01` (`#ebeae1`) | `body01` (400) | `text/textColor01` |
| Hover | 1px `text/textColor01` (`#26252a`) | `body01` (400) | `text/textColor01` |
| Selected | **2px** `actions/action01` (`#0056e0`) | `bodyBold01` (600) | `text/textColor01` |
| Disabled | 1px `interactive/disabled02` (`#c8c8bd`) | `body01` (400) | `interactive/disabled02` |
| Focus | `interactive/focus01` ring (2px solid) + underlying state tokens | — | — |

---

### Layout

| Property | `tabs` | `tabsDisclosure` |
|----------|--------|-----------------|
| Layout mode | VERTICAL auto-layout | VERTICAL auto-layout |
| Padding | 16px all sides | 6px all sides |
| Sizing | HUG × HUG | 52 × 52px fixed |
| Default size | ~68px wide × 52px tall | 52 × 52px |
| Transition | SMART_ANIMATE, 70ms, cubic-bezier(0.2, 0, 0.38, 0.9) | Inherited from Icon Button |

---

### Design properties

#### `tabs` component set

| Property | Type | Default | Notes |
|----------|------|---------|-------|
| `state` | Variant | `rest` | `rest` \| `hover` |
| `isSelected` | Variant | `false` | Maps to `isActive` prop in code |
| `isDisabled` | Variant | `false` | — |
| `tabLabel` | Text | `"Label"` | Tab display label |
| `icon` | Boolean | `false` | Show leading icon alongside label |
| `selectIcon` | Instance swap | chevron icon (node `85016:131`) | Icon component to render <!-- SKIP:GAP-006 manual="Query figma_get_component for node 85016:131 to retrieve the icon's canonical name; update selectIcon default." --> |
| `badge` | Boolean | `false` | Show notification badge |
| `isFocus` | Boolean | `false` | Force focus ring visible (prototyping use) |
| `hasDropdown` | Boolean | `false` | Transforms tab into popover trigger at single-tab overflow stage |

#### `tabsDisclosure` component

| Property | Type | Default | Notes |
|----------|------|---------|-------|
| `badge` | Boolean | `false` | Show notification badge on disclosure button |
| — | Inherited | — | States (rest/hover/active/focus/disabled/badge) inherited from Icon Button |

---

### Figma page structure

| Page/Section | Node ID | Dimensions | Description |
|-------------|---------|------------|-------------|
| Tabs (component page) | `2406:2` | — | Houses component set and atoms |
| ↳ Tabs examples | `85697:271849` | — | How-to, accessibility, prototype atoms |
| 📜 How to use `<tabs />` | `86013:1449` | 972 × 6368 | Design usage: states, properties, progressive overflow |
| 🦽 Accessibility for `<tabs />` | `86302:721` | 972 × 2577 | Keyboard, focus indicators, WCAG |
| Atom | `86754:680` | 404 × 346 | `.Tabs Popover` atom |

---

### Visual snapshots

<!-- STUB:GAP-004 source="Re-capture and save PNGs from Figma nodes 85651:78740, 85651:78793, 86754:680 using figma_take_screenshot. Three files needed: figma-tabs-variants.png, figma-tabs-disclosure.png, figma-tabs-popover-atom.png." -->

Screenshots are not yet available. Figma links:

- `tabs` component set (all variants): [node 85651:78740](https://www.figma.com/design/5YihJ5WuDvnvrlrRMC4sBp/UI-components?node-id=85651-78740)
- `tabsDisclosure` overflow button: [node 85651:78793](https://www.figma.com/design/5YihJ5WuDvnvrlrRMC4sBp/UI-components?node-id=85651-78793)
- `.Tabs Popover` atom: [node 86115:3520](https://www.figma.com/design/5YihJ5WuDvnvrlrRMC4sBp/UI-components?node-id=86115-3520)

---

### Legacy / hidden components

| Name | Node ID | Note |
|------|---------|------|
| `Fixed width tabs` | `5178:4112` | COMPONENT_SET — hidden, legacy variant |
| `Rectangle 2` | `5178:4145` | RECTANGLE — hidden, design artifact |

_Source: Figma (file `5YihJ5WuDvnvrlrRMC4sBp`) · Extracted 2026-04-30_
