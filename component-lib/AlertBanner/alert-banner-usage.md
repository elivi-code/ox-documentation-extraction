---
component: AlertBanner
package: "@8x8/oxygen-alert-banner"
category: feedback_status
role: usage
role_description: "Usage guidelines — editorially authored from extracted artifacts; no Figma examples page exists"
pipeline_stage: extracted
pipeline_note: "Usage extracted (editorial); audit not yet re-run"
audit_verdict: null
siblings:
  - "[[AlertBanner/props]]"
  - "[[AlertBanner/examples]]"
  - "[[AlertBanner/tokens]]"
  - "[[AlertBanner/accessibility]]"
  - "[[AlertBanner/alert-banner-figma]]"
  - "[[AlertBanner/alert-banner-audit]]"
tags:
  - oxygen
  - component/AlertBanner
  - role/usage
  - stage/extracted
  - category/feedback_status
---
<!-- SOURCE: editorial — no Figma "↳ AlertBanner examples" page exists -->
<!-- FIGMA EXAMPLES PAGE: absent — figma-extract-usage cannot run for this component -->
<!-- GROUNDING: full — props.md, examples.md, alert-banner-figma.md, accessibility.md, tokens.md, alert-banner-audit.md -->
<!-- DRAFTED: 2026-05-11 -->
<!-- MODE: open -->
<!-- PAIRS: 4 -->
<!-- STATUS: editorial draft — replace with figma-extract-usage output when a Figma examples page is created -->

# Alert Banner — Usage Guidelines

> **See also:** [props.md](./props.md) · [examples.md](./examples.md) · [tokens.md](./tokens.md) ·
> [accessibility.md](./accessibility.md) · [alert-banner-figma.md](./alert-banner-figma.md)

AlertBanner is a persistent, page-scoped warning strip. It uses a single fixed amber style to signal that a system-level condition requires the user's attention. The banner stays visible until the underlying condition is resolved — it is not dismissable.

---

## When to use

- A system-level warning affects the user's ability to proceed (session expiry, connectivity loss, scheduled maintenance).
- The condition is persistent — it is not a one-time confirmation or a transient status update.
- The warning applies to the whole page or region, not to a specific field or isolated element.

## When not to use

| Situation | Use instead |
|-----------|-------------|
| Transient confirmation ("File saved", "Settings updated") | Toast |
| The user should be able to dismiss the notice | Toast (dismissable) |
| Field-level validation feedback | Inline error / form field error state |
| User must complete an action before continuing and the whole UI is blocked | Modal / Dialog |
| Low-urgency informational status update that should not interrupt screen reader flow | Status region / Toast |

> AlertBanner has no built-in dismiss control. If the use case requires dismissal, use Toast.

---

## Do / Don't

<!-- SCREENSHOTS UNAVAILABLE — no Figma examples page exists for AlertBanner -->

### Pair 1 — Urgency match: use it for warnings, not for gentle notices

#### ✅ Do — Reserve AlertBanner for time-sensitive, page-level warnings

> AlertBanner maps to an immediate screen reader announcement (`role="alert"` behaviour). It is the right tool when the condition affects what the user can do right now — for example, a session about to expire or a service outage blocking a core workflow.

**Grounded in:** `accessibility.md` lines 40–51 — explicit `role="alert"` (immediate announcement) vs `role="status"` (polite) decision table.

#### ❌ Don't — Use AlertBanner for low-urgency informational updates

> Announcing "Autosaved 2 minutes ago" or "New features available" as an alert will interrupt screen reader users at the wrong moment. Use a polite status region or Toast for information that does not require immediate action.

---

### Pair 2 — Single severity: use the amber style as intended

#### ✅ Do — Use AlertBanner only for warning-level conditions

> The amber background is intentional and fixed. It signals "warning" system-wide. Using it only for that purpose preserves its meaning across the product.

**Grounded in:** `props.md` lines 102–107 — "The current Oxygen API does not expose a `type`, `variant`, or `severity` prop. The component renders with a single fixed amber/warning style."

#### ❌ Don't — Repurpose AlertBanner for success, info, or error states by overriding its colour

> There is no `severity` or `variant` prop. Applying custom CSS to change the background to green, red, or blue breaks the design system contract and produces an untokenised one-off. If your use case needs multiple severities, raise a request with the design system team.

---

### Pair 3 — Action button labelling: make the label meaningful out of context

#### ✅ Do — Label the action button with a specific, self-contained verb phrase

> "Retry", "Reconnect", "Sign in again", "Contact support" — each label tells the user exactly what will happen when they activate it, even when read in isolation by a screen reader.

**Grounded in:** `accessibility.md` lines 66–72 — "Have a label that is meaningful out of context (avoid generic labels like 'Click here')." `examples.md` models this with "Retry" and "Contact support".

#### ❌ Don't — Use generic labels like "Click here", "OK", or "More"

> Generic labels fail screen reader users who navigate by button. They also waste the action button's value for sighted users — the button is the clearest signal of what to do next, and a vague label squanders that.

---

### Pair 4 — Message copy: write for the user, not for the error log

#### ✅ Do — Write short, user-actionable copy that names the issue and the next step

> "Your session has expired. Sign in again to continue." One sentence, two things: what happened and what to do. Keep `children` to plain text or simple inline elements.

**Grounded in:** `props.md` lines 86–89 — "`children`… is typically a plain text string or a fragment with inline elements. Avoid complex interactive content inside the banner message." `examples.md` models this pattern throughout.

#### ❌ Don't — Paste raw error messages, status codes, or stack traces into the banner

> Technical error strings are rarely actionable for end users and create noise for screen readers. If diagnostic information needs to be surfaced, link to a details view via the action button rather than embedding it in the banner message.

---

## Gaps & open questions

| ID | Type | Description |
|----|------|-------------|
| CONFLICT-001 | Conflict | `mode` (light/dark) and `breakpoint` (> 576 / < 576) are Figma variant axes with no corresponding props in the Oxygen API. Confirm whether the component reads from a theme context, a container query, or viewport width automatically. |
| CONFLICT-002 | Conflict | Banner background token identity is unresolved. Figma extraction confirms `warning/warning01` → `color/yellow/yellow06` → `#f8ae1a` (mode-invariant); `tokens.md` notes the `alertYellow` token is documented as data-viz scope. Design team must confirm the correct semantic token name before `doc-rewrite` runs. |
| GAP-013 | Source gap | ARIA role implementation is unconfirmed. `accessibility.md` recommends `role="alert"`, but the component source has not been verified. Usage Pair 1 above is grounded in that recommendation — confirm before using this guidance in shipped documentation. |
| — | Editorial | These Do/Don't pairs are authored from extracted artifacts, not from Figma examples frames. They should be reviewed by a designer and replaced with Figma-sourced pairs once a `↳ AlertBanner examples` page is created. |

---

_Source: editorial guidance authored from extracted artifacts (props.md, examples.md, alert-banner-figma.md, accessibility.md, alert-banner-audit.md) · No Figma examples page available · 2026-05-11_
