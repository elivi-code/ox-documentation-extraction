# Pagination — Accessibility

> **See also:** [props.md](props.md) · [examples.md](examples.md) · [tokens.md](tokens.md)

> **Note:** The Oxygen MCP returned no explicit accessibility documentation for Pagination. The guidance below is inferred from the component's interactive nature and standard pagination accessibility patterns.

## ARIA Roles & Attributes

| Element | Role / Attribute | Notes |
|---------|-----------------|-------|
| Pagination container | `role="navigation"` | Identifies the region as navigation |
| Container | `aria-label="Pagination"` (or localised equivalent) | Distinguishes from other `<nav>` regions |
| Previous button | `aria-label="Previous page"` (or `translations.prevPage`) | Must convey purpose when icon-only |
| Next button | `aria-label="Next page"` (or `translations.nextPage`) | Must convey purpose when icon-only |
| Rows per page dropdown | `aria-label="Rows per page"` | Associates label text with control |
| Page location dropdown | `aria-label="Page number"` | Associates label text with control |
| Disabled state | `aria-disabled="true"` on buttons | When `isDisabled` or `canGoBack`/`canGoNext` is `false` |

## Keyboard Interactions

| Key | Behavior |
|-----|---------|
| `Tab` | Moves focus through all interactive controls (dropdowns, prev/next buttons) |
| `Shift + Tab` | Moves focus backwards through controls |
| `Enter` / `Space` | Activates the focused button or opens the focused dropdown |
| `Arrow Up` / `Arrow Down` | Navigates options within an open dropdown |
| `Escape` | Closes an open dropdown |

## Disabled State

When `isDisabled` is `true`, all interactive controls should be non-operable. When `canGoBack` is `false`, the previous button should be visually and programmatically disabled. Same applies to `canGoNext` for the next button.

## Screen Reader Guidance

- The `translations` prop provides all visible text labels — ensure values are meaningful in the target language and not truncated.
- The `numberOfPages` interpolation in `translations.numberOfPages` (e.g. `"of 10 pages"`) should be announced when the page changes.
- Page change events should update content in a way that screen readers detect; consider pairing with a live region (`aria-live="polite"`) on the associated content area.

## WCAG 2.1 AA Checklist

| Criterion | Requirement | Notes |
|-----------|-------------|-------|
| 1.3.1 Info and Relationships | Navigation landmark and labels | Use `role="navigation"` with `aria-label` |
| 1.4.3 Contrast (Minimum) | 4.5:1 text, 3:1 UI components | Verify button and dropdown contrast meet ratio |
| 2.1.1 Keyboard | All functionality via keyboard | Prev/next buttons and dropdowns must be keyboard-operable |
| 2.4.3 Focus Order | Logical focus sequence | Tab order: rows-per-page → prev → page dropdown → next |
| 2.4.7 Focus Visible | Visible focus indicator | All interactive elements must show a visible focus ring |
| 3.2.2 On Input | No unexpected context change | Page navigation should only fire on explicit user action |
| 4.1.2 Name, Role, Value | Interactive controls labelled | All buttons and dropdowns have accessible names |

_Source: Oxygen MCP · Extracted 2026-05-01_
