---
component: Pagination
package: "@8x8/oxygen-pagination"
category: navigation
role: figma
role_description: "Figma design spec — anatomy, variant axes, token bindings, and spacing extracted from Figma"
pipeline_stage: spec_ready
pipeline_note: "Audit verdict YES/PARTIAL — doc-rewrite can run"
audit_verdict: YES
siblings:
  - "[[Pagination/props]]"
  - "[[Pagination/examples]]"
  - "[[Pagination/tokens]]"
  - "[[Pagination/accessibility]]"
  - "[[Pagination/Pagination-usage]]"
  - "[[Pagination/Pagination-audit]]"
tags:
  - oxygen
  - component/Pagination
  - role/figma
  - stage/spec_ready
  - category/navigation
---
<!-- SOURCE: Figma MCP + figma-console MCP -->
<!-- FILE KEY: 5YihJ5WuDvnvrlrRMC4sBp -->
<!-- NODE ID: 55766:411 -->
<!-- EXTRACTED: 2026-05-01 -->
<!-- COMPONENT: Pagination -->
<!-- COLOR STRATEGY: B (>3 variant combos — states as columns, elements as rows) -->

# Pagination — Figma Design Spec

> **See also:** [props.md](./props.md) · [tokens.md](./tokens.md) ·
> [examples.md](./examples.md) · [accessibility.md](./accessibility.md)

---

## Visual reference

![Pagination](./figma-screenshot-Pagination.png)

---

## Anatomy

Element structure extracted from the Figma layer tree. The component set is `COMPONENT_SET` node `55766:414`.

The component renders as a horizontal flex row with `justify-between`. Two major regions:

| # | Type | Name | Role | Notes |
|---|------|------|------|-------|
| 1 | frame | Rows per page | optional slot | Shown when `rowsPerPage` boolean is `true`; hidden at `breakpoint < 548px` |
| 1a | text | Label | content | "Rows per page:" — localisation string |
| 1b | instance | Select (rows) | fixed sub-component | Dropdown for rows-per-page value; width 88px (default) / 72px (small) |
| 2 | frame | Page controls | structural | Always present |
| 2a | instance | previousButton | fixed sub-component | Icon button (arrow-left-long); padding varies by size |
| 2b | frame | Group | structural | Contains page label, page Select, pageCount |
| 2c | text | Page | content | "Page" — localisation string |
| 2d | instance | Select (page) | fixed sub-component | Dropdown for current page number |
| 2e | frame | pageCount | optional slot | Shown when `numberOfPages` boolean is `true`; renders "of {pages}" |
| 2f | instance | nextButton | fixed sub-component | Icon button (arrow-right-long); padding varies by size |

### Sub-component: Select

Used twice — for "rows per page" and "page number". Both share the same internal structure:

| # | Type | Name | Role | Notes |
|---|------|------|------|-------|
| 1 | frame | Input Text | structural | Background fill varies by state and mode |
| 2 | frame | Text | content | Displays current selected value |
| 3 | instance | arrow-down | fixed sub-component | `iconSizeS` (default) / `iconSizeXS` (small) |

### Sub-component: previousButton / nextButton

Icon buttons. Padding: `10px` (default, > 548px), `6px` (small, > 548px), `4px` (small, < 548px). Border radius: `6px`.

---

## API — Component properties

### Variant axes

| Property | Values | Default |
|----------|--------|---------|
| `mode` | `light`, `dark` | `light` |
| `size` | `default`, `small` | `default` |
| `isDisabled?` | `no`, `yes` | `no` |
| `breakpoint` | `> 548px`, `< 548px` | `> 548px` |

### Boolean toggles

| Property | Default | Notes |
|----------|---------|-------|
| `rowsPerPage` | `true` | Shows/hides the "Rows per page:" label + dropdown section; always hidden at `< 548px` breakpoint |
| `numberOfPages` | `true` | Shows/hides the "of {pages}" page count text next to the page dropdown |

### Instance swap slots

<!-- NO INSTANCE SWAP SLOTS FOUND -->

### Persistent states

