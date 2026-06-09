<!-- SKILL: usage-advisor -->
<!-- COMPONENT: Toast -->
<!-- DRAFTED: 2026-05-15 -->
<!-- PROMOTED: 2026-05-15 -->
<!-- MODE: open (autonomous — designer review pending) -->
<!-- GROUNDING: full -->
<!-- SOURCE: editorial — no Figma "↳ Toast examples" page exists -->
<!-- FIGMA EXAMPLES PAGE: absent — figma-extract-usage cannot run for this component -->
<!-- STATUS: editorial guidance — replace Do/Don't pairs with figma-extract-usage output when a Figma examples page is created -->
---
component: Toast
package: "@8x8/oxygen-toast"
category: feedback_status
role: usage
role_description: "Usage guidelines — editorially authored from extracted artifacts; no Figma examples page exists"
pipeline_stage: spec_ready
pipeline_note: "Usage authored editorially from extracted artifacts — NOT from Figma Do/Don't frames. Replace pairs with figma-extract-usage output when a Figma examples page exists."
source_type: editorial
audit_verdict: null
siblings:
  - "[[Toast/props]]"
  - "[[Toast/examples]]"
  - "[[Toast/tokens]]"
  - "[[Toast/accessibility]]"
  - "[[Toast/Toast-figma]]"
  - "[[Toast/Toast-pui]]"
  - "[[Toast/Toast-audit]]"
tags:
  - oxygen
  - component/Toast
  - role/usage
  - stage/spec_ready
  - category/feedback_status
---
# Toast — Usage Guidelines

> **See also:** [props.md](props.md) · [examples.md](examples.md) · [tokens.md](tokens.md) ·
> [accessibility.md](accessibility.md) · [Toast-figma.md](Toast-figma.md) · [Toast-pui.md](Toast-pui.md)

> **Editorial guidance — not Figma-sourced.** No `↳ Toast examples` Figma page exists, so `figma-extract-usage` cannot run. The Do/Don't pairs below are inferred from `props.md`, `examples.md`, `accessibility.md`, and `Toast-figma.md`. Treat as provisional until a designer reviews them.

Toast is a transient, floating feedback surface anchored to the top corner of the UI below the top bar ([Toast-figma.md:224](Toast-figma.md)). It announces the outcome of an action or a system event without interrupting the user's flow. It is intentionally rendered on an **inverted dark background** so it pops against the main canvas, and it carries five semantic types (`success`, `error`, `warning`, `info`, `loading`) that map to a coloured left indicator bar.

Use Toast for short, ephemeral messages. For persistent page-level warnings, blocking decisions, or inline field-level feedback, see the comparator in **When not to use** below.

---

## Grounding summary

- **Files used:** `props.md`, `examples.md`, `tokens.md`, `accessibility.md`, `Toast-figma.md`, `Toast-pui.md`, `Toast-audit.md`
- **Files missing:** none — full grounding
- **Internal precedent:**
  - [AlertBanner/alert-banner-usage.md:56-58](../AlertBanner/alert-banner-usage.md) — comparator routing (Toast vs AlertBanner vs Modal vs inline error vs status region).
  - [AlertBanner/alert-banner-usage.md:68-80](../AlertBanner/alert-banner-usage.md) — `role="alert"` (immediate) vs `role="status"` (polite) decision discipline.
  - [AlertBanner/alert-banner-usage.md:110-121](../AlertBanner/alert-banner-usage.md) — Pair 4: write user-actionable copy, never paste raw error strings.
  - [Modal/Modal-usage-draft.md:88-98](../Modal/Modal-usage-draft.md) — destructive-action labelling discipline (specific verbs, not "OK"/"Yes").

---

## When to use

- A short, transient status update the user can read and move past (file saved, message sent, copy-to-clipboard succeeded).
- A non-blocking error or warning the user should notice but doesn't have to acknowledge immediately.
- An in-progress signal for a background task that doesn't justify a full inline loader.
- An imperative event dispatched from anywhere in the app via `Toaster` + `notify()` ([examples.md:89-112](examples.md)).

