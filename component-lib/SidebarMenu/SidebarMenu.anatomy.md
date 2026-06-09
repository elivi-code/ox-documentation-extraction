---
parent: "[[SidebarMenu]]"
section: anatomy
component: SidebarMenu
category: navigation
pipeline_stage: draft
figma: "https://www.figma.com/file/5YihJ5WuDvnvrlrRMC4sBp?node-id=62897:18973"
tags:
  - oxygen
  - component/SidebarMenu
  - role/anatomy
  - stage/draft
  - category/navigation
---

<!-- source: figma-only -->

## Visual reference

Figma file key: `5YihJ5WuDvnvrlrRMC4sBp`
Node IDs: `62897:18973` (Sidebar menu) · `62897:19352` (Sidebar menu - Sublist item)

Screenshot on file: `source/figma-screenshot-SidebarMenu.png` (light mode, expanded)

---

## Anatomy

### Component set: Sidebar menu (`62897:18973`)

Top-level structure of the `mode=light, collapsed?=false` variant.

| # | Type | Name | Role | Notes |
|---|------|------|------|-------|
| 1 | frame | Scroll | Structural — scrollable viewport | 200 × 643 px; contains Primary navigation |
| 2 | frame | Primary navigation | Structural — main nav list | 200 × 740 px; contains 17× `_Menu List Items / Expanded`; fill → `ui25` |
| 3 | frame | Secondary Navigation | Structural — footer slot | 200 × 186 px; contains dividers + 4× footer items; fill → `ui25` |
| 4 | instance (×n) | _Menu List Items / Expanded | Content element — nav item | Repeated instance; one per navigation entry |
| 5 | instance (×2) | Dividers | Structural/decorative | Horizontal rules separating footer sections |

> **Collapsed variant:** In `collapsed?=true`, the `Scroll` frame hides labels — only icons are visible. The `Secondary Navigation` frame is also present in icon-only form.

### Component set: Sidebar menu - Sublist item (`62897:19352`)

Structure of the `mode=light, State=Rest` variant.

| # | Type | Name | Role | Notes |
|---|------|------|------|-------|
| 1 | frame | Text Info | Content element — label area | 120×20 px; VERTICAL layout; `layoutGrow: 1` fills remaining width |
| 2 | text | List Label | Content element — primary label | Inter 14px/20px Regular; color → variable `20136:254`; always visible |
| 3 | text | Sub List Label | Optional slot — secondary label | Inter 12px/16px Regular; color → variable `20136:255`; `visible: false` by default |
| 4 | frame | Frame 6 | Optional slot — badge container | 16×20 px; HORIZONTAL; `visible: false` by default; controlled by `hasBadge` |
| 5 | instance | Badge (dot) | Optional slot — dot badge | 12×12 px; `type=dot`; color → variable `20136:487`; shown by `↪ small (no number)` |
| 6 | instance | Badge (counter) | Optional slot — count badge | 16×16 px; `type=counter`; padding 4px H; color → variable `20136:487`; shown by `↪ medium (with number)` |

<!-- STUB:GAP-010 source="Run figma_get_component_for_development on `_Menu List Items / Expanded` atom node ID 62897:19254 to extract its full internal anatomy (icon slot, label, hover/active states)" -->

---

## Variants

### Sidebar menu

| Property | Values | Default |
|----------|--------|---------|
| `mode` | `light`, `dark` | `light` |
| `collapsed?` | `false`, `true` | `false` |

<!-- CONFLICT:GAP-009 finding="Figma `collapsed?` variant axis does not map directly to a single React prop: `Sidebar` uses `initialCollapsedState` (uncontrolled initial value); `SidebarContainer` uses `collapsed` (controlled prop). Spec must declare which API surface this variant documents." HUMAN DECISION REQUIRED -->

### Sidebar menu - Sublist item

| Property | Values | Default |
|----------|--------|---------|
| `mode` | `light`, `dark` | `light` |
| `State` | `Rest`, `Hover`, `Selected`, `Focus`, `Disabled` | `Rest` |

---

## Boolean toggles

### Sidebar menu - Sublist item