| State | Property name | Notes |
|-------|--------------|-------|
| Disabled | `isDisabled?=yes` | Affects all interactive controls; dropdowns use `--interactive/disabled01` background, text uses `--interactive/disabled04` |

### Token coverage

- **Coverage:** High — most color and typography values use CSS variable tokens; widths and some paddings are hardcoded px values.
- **Hardcoded values flagged:**
  - `Select (rows).width (default)`: `88px` — no token binding found
  - `Select (page).width (default)`: `88px` — no token binding found
  - `Select (rows).width (small)`: `72px` — no token binding found
  - `Select (page).width (small)`: `72px` — no token binding found
  - `container.width (> 548px)`: `640px` — breakpoint-specific width, no token binding
  - `container.width (< 548px)`: `547px` / min `288px` — breakpoint-specific, no token binding
  - `previousButton.padding (default/> 548px)`: `10px` — no token binding
  - `previousButton.padding (small/> 548px)`: `6px` — no token binding
  - `previousButton.padding (small/< 548px)`: `4px` — no token binding
  - `border-radius`: `6px` on all interactive elements — no token binding

---

## Color & token bindings

<!-- COLOR STRATEGY B: states as columns, elements as rows -->

### Text & label elements

| Element | Token (light/enabled) | Light value | Token (light/disabled) | Light disabled | Token (dark/enabled) | Dark value | Token (dark/disabled) | Dark disabled |
|---------|----------------------|-------------|------------------------|---------------|----------------------|-----------|----------------------|--------------|
| "Rows per page:" label | `--text/textcolor01` | `#26252a` | `--text/textcolor01` | `#26252a` | `--text/textcolor01` | `white` | `--text/textcolor01` | `white` |
| "Page" label | `--text/textcolor01` | `#26252a` | `--text/textcolor01` | `#26252a` | `--text/textcolor01` | `white` | `--text/textcolor01` | `white` |
| "of N pages" pageCount | `--text/textcolor01` | `#26252a` | `--text/textcolor01` | `#26252a` | `--text/textcolor01` | `white` | `--text/textcolor01` | `white` |
| Select input text | `--text/textcolor01` | `#26252a` | `--interactive/disabled04` | `#8d8b7e` | `--text/textcolor01` | `white` | `--interactive/disabled04` | `#858585` |

### Select dropdown background

| Element | Light / enabled | Light / disabled | Dark / enabled | Dark / disabled |
|---------|----------------|-----------------|----------------|-----------------|
| Select (rows) Input Text bg | `--ui/ui05` → `#f4f3ee` | `--interactive/disabled01` → `#c8c8bd` | `--ui/ui05` → `#2f2e32` | `--interactive/disabled01` → `#c2c2c2` |
| Select (page) Input Text bg | `--ui/ui05` → `#f4f3ee` | `--interactive/disabled01` → `#c8c8bd` | `--ui/ui05` → `#2f2e32` | `--interactive/disabled01` → `#c2c2c2` |

### Text styles

| Element | Style token | Size | Weight | Line height | Letter spacing |
|---------|------------|------|--------|-------------|----------------|
| All text (default size) | `typography/body01/*` | `14px` | `400` (normal) | `20px` | `-0.06px` |
| All text (small size) | `typography/label01/*` | `12px` | `400` (normal) | `16px` | `0px` |
| Font family (default) | `typography/body01/font-family` | — | — | — | — |
| Font family (small) | `typography/font-family/sans` | — | — | — | — |

### Effect styles

<!-- NO EFFECT STYLES FOUND IN FIGMA RESPONSE -->

---

## Structure & spacing

### Container

| Property | Token | Value | Variant |
|----------|-------|-------|---------|
| Height | — | `40px` | default size |
| Height | — | `32px` | small size |
| Width | — | `640px` | > 548px breakpoint |
| Width | — | `547px` (max) / `288px` (min) | < 548px breakpoint |
| Auto-layout | — | horizontal flex, `justify-between` | all |

### Internal spacing

