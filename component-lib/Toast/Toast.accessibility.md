---
component: Toast
parent: "[[Toast]]"
section: accessibility
role: spoke
pipeline_stage: spec_ready
audit_verdict: partial
siblings:
  - "[[Toast.props]]"
  - "[[Toast.anatomy]]"
  - "[[Toast.tokens]]"
  - "[[Toast.usage]]"
  - "[[Toast.platform]]"
  - "[[Toast.composition]]"
tags:
  - oxygen
  - component/Toast
  - role/spoke
  - stage/spec_ready
---

<!-- STUB:GAP-002 source="All accessibility content is inferred — MCP returned no explicit ARIA role, keyboard interaction, or live-region data for Toast. Obtain confirmed ARIA implementation from @8x8/oxygen-toast source code or Storybook a11y addon output. Replace inferred content with deterministic data." -->

> **Inferred content.** No explicit ARIA role or keyboard data was returned by the MCP for this component. The following is derived from the component's nature as a transient feedback/notification component and from standard ARIA patterns. Confirm against @8x8/oxygen-toast source or Storybook a11y addon before shipping.

---

## ARIA roles and attributes

| Element | Role / Attribute | Notes |
|---------|-----------------|-------|
| Toast container | `role="status"` or `role="alert"` | `type="error"` should use `role="alert"` (assertive); all others use `role="status"` (polite) |
| Close button | `aria-label` | Provided via `closeButtonLabel` prop — always supply this |
| Status icon | `aria-label` | Provided via `iconTitle` prop — always supply when the icon conveys meaning |
| Action buttons | standard button semantics | Labels should be descriptive and self-contained |

---

## Keyboard interactions

| Key | Action |
|-----|--------|
| `Tab` | Moves focus to the close button (when visible) and action buttons |
| `Enter` / `Space` | Activates the focused close button or action button |
| `Escape` | May dismiss the toast (implementation-dependent) |

---

## Screen reader guidance

- Always provide `closeButtonLabel` — without it the close button has no accessible name.
- Always provide `iconTitle` when the status icon conveys semantic meaning (success, error, warning, info).
- For `type="error"`, prefer `role="alert"` so the toast is announced immediately and assertively.
- For `type="loading"`, use `aria-live="polite"` and update the content once the operation completes.
- The `Toaster` portal component should ensure its container has an appropriate `aria-live` region so dynamically injected toasts are announced.
- Avoid auto-dismissing error or warning toasts — users relying on screen readers or with cognitive disabilities may need extended time.
- When using `hideCloseControl`, ensure users have an alternative way to dismiss the toast (e.g. timed auto-dismiss with sufficient duration).

---

## WCAG 2.1 AA checklist

| Criterion | Status | Notes |
|-----------|--------|-------|
| 1.3.1 Info and Relationships | ✅ | Status semantics conveyed via `iconTitle` and role |
| 1.4.1 Use of Color | ✅ | Type is conveyed by icon + text, not color alone |
| 1.4.3 Contrast (Minimum) | ⚠️ | Verify token values meet 4.5:1 for text, 3:1 for large text |
| 2.1.1 Keyboard | ✅ | Close button and actions are keyboard-accessible |
| 2.4.3 Focus Order | ✅ | Close button should receive focus when toast appears |
| 2.5.3 Label in Name | ✅ | `closeButtonLabel` and `iconTitle` must match visible labels |
| 4.1.2 Name, Role, Value | ✅ | Use `closeButtonLabel` and `iconTitle` props consistently |
| 4.1.3 Status Messages | ✅ | Use `role="status"` / `role="alert"` appropriate to urgency |
