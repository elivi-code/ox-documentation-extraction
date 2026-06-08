---
parent: "[[DataTable]]"
section: anatomy
---

## Anatomy

The DataTable is composed of **10 distinct Figma component sets** on the "Table" canvas. Each maps to a sub-component or region of the rendered table.

| # | Component Set | Node ID | Role |
|---|---------------|---------|------|
| 1 | `table cell` | 50268:24462 | Data cell — the main `<Cell>` area with all content type variants |
| 2 | `table header` | 50690:112119 | Column header cell — `<HeaderCell>` |
| 3 | `table start controls cell` | 53841:35814 | Left-side selection/drag cell — checkbox/radio row selector + status bar |
| 4 | `table end controls cell` | 54027:37388 | Right-side row action cell — overflow menu, inline buttons, collapse toggle |
| 5 | `table row hover` | 51615:26100 | Hover-state overlay with action buttons or icon buttons |
| 6 | `table start controls header` | 53841:36967 | Column header for the selection column (select-all, sort/drag indicators) |
| 7 | `table end controls header` | 54027:37204 | Column header for the end actions column |
| 8 | `table action header` | 54456:153760 | Toolbar above the table — `<TableHeader>` |
| 9 | `table footer` | 54587:154269 | Pagination row below the table — `<Pagination>` |
| 10 | `table collapsible row slot` | 55222:11958 | Slot area for expandable/collapsible row content |

### table cell (50268:24462)

| Type | Name | Role | Notes |
|------|------|------|-------|
| frame | state | Structural — background overlay | absolute fill; carries hover/active background |
| frame | statusBar | Optional slot (`statusBar?`) | 4px left-edge indicator; default hidden |
| frame | info | Content — primary + secondary text block | flex row, gap 8px |
| instance | icon | Optional slot (`icon?`) | Icon sub-component; default visible |
| text | Primary | Content element | body01 style; truncates with ellipsis |
| text | Secondary | Optional slot (`secondaryInfo?`) | label01 style; secondary text line |
| frame | _fixedDivider (left) | Optional slot (`fixedLeft?`) | 2px right-edge divider when pinned left |
| frame | _fixedDivider (right) | Optional slot (`fixedRight?`) | 2px left-edge divider when pinned right |

### table header (50690:112119)

| Type | Name | Role | Notes |
|------|------|------|-------|
| text | title | Content element | default "Table header" |
| instance | sortIcon | Optional slot (`sortIcon?`) | Sort direction indicator; hidden by default |
| instance | infoIcon | Optional slot (`infoIcon?`) | Info tooltip trigger; hidden by default |
| frame | _fixedDivider (left/right) | Optional slots (`fixedLeft?`/`fixedRight?`) | 2px dividers for pinned columns |

### table action header (54456:153760) → `<TableHeader>`

Nine slots on a single toolbar row: `title?`, `action?`, `alerts?`, `iconButtons?`, `search?`, `filter?`, `favourites?`, `results?`, plus a `↳ resultsText` text property (default `"31 results"`).

### table footer / Pagination (54587:154269)

`rows-per-page` select (left) · `navigation` arrows + page selector (right) · `page indicator` ("Page X of Y").

<!-- STUB:GAP-013 source="Run figma_get_component with enrich=true on node 55222:11958 (table collapsible row slot) and append internal anatomy, boolean toggles, and spacing. Currently only the variant axis (mode) is documented." -->

> **Incomplete (GAP-013):** `table collapsible row slot` (55222:11958) — only its `mode` variant axis is documented; internal anatomy not retrieved.

<!-- STUB:GAP-014 source="Run figma_get_component with format=reconstruction on node 51615:26100 (table row hover) to retrieve internal anatomy (hover overlay layer structure, button positions)." -->

> **Incomplete (GAP-014):** `table row hover` (51615:26100) — only top-level properties documented; hover overlay layer structure not retrieved.

## Variants & states

### table cell — variant axes

| Property | Values | Default |
|----------|--------|---------|
| `mode` | `light`, `dark` | `light` |
| `type` | `default`, `checkbox`, `radio`, `avatar`, `switch`, `text input`, `select input`, `icons`, `tag`, `link`, `action`, `trend`, `trend filled`, `status`, `sentiment`, `error filled`, `empty state`, `skeleton` | `radio` |
| `isCompact?` | `no`, `yes` | `no` |

