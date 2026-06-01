---
parent: "[[AlertBanner]]"
component: AlertBanner
section: usage
role: spoke-usage
source_type: editorial
pipeline_stage: rewritten
audit_verdict: NO
tags:
  - oxygen
  - component/AlertBanner
  - role/spoke/usage
  - stage/rewritten
---

# AlertBanner — Usage

<!-- source: editorial — no Figma "↳ AlertBanner examples" page exists; pairs derived from props, examples, accessibility and figma sources. Replace with figma-extract-usage output when a Figma examples page is created. -->

AlertBanner is a persistent, page-scoped warning strip. It uses a single fixed amber style to signal that a system-level condition requires the user's attention. The banner stays visible until the underlying condition is resolved — it is not dismissable.

## When to use

- A system-level warning affects the user's ability to proceed (session expiry, connectivity loss, scheduled maintenance).
- The condition is persistent — it is not a one-time confirmation or a transient status update.
- The warning applies to the whole page or region, not to a specific field or isolated element.

## When not to use

| Situation | Use instead |
|-----------|-------------|
| Transient confirmation ("File saved", "Settings updated") | [[Toast]] |
| The user should be able to dismiss the notice | [[Toast]] (dismissable) |
| Field-level validation feedback | Inline error / form field error state |
| User must complete an action before continuing and the whole UI is blocked | [[Modal]] / [[Dialog]] |
| Low-urgency informational status update that should not interrupt screen reader flow | Status region / [[Toast]] |

AlertBanner has no built-in dismiss control. If the use case requires dismissal, use [[Toast]].

## Do / Don't

### Pair 1 — Urgency match: use it for warnings, not for gentle notices

**✅ Do — Reserve AlertBanner for time-sensitive, page-level warnings.**
AlertBanner maps to an immediate screen reader announcement (`role="alert"` behaviour). It is the right tool when the condition affects what the user can do right now — for example, a session about to expire or a service outage blocking a core workflow.

**❌ Don't — Use AlertBanner for low-urgency informational updates.**
Announcing "Autosaved 2 minutes ago" or "New features available" as an alert will interrupt screen reader users at the wrong moment. Use a polite status region or Toast for information that does not require immediate action.

### Pair 2 — Single severity: use the amber style as intended

**✅ Do — Use AlertBanner only for warning-level conditions.**
The amber background is intentional and fixed. It signals "warning" system-wide. Using it only for that purpose preserves its meaning across the product.

**❌ Don't — Repurpose AlertBanner for success, info, or error states by overriding its colour.**
There is no `severity` or `variant` prop. Applying custom CSS to change the background breaks the design system contract and produces an untokenised one-off. If your use case needs multiple severities, raise a request with the design system team.

### Pair 3 — Action button labelling: make the label meaningful out of context

**✅ Do — Label the action button with a specific, self-contained verb phrase.**
"Retry", "Reconnect", "Sign in again", "Contact support" — each label tells the user exactly what will happen when activated, even when read in isolation by a screen reader.

**❌ Don't — Use generic labels like "Click here", "OK", or "More".**
Generic labels fail screen reader users who navigate by button. They also waste the action button's value for sighted users — the button is the clearest signal of what to do next, and a vague label squanders that.

### Pair 4 — Message copy: write for the user, not for the error log

**✅ Do — Write short, user-actionable copy that names the issue and the next step.**
"Your session has expired. Sign in again to continue." One sentence, two things: what happened and what to do. Keep `children` to plain text or simple inline elements.

**❌ Don't — Paste raw error messages, status codes, or stack traces into the banner.**
Technical error strings are rarely actionable for end users and create noise for screen readers. If diagnostic information needs to be surfaced, link to a details view via the action button rather than embedding it in the banner message.

<!-- STUB:GAP-015 source="Replace these editorial Do/Don't pairs with figma-extract-usage output once a Figma '↳ AlertBanner examples' page is created. Pairs are currently authored from extracted artifacts." -->
