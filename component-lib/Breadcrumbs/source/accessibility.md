---
component: Breadcrumbs
package: "@8x8/oxygen-breadcrumbs"
category: navigation
role: accessibility
role_description: "Accessibility — ARIA roles, keyboard interactions, and WCAG 2.1 AA guidance"
pipeline_stage: spec_ready
pipeline_note: "Audit verdict YES/PARTIAL — doc-rewrite can run"
audit_verdict: YES
siblings:
  - "[[Breadcrumbs/props]]"
  - "[[Breadcrumbs/examples]]"
  - "[[Breadcrumbs/tokens]]"
  - "[[Breadcrumbs/Breadcrumbs-figma]]"
  - "[[Breadcrumbs/Breadcrumbs-usage]]"
  - "[[Breadcrumbs/Breadcrumbs-pui]]"
  - "[[Breadcrumbs/Breadcrumbs-audit]]"
tags:
  - oxygen
  - component/Breadcrumbs
  - role/accessibility
  - stage/spec_ready
  - category/navigation
---
# Breadcrumbs — Accessibility

> **See also:** [props.md](props.md) | [examples.md](examples.md) | [tokens.md](tokens.md) | [Breadcrumbs-figma.md](Breadcrumbs-figma.md) | [Breadcrumbs-usage.md](Breadcrumbs-usage.md)

## ARIA roles and structure

| Element | Role / Attribute | Notes |
|---------|-----------------|-------|
| Root wrapper | `<nav>` with `aria-label` | Label is set via the `ariaLabel` prop (default `'Breadcrumbs'`). |
| Ordered list | `<ol>` | Semantic list conveys the trail as an ordered sequence to screen readers. |
| Breadcrumb link | `<a>` | Standard anchor; receives focus in tab order. |
| Active (current) item | `aria-current="page"` | Applied to the last, non-link item to indicate the current page. |
| Collapsed ellipsis button | `<button>` with `title` | `title` is set via `collapsedTitle` prop (default `'Show all links'`). Keyboard-activatable. |

## Keyboard interactions

| Key | Behaviour |
|-----|-----------|
| `Tab` | Moves focus to each breadcrumb link in order; skips the active (non-link) item. |
| `Shift+Tab` | Moves focus backwards through breadcrumb links. |
| `Enter` / `Space` | Activates a focused breadcrumb link or the collapsed-items button. |

## Screen reader guidance

- The `<nav>` landmark with `aria-label="Breadcrumbs"` (or a custom label) lets users jump to breadcrumb navigation via landmark navigation.
- `aria-current="page"` on the active item tells screen reader users they are on the current page without visual inspection.
- When items are collapsed, the ellipsis button should have a meaningful `title`; override `collapsedTitle` when localising or when the default `'Show all links'` is ambiguous in context.
- The separator (default `/`) is decorative. Ensure it is marked `aria-hidden` or excluded from the accessibility tree — this is expected to be handled internally by the component.

## WCAG 2.1 AA checklist

| Criterion | Status | Notes |
|-----------|--------|-------|
| 1.3.1 Info and Relationships | ✓ | `<nav>` + `<ol>` provide semantic structure. |
| 1.4.3 Contrast (Minimum) | Unverified | Link and separator colours depend on theme tokens; verify against design. |
| 2.1.1 Keyboard | ✓ | All links and the collapse button are keyboard-operable. |
| 2.4.3 Focus Order | ✓ | Tab order follows the visual left-to-right trail. |
| 2.4.4 Link Purpose (In Context) | Depends on usage | Breadcrumb link labels should clearly reflect the destination page. |
| 2.4.7 Focus Visible | Unverified | Focus state is documented in design (Focus state listed); verify focus ring meets contrast. |
| 2.4.8 Location | ✓ | Breadcrumbs are a standard location indicator within a site hierarchy. |
| 4.1.2 Name, Role, Value | ✓ | `ariaLabel` on `<nav>`, `aria-current` on active item, `title` on ellipsis button. |

_Source: Oxygen MCP · Extracted 2026-04-30_
