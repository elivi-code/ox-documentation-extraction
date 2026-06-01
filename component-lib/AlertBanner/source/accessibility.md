---
component: AlertBanner
package: "@8x8/oxygen-alertBanner"
category: feedback_status
role: accessibility
role_description: "Accessibility — ARIA roles, keyboard interactions, and WCAG 2.1 AA guidance"
pipeline_stage: blocked
pipeline_note: "Audit verdict NO — resolve CONFLICTs before rewrite"
audit_verdict: NO
siblings:
  - "[[AlertBanner/props]]"
  - "[[AlertBanner/examples]]"
  - "[[AlertBanner/tokens]]"
  - "[[AlertBanner/alert-banner-figma]]"
  - "[[AlertBanner/alert-banner-audit]]"
tags:
  - oxygen
  - component/AlertBanner
  - role/accessibility
  - stage/blocked
  - category/feedback_status
---
# AlertBanner — Accessibility

> **See also:** [alert-banner-figma.md](./alert-banner-figma.md) · [props.md](./props.md) ·
> [tokens.md](./tokens.md) · [examples.md](./examples.md) ·
> [alert-banner-usage.md](./alert-banner-usage.md)

---

## Source note

No accessibility annotations were found in the Figma file. The guidance below is
inferred from the component's nature (passive informational banner) and the props
exposed by the Oxygen API. Verify all items with the 8x8 accessibility team before
shipping.

---

## ARIA role

The AlertBanner is a passive notification component. Recommended role:

| Scenario | Role | Rationale |
|----------|------|-----------|
| Time-sensitive, must be announced immediately (errors, warnings) | `role="alert"` | Announces to screen readers automatically on mount |
| Informational, low urgency | `role="status"` | Polite announcement; does not interrupt the user |

> The Oxygen component does not expose a `role` prop in the current API. If the internal
> implementation uses a hardcoded role, confirm which one with the component source or
> the design system team.

---

## Icon accessibility

The component exposes an `iconAriaLabel` prop for the warning icon.

| Situation | Recommended value |
|-----------|------------------|
| Icon adds context not in `children` (e.g. severity level) | `"Warning"` or a descriptive phrase |
| `children` already fully describes the alert | `""` (empty) or omit — hides icon from AT |

---

## Action button

When `actionText` and `actionCallback` are provided, the button must:

- Be reachable via keyboard (`Tab`)
- Be activatable with `Enter` and `Space`
- Have a label that is meaningful out of context (avoid generic labels like "Click here")
- Remain focusable even when the banner is in a visually prominent position

---

## Focus management

| Scenario | Recommendation |
|----------|----------------|
| Banner appears on page load / static | No programmatic focus shift needed |
| Banner is injected dynamically (e.g. after an action) | Move focus to the banner element, or ensure `role="alert"` triggers an announcement |

---

## Colour contrast

The amber background (`#F8AE1A`) on white text or dark text must meet WCAG 2.1 AA:

| Combination | Minimum ratio | Status |
|-------------|--------------|--------|
| Dark text on `#F8AE1A` background | 4.5 : 1 (normal text) | Verify — `#F8AE1A` is a medium-luminance amber |
| White text on `#F8AE1A` background | 4.5 : 1 (normal text) | Likely failing — confirm with contrast checker |
| Dark-mode variant | verify separately | Text/icon colours not extracted — needs design clarification |

> Text and icon colours inside the component were not returned by the Figma API.
> Confirm contrast ratios once inner layer tokens are confirmed.

---

## WCAG 2.1 AA checklist

| Criterion | Applies | Status | Notes |
|-----------|---------|--------|-------|
| 1.4.3 Contrast (Minimum) | Yes | ⚠ Unverified | Text colour not extracted from Figma |
| 1.4.11 Non-text Contrast | Yes | ⚠ Unverified | Icon colour not extracted |
| 2.1.1 Keyboard | Yes | ⚠ Unverified | Action button must be keyboard operable |
| 2.4.3 Focus Order | Yes | ⚠ Unverified | Confirm focus order when banner is dynamic |
| 4.1.2 Name, Role, Value | Yes | ⚠ Unverified | Confirm `role` implementation in source; `iconAriaLabel` prop available |
| 4.1.3 Status Messages | Yes | ⚠ Unverified | Confirm `role="alert"` or `role="status"` |

---

## Screen reader behaviour (inferred)

- The banner container should announce its content to screen readers on mount.
- The warning icon, if given an `iconAriaLabel`, will be announced before the message text.
- The action button, if present, should be announced with its label and role.
- Hidden elements (if any) should use `aria-hidden="true"` or be removed from the DOM.

---

_Source: Oxygen MCP · Figma annotations (none found) · Inferred from component nature · Extracted 2026-04-28_