| Property | Token | Value | Notes |
|----------|-------|-------|-------|
| Gap within "Rows per page" group | — | `8px` | label + Select |
| Gap within "Page controls" group | — | `12px` | prev + page group + next |
| Gap within page group | — | `8px` | "Page" + Select + pageCount |
| Gap within pageCount | — | `2px` | "of" + page number |
| Select input padding (default) | — | `12px` horizontal, `8px` vertical | default size |
| Select input padding (small) | — | `8px` horizontal, `4px` vertical | small size |
| prev/next button padding (default, > 548px) | — | `10px` | default size |
| prev/next button padding (small, > 548px) | — | `6px` | small size |
| prev/next button padding (small/default, < 548px) | — | `4px` / `10px` | breakpoint < 548px |
| Border radius (buttons + dropdowns) | — | `6px` | all interactive elements |

### Auto-layout

- Direction: horizontal
- Alignment: `items-center`, `justify-between` (outer); `items-center` (inner groups)

### Density / size variants

| Variant | Property | Token | Value |
|---------|----------|-------|-------|
| default | Container height | — | `40px` |
| small | Container height | — | `32px` |
| default | Select width (rows/page) | — | `88px` |
| small | Select width (rows/page) | — | `72px` |
| default | Typography | `typography/body01/*` | 14px / 20px lh |
| small | Typography | `typography/label01/*` | 12px / 16px lh |
| default | Arrow icon size | — | `iconSizeS` |
| small | Arrow icon size | — | `iconSizeXS` |

---

## Interaction states

States visible in the Figma variant structure only; no transient hover/focus/pressed states modelled in the component set.

| State | Trigger | Visual change |
|-------|---------|---------------|
| Default | — | `--ui/ui05` dropdown background; `--text/textcolor01` text |
| Disabled | `isDisabled?=yes` | `--interactive/disabled01` dropdown background; `--interactive/disabled04` text; all controls non-interactive |

<!-- NO HOVER / FOCUS / PRESSED STATES FOUND IN FIGMA VARIANT STRUCTURE -->

---

## Design decisions & annotations

> **Pagination docs:** https://oxygen.8x8.com/components/pagination/usage

> **Breakpoint behaviour:** The component has two breakpoint variants. At `> 548px` the full layout is shown (rows-per-page on the left, page controls on the right). At `< 548px` the rows-per-page section is hidden and only page controls render. The `breakpoint` is a Figma variant axis — it is not directly mapped to an Oxygen prop; responsive handling is expected to be managed by the consuming application.

> **`rowsPerPage` and `numberOfPages` toggles:** These boolean properties in Figma control the visibility of the "Rows per page" section and the "of N pages" count respectively. They correspond to the `rowsPerPageOptions` and `numberOfPages` props (or similar logic) in the React component.

---

## Accessibility (from Figma annotations only)

<!-- NOT ANNOTATED IN FIGMA -->

- **ARIA role:** Not annotated in Figma
- **Focus order:** Not annotated in Figma
- **Keyboard interactions:** Not annotated in Figma

For full accessibility documentation see [accessibility.md](./accessibility.md).

---

## Gaps & conflicts

| Type | Description |
|------|-------------|
| Missing token | `Select.width` (88px default / 72px small) — hardcoded, no token binding |
| Missing token | Container width (640px / 547px) — breakpoint-specific, no token binding |
| Missing token | `previousButton`/`nextButton` padding (10px / 6px / 4px) — no token binding |
| Missing token | Border radius `6px` on all interactive elements — no token binding |
| Incomplete data | `figma_get_component_details` failed (Desktop Bridge not connected) — full variant key map unavailable |
| Incomplete data | `figma_get_variables` failed — token collection data unavailable; tokens extracted from inline CSS variables in design context only |
| Incomplete data | `figma_get_styles` returned empty — file styles not accessible via REST API |
| Missing annotation | No ARIA roles, focus order, or keyboard interaction annotations present in Figma |
| Conflict | Figma has a `breakpoint` variant axis (`> 548px` / `< 548px`) with no direct equivalent in the Oxygen React prop API — responsive layout is a consuming-app responsibility |
| Conflict | Figma boolean `rowsPerPage` toggle has no direct 1:1 Oxygen prop — `rowsPerPageOptions` array controls whether the rows-per-page dropdown renders |

---

_Source: Figma MCP · figma-console MCP · Extracted 2026-05-01_
