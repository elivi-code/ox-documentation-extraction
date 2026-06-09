---
parent: "[[SidebarMenu]]"
section: accessibility
component: SidebarMenu
package: "@8x8/oxygen-sidebar-menu"
category: navigation
pipeline_stage: draft
tags:
  - oxygen
  - component/SidebarMenu
  - role/accessibility
  - stage/draft
  - category/navigation
---

> **Note:** The Oxygen MCP returned no explicit accessibility documentation for `@8x8/oxygen-sidebar-menu`. The guidance below is inferred from the component's nature as an interactive navigation pattern and from props observed in examples (e.g. `badgeAriaLabel`, `aria-label` on `SubMenuItem`).

---

## ARIA roles and semantics

| Component | Inferred HTML / ARIA role | Notes |
|---|---|---|
| `SidebarContainer` | Landmark — `<nav>` | Should wrap the entire sidebar to expose it as a navigation landmark. |
| `MenuList` | `role="list"` (via `<ul>`) | Provides list semantics; `Ul` is the underlying primitive. |
| `MenuItem` | `role="listitem"` + interactive descendant | Each item is a list item; the clickable element inside should be a `<button>` or `<a>`. |
| `SubMenuItem` | `role="listitem"` + interactive descendant | Same pattern as `MenuItem`; supports `aria-label` for override. |
| `CollapseItem` | `<button>` | Toggles sidebar collapsed state; label text changes with state. |
| Badge | `role="status"` or `aria-label` override | Use `badgeAriaLabel` to provide screen-reader text (e.g. `"99 unread notifications"` instead of the visual `"99+"`). |

---

## Keyboard interaction

| Key | Behaviour |
|---|---|
| `Tab` | Moves focus through sidebar items in DOM order. |
| `Shift+Tab` | Moves focus backward. |
| `Enter` / `Space` | Activates the focused `MenuItem`, `SubMenuItem`, or `CollapseItem`. |
| Arrow keys | Not documented by MCP; confirm whether sub-menu expansion uses arrow navigation. |

<!-- STUB:GAP-006 source="Test keyboard behaviour in @8x8/oxygen-sidebar-menu and update accessibility.md with confirmed arrow key handling for sub-menu expansion" -->

---

## Screen reader guidance

- **Navigation landmark**: wrap `SidebarContainer` in a `<nav aria-label="Main navigation">` (or confirm the component renders one internally) so screen reader users can jump directly to the sidebar.
- **Active state**: `isActive` should map to `aria-current="page"` on the active item's interactive element, indicating to screen readers which route is current.
- **Collapsed state**: when `collapsed={true}`, item labels are visually hidden. Ensure they remain available to screen readers (visible to AT, not to sighted users) rather than being removed from the DOM.
- **Badge content**: always supply `badgeAriaLabel` when `badgeChildren` is a truncated count (e.g. `"99+"`). Screen readers should hear `"99 unread notifications"`, not `"99+"`.
- **`aria-label` on `SubMenuItem`**: the example code shows `aria-label="test-label"` passed directly to `SubMenuItem`, confirming the component passes through ARIA attributes. Use this to disambiguate items that share the same visual label across different groups.
- **Collapse toggle**: the `CollapseItem` label must reflect the current state. Pass `label={isSidebarCollapsed ? expandLabel : collapseLabel}` so AT users hear the correct action.

---

## WCAG 2.1 AA checklist

| Criterion | Requirement | Notes |
|---|---|---|
| 1.3.1 Info and Relationships | Navigation structure communicated via semantics | Verify `<nav>` landmark and list structure are rendered. |
| 1.4.1 Use of Color | Active item not indicated by color alone | Confirm active item also uses shape, icon, or text change. |
| 1.4.3 Contrast (Minimum) | Text ≥ 4.5:1, large text ≥ 3:1 | Sidebar uses `ui25` background — verify label colors meet ratio. |
| 2.1.1 Keyboard | All functionality operable by keyboard | Tab/Enter/Space must activate items and the collapse toggle. |
| 2.4.3 Focus Order | Focus order is logical | Items should receive focus in the visual DOM order. |
| 2.4.7 Focus Visible | Focus indicator visible | Verify a visible focus ring is present on `MenuItem`, `SubMenuItem`, and `CollapseItem`. |
| 4.1.2 Name, Role, Value | Interactive elements have accessible name | `label` prop provides the accessible name; badge needs `badgeAriaLabel`; collapse toggle needs an accurate label. |
| 4.1.3 Status Messages | Badge counts announced | Use `badgeAriaLabel` with a live region or via `aria-label` so count changes are announced. |

> **WARN-001:** All ARIA roles above are inferred, not verified from rendered HTML. Verify rendered output in a browser to confirm actual ARIA output before publishing.

_Source: Oxygen MCP · Extracted 2026-05-07_
