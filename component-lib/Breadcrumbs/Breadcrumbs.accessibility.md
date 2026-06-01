---
parent: "[[Breadcrumbs]]"
section: accessibility
---

<!-- SKIP:WARN-001 manual="Verify ARIA roles against the rendered DOM of @8x8/oxygen-breadcrumbs before shipping docs." -->
> **ARIA roles inferred, not DOM-verified (WARN-001):** The roles below are inferred from the component's expected behaviour and the WAI-ARIA breadcrumb pattern — not confirmed from the rendered DOM. If the implementation uses `div`s without explicit roles, screen readers will not announce the breadcrumb pattern correctly. Verify against rendered output.

## ARIA roles and structure

| Element | Role / Attribute | Notes |
|---------|-----------------|-------|
| Root wrapper | `<nav>` with `aria-label` | Label set via the `ariaLabel` prop (default `'Breadcrumbs'`). |
| Ordered list | `<ol>` | Semantic list conveys the trail as an ordered sequence. |
| Breadcrumb link | `<a>` | Standard anchor; receives focus in tab order. |
| Active (current) item | `aria-current="page"` | Applied to the last, non-link item to indicate the current page. |
| Collapsed ellipsis button | `<button>` with `title` | `title` set via `collapsedTitle` (default `'Show all links'`). Keyboard-activatable. |

## Keyboard interactions

| Key | Behaviour |
|-----|-----------|
| `Tab` | Moves focus to each breadcrumb link in order; skips the active (non-link) item. |
| `Shift+Tab` | Moves focus backwards through breadcrumb links. |
| `Enter` / `Space` | Activates a focused breadcrumb link or the collapsed-items button. |

## Screen reader guidance

- The `<nav>` landmark with `aria-label` lets users jump to breadcrumb navigation via landmark navigation.
- `aria-current="page"` on the active item tells screen-reader users they are on the current page.
- When items are collapsed, the ellipsis `<button>` should have a meaningful `title`; override `collapsedTitle` when localising or when the default is ambiguous.
- The separator (default `/`) is decorative — expected to be marked `aria-hidden` / excluded from the accessibility tree by the component.

## WCAG 2.1 AA checklist

| Criterion | Status | Notes |
|-----------|--------|-------|
| 1.3.1 Info and Relationships | ✓ | `<nav>` + `<ol>` provide semantic structure. |
| 1.4.3 Contrast (Minimum) | Unverified | Link/separator colours depend on tokens; verify against design (WARN-002). |
| 2.1.1 Keyboard | ✓ | All links and the collapse button are keyboard-operable. |
| 2.4.3 Focus Order | ✓ | Tab order follows the visual left-to-right trail. |
| 2.4.4 Link Purpose (In Context) | Depends on usage | Link labels should clearly reflect the destination page. |
| 2.4.7 Focus Visible | Unverified | Focus ring token unresolved (GAP-003); contrast cannot be confirmed (WARN-002). |
| 2.4.8 Location | ✓ | Breadcrumbs are a standard location indicator within a site hierarchy. |
| 4.1.2 Name, Role, Value | ✓ | `ariaLabel` on `<nav>`, `aria-current` on active item, `title` on ellipsis button. |

<!-- SKIP:WARN-002 manual="Verify WCAG 1.4.3 contrast (--actions/action08 #0056e0 on white likely meets AA but unconfirmed) and 2.4.7 focus-visible once hover/focus tokens are resolved (GAP-003)." -->

<!-- STUB:GAP-006 source="Request the Figma component owner to add accessibility annotations (ARIA role, focus order, keyboard behaviour) to node 21927:40413." -->
> **No Figma a11y annotations (GAP-006):** The Figma component carries no accessibility annotations — ARIA role, focus order, and keyboard interaction notes are all absent in the design source. The guidance above is derived from the WAI-ARIA breadcrumb pattern, not from Figma annotations.

_Source: [[Breadcrumbs/accessibility]] · Oxygen MCP · Extracted 2026-04-30_
