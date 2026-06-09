---
parent: "[[SlideOut]]"
section: accessibility
pipeline_stage: spec_ready
tags:
  - oxygen
  - component/SlideOut
  - role/accessibility
---

<!-- STUB:GAP-009 source="Obtain confirmed accessibility implementation from component source, Storybook a11y addon output, or engineering. Replace inferred guidance below with deterministic data — in particular: whether SlideOut itself applies aria-hidden when not visible, whether it traps focus in dialog mode, and whether the resize handle is keyboard-accessible." -->

> **All accessibility guidance below is inferred** from the component's panel/drawer nature and WCAG 2.1 AA requirements. The Oxygen MCP returned no explicit accessibility documentation for SlideOut.

## ARIA roles and attributes

| Attribute | Recommended value | Notes |
|---|---|---|
| `role` | `complementary` or `dialog` | Use `dialog` when the panel requires user interaction before dismissal; `complementary` when it is informational/supplemental |
| `aria-label` or `aria-labelledby` | Descriptive panel title | Required when `role="dialog"` |
| `aria-hidden` | `"true"` when `isVisible={false}` | Hides the panel from the accessibility tree when not visible |
| `aria-expanded` | On the trigger element | The toggle button (outside SlideOut) should reflect the current open/closed state |

## Keyboard interactions

| Key | Behaviour |
|---|---|
| `Tab` | Moves focus through interactive elements inside the panel when visible |
| `Shift + Tab` | Moves focus in reverse |
| `Escape` | Should close the panel — **must be implemented by the consuming application** via `isVisible` state |

> Focus management is the consuming application's responsibility. When the panel opens, focus should be programmatically moved to the first interactive element inside it. When it closes, focus should return to the trigger element.

## Screen reader guidance

- The panel content is rendered in the DOM regardless of `isVisible`; ensure `aria-hidden` toggling is applied so screen readers do not announce hidden panel content.
- The trigger button label should clearly indicate the action (e.g., "Open details panel", not "Toggle").
- If the panel is resizable, the drag handle should have an accessible label (e.g., `aria-label="Resize panel"`) and should be keyboard-operable.

## WCAG 2.1 AA checklist

| Criterion | SC | Status |
|---|---|---|
| Keyboard accessible | 2.1.1 | Must verify — panel and resize handle need keyboard support |
| No keyboard trap | 2.1.2 | Focus must not be trapped inside the panel when dismissed |
| Focus visible | 2.4.7 | All interactive elements inside panel must have visible focus indicators |
| Name, role, value | 4.1.2 | Panel container and trigger must have appropriate ARIA roles and labels |
| Reflow | 1.4.10 | Panel with `minWidth`/`maxWidth` constraints must not cause horizontal scroll at 320 CSS px |
| Non-text contrast | 1.4.11 | Resize handle (if present) must meet 3:1 contrast against adjacent colours |