## When not to use

| Situation | Use instead |
|-----------|-------------|
| Persistent page-level warning until the underlying condition is resolved (session expiry, outage) | [AlertBanner](../AlertBanner/alert-banner-usage.md) |
| User must complete an action before continuing and the whole UI is blocked | [Modal](../Modal/Modal-usage-draft.md) (Dialog Modal for confirmations) |
| Field-level validation or inline status next to a specific input | Inline error / form field error state |
| Long-running operation where progress is the primary signal | `ProgressBar` (determinate) or `Spinner` (indeterminate, inline) |
| Static informational status that lives inside a card or section | Inline status badge / `Tag` |
| Non-floating notification inside a layout column | `InlineNotification` (also in `@8x8/oxygen-toast`) |

> The five `type` values are semantic, not stylistic. Don't pick `success` because you like green — pick it because the underlying event was a successful outcome.

---

## Do / Don't

<!-- SCREENSHOTS UNAVAILABLE — no Figma examples page exists for Toast -->

### Pair 1 — Match `role` to urgency: errors announce immediately, everything else announces politely

**Decision:** `type="error"` toasts should use `role="alert"` (assertive); `success`, `warning`, `info`, and `loading` should use `role="status"` (polite). Announcement urgency must match the user's need to know now.

**Grounded in:** [accessibility.md:34](accessibility.md) — *"`"error"` type should use `role="alert"` (assertive); all others use `role="status"` (polite)."* · [accessibility.md:51](accessibility.md).
**Internal precedent:** [AlertBanner/alert-banner-usage.md:68-80](../AlertBanner/alert-banner-usage.md).

#### ✅ Do — Reserve `role="alert"` for `type="error"` and let other types announce politely

> An error toast that interrupts the screen reader is appropriate when the user's last action failed. A success or info toast that does the same is noise — it interrupts whatever the user was reading or doing.

#### ❌ Don't — Promote routine confirmations and info toasts to `role="alert"`

> Announcing "Settings saved" or "3 new messages" assertively trains users to ignore your alerts. Save the assertive channel for things that actually require an immediate response.

---

### Pair 2 — Don't auto-dismiss error or warning toasts

**Decision:** Error and warning toasts must persist until the user acknowledges them. Auto-dismissing them strands screen reader, cognitive-disability, and away-from-screen users.

**Grounded in:** [accessibility.md:54](accessibility.md) — *"Avoid auto-dismissing error or warning toasts — users relying on screen readers or with cognitive disabilities may need extended time."*

#### ✅ Do — Keep error and warning toasts visible until the user dismisses them (or the underlying condition is resolved)

> A warning that vanishes after 5 seconds is invisible to anyone who isn't watching the screen at that moment. Render error and warning toasts with no `DURATION` timeout and a visible close control.

#### ❌ Don't — Apply the same short auto-dismiss timer to error/warning that you use for success

> Success toasts can fade — the action already completed. Errors and warnings carry information the user has to act on, and that information can't disappear before they've read it.

---

### Pair 3 — Don't hide the close control on a toast that also doesn't auto-dismiss

**Decision:** `hideCloseControl` removes the only manual way out. If you use it, you must guarantee an alternative dismissal path — typically a timed auto-dismiss with sufficient duration.

**Grounded in:** [accessibility.md:55](accessibility.md) — *"When using `hideCloseControl`, ensure users have an alternative way to dismiss the toast (e.g. timed auto-dismiss with sufficient duration)."* · [props.md:73](props.md) `hideCloseControl: boolean`.

#### ✅ Do — Reserve `hideCloseControl` for short-lived `type="loading"` toasts that auto-resolve when the operation completes

> A "Saving…" loading toast doesn't need a close button because the toast updates itself the moment the save finishes. The user is never stuck with it.

#### ❌ Don't — Combine `hideCloseControl` with persistent or error/warning toasts

