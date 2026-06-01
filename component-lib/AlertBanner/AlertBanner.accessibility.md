---
parent: "[[AlertBanner]]"
component: AlertBanner
section: accessibility
role: spoke-accessibility
pipeline_stage: rewritten
audit_verdict: NO
tags:
  - oxygen
  - component/AlertBanner
  - role/spoke/accessibility
  - stage/rewritten
---

# AlertBanner — Accessibility

## ARIA role

The AlertBanner is a passive notification component. Recommended role:

| Scenario | Role | Rationale |
|----------|------|-----------|
| Time-sensitive, must be announced immediately (errors, warnings) | `role="alert"` | Announces to screen readers automatically on mount |
| Informational, low urgency | `role="status"` | Polite announcement; does not interrupt the user |

The Oxygen component does not expose a `role` prop. The internal implementation likely uses a hardcoded role.

<!-- STUB:GAP-013 source="Inspect component source code (@8x8/oxygen-alert-banner) to confirm the implemented ARIA role. Update this section with the authoritative role." -->

## Icon accessibility

The component exposes an `iconAriaLabel` prop for the warning icon.

| Situation | Recommended value |
|-----------|------------------|
| Icon adds context not in `children` (e.g. severity level) | `"Warning"` or a descriptive phrase |
| `children` already fully describes the alert | `""` (empty) or omit — hides icon from AT |

## Action button

When `actionText` and `actionCallback` are provided, the button must:

- Be reachable via keyboard (`Tab`)
- Be activatable with `Enter` and `Space`
- Have a label that is meaningful out of context (avoid generic labels like "Click here")
- Remain focusable even when the banner is in a visually prominent position

## Focus management

| Scenario | Recommendation |
|----------|----------------|
| Banner appears on page load / static | No programmatic focus shift needed |
| Banner is injected dynamically (e.g. after an action) | Move focus to the banner element, or ensure `role="alert"` triggers an announcement |

## Colour contrast

Text and icon tokens were confirmed in [[AlertBanner.tokens]] — both resolve to dark values (`#26252a` / `#292929`) on the fixed amber background (`#f8ae1a`) in both modes.

| Combination | Hex pair | Minimum ratio | Status |
|-------------|----------|--------------|--------|
| `text/textColor07` on `warning/warning01` (light mode) | `#26252a` on `#f8ae1a` | 4.5 : 1 (normal text) | Verify with contrast checker |
| `text/textColor07` on `warning/warning01` (dark mode) | `#292929` on `#f8ae1a` | 4.5 : 1 (normal text) | Verify with contrast checker |
| `icon/icon08` on `warning/warning01` | same as text | 3 : 1 (non-text) | Verify |

<!-- STUB:GAP-014 source="Calculate exact contrast ratios for text-on-amber and icon-on-amber using the confirmed hex pairs. Update WCAG checklist statuses below." -->

## WCAG 2.1 AA checklist

| Criterion | Applies | Status | Notes |
|-----------|---------|--------|-------|
| 1.4.3 Contrast (Minimum) | Yes | ⚠ Unverified | Hex pairs known (see above) — needs ratio calculation |
| 1.4.11 Non-text Contrast | Yes | ⚠ Unverified | Icon `icon/icon08` on `warning/warning01` |
| 2.1.1 Keyboard | Yes | ⚠ Unverified | Action button must be keyboard operable |
| 2.4.3 Focus Order | Yes | ⚠ Unverified | Confirm focus order when banner is dynamic |
| 4.1.2 Name, Role, Value | Yes | ⚠ Unverified | Confirm `role` implementation; `iconAriaLabel` prop available |
| 4.1.3 Status Messages | Yes | ⚠ Unverified | Confirm `role="alert"` or `role="status"` |

## Screen reader behaviour (inferred)

- The banner container should announce its content to screen readers on mount.
- The warning icon, if given an `iconAriaLabel`, will be announced before the message text.
- The action button, if present, should be announced with its label and role.
- Hidden elements (if any) should use `aria-hidden="true"` or be removed from the DOM.