Boolean toggles: `statusBar?` (false), `primaryInfo?` (true), `secondaryInfo?` (true), `icon?` (true), `info?` (true), `indicator?` (true), `fixedLeft?` (false), `fixedRight?` (false).

<!-- CONFLICT:GAP-002 finding="Figma table cell component set uses a single component with an 18-value type variant (default, checkbox, radio, avatar, switch, text input, select input, icons, tag, link, action, trend, trend filled, status, sentiment, error filled, empty state, skeleton). Oxygen code uses separate named components (TextCell, PrimaryTextCell, CheckboxCell, etc.) via columnHelper.accessor cell callbacks — no type prop on <Cell>. The design-to-code mapping is undefined." HUMAN DECISION REQUIRED -->

> **Unresolved (GAP-002) — Figma `type` ↔ Oxygen cell component mapping.** Only four types have unambiguous code analogues: `default` → `TextCell`, `checkbox` → `CheckboxCell` (via `getSelectColumnDef`), `radio` → via `getSingleSelectColumnDef`, `skeleton` → `loading={true}`. Unmapped types (`avatar`, `switch`, `text input`, `select input`, `icons`, `tag`, `link`, `action`, `trend`, `trend filled`, `status`, `sentiment`, `error filled`, `empty state`) need confirmation with the design system team before a custom cell renderer is shipped.

### table header — variant axes

`mode` (light/dark) · `type` (title/empty/skeleton, default title) · `state` (rest/hover, default rest). Toggles: `sortIcon?`, `infoIcon?`, `fixedLeft?`, `fixedRight?`.

### table start controls cell — variant axes

`mode` · `type` (checkbox/radio/skeleton) · `isCompact?` · `dragg?` (yes/no). Toggles: `statusBar?`, `favourite?`, `errorIcon?`, `checkbox?`, `radio?`, `controls?`, `fixed?`.

### table end controls cell — variant axes

`mode` · `type` (remove/overflow/collapse/buttons/skeleton, default overflow) · `isCompact?`. Toggles: `overflowMenu?`, `actionOne?`, `actionTwo?`, `actionThree?`, `fixed?`.

### table row hover — variant axes

`mode` · `isCompact?` · `type` (iconButtons/buttons, default iconButtons). Toggle: `isDraggable?`.

### table start controls header — variant axes

`mode` · `state` (rest) · `type` (checkbox/radio/skeleton) · `empty?` · `draggable?`. Toggles: `favourite?`, `errorIcon?`, `fixed?`.

## Structure & spacing

### table cell container

| Property | Value | Variant |
|----------|-------|---------|
| Min height | `64px` | `isCompact?=no` |
| Min height | _(not extracted)_ | `isCompact?=yes` |
| Width | `150px` (component default) | all |
| Padding horizontal | `16px` | all |
| Gap (icon → info) | `8px` | all |

Status bar: 4px × 63px, border radius 8px, background `--error/error01`. Fixed divider: 2px × 64px, background `--ui/ui01`. Table footer height ~88px. Auto-layout: table cell is horizontal, gap 8px, 16px horizontal padding, vertically centered; action header horizontal left-aligned with spacing groups; footer horizontal space-between.

<!-- STUB:GAP-010 source="Inspect the Figma table cell component set for isCompact?=yes variant dimensions, or query source code, to document the compact row height. get_design_context only returned the default 64px height." -->

> **Incomplete (GAP-010):** the `isCompact?=yes` row height was not captured — only the default `64px` is known.

## Interaction states

| State | Component | Trigger | Visual change |
|-------|-----------|---------|---------------|
| `hover` | table header | pointer over | `state=hover` variant — background tint |
| `hover` | table row hover | pointer over row | Overlay with `iconButtons`/`buttons` rendered on top |
| `rest` | table header | default | No background tint |
| `skeleton` | table cell / header / start controls / end controls | loading | `type=skeleton` variant — placeholder shimmer |
| `isCompact?=yes` | table cell, rows | density | Reduced row height |

## Design annotations

<!-- STUB:GAP-011 source="Request the design team adds component descriptions in Figma (Properties panel → Description field) for the core component sets: table cell, table header, table action header, table footer." -->

> **Missing (GAP-011):** all 10 Figma component-set `description` fields returned `null`. No design intent, rationale, or usage constraints are captured from Figma. Editorial guidance lives in [[DataTable.usage]] instead.

_Visual reference: Figma file `5YihJ5WuDvnvrlrRMC4sBp`, node `2433:0` (Table canvas)._