> Hiding the close button on a toast that won't auto-dismiss traps the user — there is no keyboard or pointer route to clear it. This is a hard accessibility failure.

---

### Pair 4 — Always supply `closeButtonLabel` and `iconTitle`

**Decision:** Both props are accessible names for elements that convey meaning. Treat them as mandatory in practice, not optional.

**Grounded in:** [accessibility.md:49-50](accessibility.md) — *"Always provide `closeButtonLabel` — without it the close button has no accessible name. Always provide `iconTitle` when the status icon conveys semantic meaning."* · [props.md:77-78](props.md).

#### ✅ Do — Pass a specific `closeButtonLabel` ("Dismiss save confirmation") and an `iconTitle` that names the status ("Success", "Error", "Warning", "Loading")

> Screen readers announce the toast's icon and its close button by these labels. Specific labels orient users — "Dismiss save confirmation" tells them what they're closing; "Success" tells them what the icon means.

#### ❌ Don't — Ship a toast without these props or use a generic "Close" / "Icon" label

> An unlabelled close button is a button with no name — useless to screen readers. A generic "Close" gives no context when the user is hearing it out of order with other dismiss buttons on the page.

---

### Pair 5 — Pick the right surface: Toast for transient, AlertBanner for persistent, Modal for blocking, InlineNotification for embedded

**Decision:** Toast is one of four feedback surfaces in Oxygen. Each has a different lifespan and scope. Pick by lifespan and disruption, not by which one you saw last.

**Grounded in:** [Toast-figma.md:223-224](Toast-figma.md) — *"appears at the top corner of the UI below the top bar… Incoming interactions go to the top of the stack."* · [accessibility.md:54](accessibility.md) (transience implied by auto-dismiss discussion) · [props.md:55](props.md) (`InlineNotification` is the in-layout sibling).
**Internal precedent:** [AlertBanner/alert-banner-usage.md:56-58](../AlertBanner/alert-banner-usage.md).

#### ✅ Do — Use Toast for ephemeral, app-wide events; reach for AlertBanner / Modal / InlineNotification when the situation demands persistence, blocking, or embedded placement

> A confirmation that "Your changes were saved" is a Toast. A persistent "Your VPN connection dropped — reconnect to continue" is an AlertBanner. "Delete this customer? This cannot be undone." is a Modal. A status badge inline with a settings row is an InlineNotification or Tag.

#### ❌ Don't — Use Toast for content the user must address before continuing, or that must remain visible across navigation

> If dismissal means the user loses the only copy of important information, the surface is wrong. Use AlertBanner (persistent) or Modal (blocking) instead.

---

### Pair 6 — `type="loading"` is for short, deterministic operations announced globally — not for long jobs or inline progress

**Decision:** A loading toast is a global, top-of-screen announcement that something is in flight. It should resolve into a success/error toast quickly. For inline or long-running work, use a `Spinner` or `ProgressBar` instead.

**Grounded in:** [props.md:81](props.md) `"loading"` is a `ToastType` value · [accessibility.md:52](accessibility.md) — *"For `type="loading"`, use `aria-live="polite"` and update the content once the operation completes."*

#### ✅ Do — Use a loading toast for short, fire-and-forget operations whose outcome will replace it within a few seconds

> "Exporting…" → updates to "Export ready. Download" on completion. The user sees one toast, not two; the announcement is polite (`aria-live="polite"`) and resolves quickly.

#### ❌ Don't — Use a loading toast for an operation that takes 30+ seconds or for progress that lives next to a specific element

> Long-running work needs a determinate `ProgressBar` so the user can see how far along it is. Inline operations (form submit, in-card refresh) need an inline `Spinner` near the trigger, not a floating toast detached from context.

---

### Pair 7 — Write user-actionable copy in `title` and `description`; never paste raw error strings or stack traces

**Decision:** `title` is a short user-facing headline; `description` is a single supporting sentence. Both should be plain language. Technical detail belongs behind an action button or in a details view — not in the toast body.

