---
parent: "[[Pagination]]"
section: accessibility
---

<!-- STUB:GAP-008 source="Neither OX MCP nor Figma component annotations provided explicit accessibility data — all guidance below is inferred from standard pagination patterns. Spot-check ARIA labels and keyboard behaviour against the rendered DOM before publishing (WARN-001)" -->

> **WARN-001:** All accessibility content is inferred from standard patterns. ARIA labels (e.g. `aria-label="Pagination"`) may not match the actual component implementation. Verify against the rendered DOM before publishing.

## ARIA Roles & Attributes

| Element | Role / Attribute | Notes |
|---------|-----------------|-------|
| Pagination container | `role="navigation"` | Identifies the region as a navigation landmark |
| Container | `aria-label="Pagination"` (or localised equivalent) | Distinguishes from other `<nav>` regions on the page |
| Previous button | `aria-label` from `translations.prevPage` | Icon-only button — must convey purpose via `translations` |
| Next button | `aria-label` from `translations.nextPage` | Icon-only button — must convey purpose via `translations` |
| Rows per page dropdown | `aria-label="Rows per page"` | Associates the visible label text with the control |
| Page location dropdown | `aria-label="Page number"` | Associates the visible "Page" label text with the control |
| Disabled button | `aria-disabled="true"` | Applied when `isDisabled=true`, `canGoBack=false`, or `canGoNext=false` |

## Keyboard Interactions

| Key | Behaviour |
|-----|-----------|
| `Tab` | Moves focus forward through all interactive controls (rows-per-page → prev → page selector → next) |
| `Shift + Tab` | Moves focus backward through controls |
| `Enter` / `Space` | Activates the focused button or opens the focused dropdown |
| `Arrow Up` / `Arrow Down` | Navigates options within an open dropdown |
| `Escape` | Closes an open dropdown |

Tab order: **rows-per-page dropdown → previous button → page selector dropdown → next button**

## Disabled State

When `isDisabled` is `true`, all interactive controls are non-operable. When `canGoBack` is `false`, the previous button is visually and programmatically disabled (`aria-disabled="true"`). When `canGoNext` is `false`, the same applies to the next button. Disabled buttons remain in the tab order to preserve keyboard navigation consistency.

## Screen Reader Guidance

- The `translations` prop provides all visible text — ensure values are meaningful in the target language and not truncated.
- The `translations.numberOfPages` string (e.g. `"of 10 pages"`) is announced when the page changes; keep it descriptive.
- Page change events should update content in a way screen readers detect; pair with an `aria-live="polite"` region on the associated content area if screen reader announcement of new page content is required.
- Pass `""` to `translations.numberOfPages` when the total page count is unknown — do not fabricate a number.

## WCAG 2.1 AA Checklist

| Criterion | Requirement | Guidance |
|-----------|-------------|---------|
| 1.3.1 Info and Relationships | Navigation landmark and labels | Use `role="navigation"` with `aria-label` |
| 1.4.3 Contrast (Minimum) | 4.5:1 text, 3:1 UI components | Verify button and dropdown contrast against `--text/textcolor01` and `--ui/ui05` values |
| 2.1.1 Keyboard | All functionality via keyboard | Prev/next buttons and both dropdowns must be keyboard-operable |
| 2.4.3 Focus Order | Logical focus sequence | Tab order: rows-per-page → prev → page selector → next |
| 2.4.7 Focus Visible | Visible focus indicator | All interactive elements must show a visible focus ring — never `outline: none` |
| 3.2.2 On Input | No unexpected context change | Page navigation fires only on explicit user action (click or Enter) |
| 4.1.2 Name, Role, Value | Interactive controls labelled | All buttons and dropdowns have accessible names via `translations` |