| Property | Default | Notes |
|----------|---------|-------|
| `Secondary Label` | `false` | Shows/hides the secondary label text row below the primary label |
| `↪ small (no number)` | `false` | Badge dot variant (no count) |
| `↪ medium (with number)` | `false` | Badge with numeric count |
| `hasBadge` | `false` | Master badge visibility toggle |

> **Sidebar menu:** No boolean toggles at the component set level. Collapse state is controlled via the `collapsed?` variant axis.

---

## Persistent states

### Sidebar menu - Sublist item

| State | Notes |
|-------|-------|
| Disabled | Muted text, no interaction |
| Selected | Active route; bold text, darker background |

> Hover and Focus are transient — listed under Interaction states only.

---

## Interaction states

| State | Trigger | Visual change |
|-------|---------|---------------|
| Hover | Pointer over item | Background → `hover12` (`#EBEAE1` light / `#3D3D3D` dark) |
| Selected | Active route | Background → `active12`; text bold; persists until route changes |
| Focus | Keyboard Tab | Blue outline border visible |
| Disabled | `State=Disabled` | Text muted/greyed; no pointer interaction |
| Collapsed | `collapsed?=true` | Labels hidden; sidebar narrows to icon strip |

---

## Structure and spacing

### Sidebar menu — outer container

| Property | Value | Variant |
|----------|-------|---------|
| Width | 216 px | Expanded (`collapsed?=false`) |
| Height | 853 px | Expanded |
| Width | 52 px | Collapsed (`collapsed?=true`) |
| Height | 841 px | Collapsed |
| Padding top / bottom | 12 px | Both |
| Padding left / right | 8 px | Expanded |
| Padding left / right | 0 px | Collapsed |
| Item spacing | 0 px | Both |
| Layout direction | VERTICAL | Both |
| Background fill | `ui25` — `#F4F3EE` light / `#171719` dark | Both modes |
| Border | 1 px outside, `color/offWhite/offWhite09` | Both |

### Sidebar menu — internal frames

| Frame | Width | Height | Layout | Item spacing | Notes |
|-------|-------|--------|--------|-------------|-------|
| Scroll | 200 px | 643 px | HORIZONTAL | 0 px | Clips content (scrollable viewport) |
| Primary navigation | 200 px | 740 px | VERTICAL | 8 px | Hugs content height; fill → `ui25` |
| Secondary Navigation | 200 px | 186 px | VERTICAL | 8 px | Footer zone; pinned to bottom; fill → `ui25` |

### `_Menu List Items / Expanded` atom

| Property | Value |
|----------|-------|
| Width | 200 px |
| Height | 36 px |
| Corner radius | 6 px |
| Layout | VERTICAL |

### Sublist item

| Property | Value | Notes |
|----------|-------|-------|
| Width | 144 px | Fixed; fills container in use |
| Height | 36 px | |
| Padding top / bottom | 8 px | |
| Padding left / right | 12 px | |
| Item spacing (icon ↔ text) | 12 px | |
| Corner radius | 6 px | |
| Layout direction | HORIZONTAL | |

### Text styles (Sublist item)

| Element | Font | Size | Weight | Line height | Primitive token | Hex |
|---------|------|------|--------|-------------|-----------------|-----|
| List Label (primary) | Inter | 14 px | 400 Regular | 20 px | `color/offWhite/offWhite02` | `#26253A` |
| Sub List Label (secondary) | Inter | 12 px | 400 Regular | 16 px | `color/offWhite/offWhite05` | `#6C6861` |

> Sub List Label is `visible: false` by default — shown only when the `Secondary Label` boolean toggle is enabled.

### Badge atoms (inside Frame 6)

| Variant | Width | Height | Corner radius | Padding | Color variable |
|---------|-------|--------|---------------|---------|----------------|
| Dot (`↪ small`) | 12 px | 12 px | 8 px | — | `20136:487` |
| Counter (`↪ medium`) | 16 px | 16 px | 8 px | 4 px horizontal | `20136:487` |

<!-- STUB:GAP-007 source="Add inline Figma annotations to 'Sidebar menu' and 'Sidebar menu - Sublist item' component sets explaining key design decisions; re-run figma-extract to capture them" -->

_Source: Figma MCP · figma-console MCP · Extracted 2026-05-07_