**Grounded in:** [Toast-figma.md:102-104](Toast-figma.md) (default Figma values model short user-facing copy) · [props.md:67-68](props.md) (`title` and `description` accept `ReactNode` but are sized for short text — title is 14px semi-bold, description 14px regular at 320px container width per [Toast-figma.md:60-61, 189](Toast-figma.md)).
**Internal precedent:** [AlertBanner/alert-banner-usage.md:110-121](../AlertBanner/alert-banner-usage.md) (Pair 4).

#### ✅ Do — Write `title` as a short outcome statement and `description` as one helpful supporting sentence

> *Title:* "Couldn't send message." *Description:* "Check your connection and try again." Two short, plain-language strings. If technical detail matters, expose it behind an action button ("View details") rather than inside the toast text.

#### ❌ Don't — Drop raw error codes, stack traces, or JSON payloads into the toast body

> *"Error: ECONNRESET at TCPConnectWrap.afterConnect..."* is noise for end users and a wall of text for screen readers. If diagnostic info needs to surface, link to it from an action button or a log view.

---

## Gaps & open questions

| ID | Type | Description |
|----|------|-------------|
| GAP-USAGE-001 | Editorial | These Do/Don't pairs are authored from extracted artifacts, not from Figma examples frames. They should be reviewed by a designer and replaced with Figma-sourced pairs once a `↳ Toast examples` page is created. |
| GAP-USAGE-002 | Source gap | No accessibility annotations exist on the Notification component set in Figma ([Toast-figma.md:228](Toast-figma.md)). The `role="alert"` / `role="status"` distinction in Pair 1 is inferred from `accessibility.md`; confirm against the component source before shipping. |
| GAP-USAGE-003 | Source gap | The `DURATION` constant from `@8x8/oxygen-toaster` ([props.md:58](props.md)) is referenced but its values are not surfaced by MCP. Pair 2's "sufficient duration" guidance can't yet point to a specific token. |
| CONFLICT-001 (carried from [Toast-figma.md](Toast-figma.md)) | Conflict | Figma's `Style` axis (Full / Group collapsed / Group expanded) has no corresponding prop on `Toast` directly — stacking/grouping is handled by `ToastStack` + `Toaster`. Stacking guidance was deliberately omitted from this draft pending confirmation; revisit when the boundary is settled. |
| GAP-USAGE-004 | Skipped axis | Number-of-actions guidance (zero / one / two) was excluded — it overlaps with action-button labelling rules in `accessibility.md:65-72` (via AlertBanner precedent) and adds little editorial leverage on top of Pair 5. Re-add if a designer wants explicit guidance. |
| GAP-USAGE-005 | Skipped axis | `notify()` vs rendering `<Toast>` directly was excluded as an implementation/architecture pattern more suited to dev docs than editorial usage guidelines. |
| GAP-USAGE-006 | Skipped axis | `size` (small/medium/large) was excluded as mechanical (picked by layout fit, not editorial intent). |

---

## Axes presented but skipped (audit trail)

| Axis | Reason skipped |
|------|----------------|
| Stacking / grouping (`ToastStack`, group collapsed/expanded) | Conflict between Figma `Style` axis and Toast API ([Toast-figma.md](Toast-figma.md)) — needs resolution before editorial guidance. |
| Number of actions (0 / 1 / 2 in `actions` array) | Action-labelling discipline is generic across feedback surfaces — covered by internal precedent (AlertBanner Pair 3). |
| `notify()` vs `<Toast>` directly | Implementation pattern, not editorial. Belongs in dev docs / `examples.md`. |
| `size` (small / medium / large) | Mechanical — picked by layout fit. |
| Mode (Light / Dark) | Not an editorial choice — driven by theme context. |

---

_Source: editorial guidance authored from extracted artifacts (props.md, examples.md, accessibility.md, tokens.md, Toast-figma.md, Toast-pui.md, Toast-audit.md) · No Figma examples page available · 2026-05-15_
