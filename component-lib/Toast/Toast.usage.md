---
component: Toast
parent: "[[Toast]]"
section: usage
role: spoke
pipeline_stage: spec_ready
audit_verdict: partial
siblings:
  - "[[Toast.props]]"
  - "[[Toast.anatomy]]"
  - "[[Toast.tokens]]"
  - "[[Toast.accessibility]]"
  - "[[Toast.platform]]"
  - "[[Toast.composition]]"
tags:
  - oxygen
  - component/Toast
  - role/spoke
  - stage/spec_ready
---

> **Editorial guidance — not Figma-sourced.** No `↳ Toast examples` Figma page exists, so `figma-extract-usage` cannot run. The Do/Don't pairs below are authored from `props.md`, `examples.md`, `accessibility.md`, `tokens.md`, and `Toast-figma.md`. Treat as provisional until a designer reviews. Replace pairs with `figma-extract-usage` output when a Figma examples page is created.

Toast is a transient, floating feedback surface anchored to the top corner of the UI below the top bar. It announces the outcome of an action or a system event without interrupting the user's flow. It is intentionally rendered on an **inverted dark background** so it pops against the main canvas, and it carries five semantic types (`success`, `error`, `warning`, `info`, `loading`) that map to a coloured left indicator bar.

---

## When to use

- A short, transient status update the user can read and move past (file saved, message sent, copy-to-clipboard succeeded).
- A non-blocking error or warning the user should notice but doesn't have to acknowledge immediately.
- An in-progress signal for a background task that doesn't justify a full inline loader.
- An imperative event dispatched from anywhere in the app via `Toaster` + `notify()`.

## When not to use

| Situation | Use instead |
|-----------|-------------|
| Persistent page-level warning until the underlying condition resolves (session expiry, outage) | `[[AlertBanner]]` |
| User must complete an action before continuing and the whole UI is blocked | `[[Modal]]` (Dialog Modal for confirmations) |
| Field-level validation or inline status next to a specific input | Inline error / form field error state |
| Long-running operation where progress is the primary signal | `[[ProgressBar]]` (determinate) or `[[Spinner]]` (indeterminate, inline) |
| Static informational status inside a card or section | Inline status badge / `[[Tag]]` |
| Non-floating notification inside a layout column | `InlineNotification` (also in `@8x8/oxygen-toast`) |

> The five `type` values are semantic, not stylistic. Don't pick `success` because you like green — pick it because the underlying event was a successful outcome.

---

## Do / Don't

### Pair 1 — Match `role` to urgency: errors announce immediately, everything else announces politely

**Decision:** `type="error"` toasts should use `role="alert"` (assertive); `success`, `warning`, `info`, and `loading` should use `role="status"` (polite). Announcement urgency must match the user's need to know now.

**Grounded in:** `accessibility.md` — *"`error` type should use `role="alert"` (assertive); all others use `role="status"` (polite)."*

#### ✅ Do — Reserve `role="alert"` for `type="error"` and let other types announce politely

> An error toast that interrupts the screen reader is appropriate when the user's last action failed. A success or info toast that does the same is noise — it interrupts whatever the user was reading or doing.

#### ❌ Don't — Promote routine confirmations and info toasts to `role="alert"`

> Announcing "Settings saved" or "3 new messages" assertively trains users to ignore your alerts. Save the assertive channel for things that actually require an immediate response.

---

### Pair 2 — Don't auto-dismiss error or warning toasts

**Decision:** Error and warning toasts must persist until the user acknowledges them. Auto-dismissing them strands screen reader, cognitive-disability, and away-from-screen users.

**Grounded in:** `accessibility.md` — *"Avoid auto-dismissing error or warning toasts — users relying on screen readers or with cognitive disabilities may need extended time."*

#### ✅ Do — Keep error and warning toasts visible until the user dismisses them (or the underlying condition resolves)

> Render error and warning toasts with no `DURATION` timeout and a visible close control.

#### ❌ Don't — Apply the same short auto-dismiss timer to error/warning that you use for success

> Success toasts can fade — the action already completed. Errors and warnings carry information the user has to act on, and that information can't disappear before they've read it.

---

### Pair 3 — Don't hide the close control on a toast that also doesn't auto-dismiss

**Decision:** `hideCloseControl` removes the only manual way out. If you use it, guarantee an alternative dismissal path — typically a timed auto-dismiss with sufficient duration.

**Grounded in:** `accessibility.md` — *"When using `hideCloseControl`, ensure users have an alternative way to dismiss the toast."* · `props.md` — `hideCloseControl: boolean`.

#### ✅ Do — Reserve `hideCloseControl` for short-lived `type="loading"` toasts that auto-resolve when the operation completes

> A "Saving…" loading toast doesn't need a close button because the toast updates itself the moment the save finishes.

#### ❌ Don't — Combine `hideCloseControl` with persistent or error/warning toasts

> Hiding the close button on a toast that won't auto-dismiss traps the user — there is no keyboard or pointer route to clear it. This is a hard accessibility failure.

---

### Pair 4 — Always supply `closeButtonLabel` and `iconTitle`

**Decision:** Both props are accessible names for elements that convey meaning. Treat them as mandatory in practice, not optional.

**Grounded in:** `accessibility.md` — *"Always provide `closeButtonLabel` — without it the close button has no accessible name. Always provide `iconTitle` when the status icon conveys semantic meaning."*

#### ✅ Do — Pass a specific `closeButtonLabel` and an `iconTitle` that names the status

> Screen readers announce the toast's icon and its close button by these labels. "Dismiss save confirmation" tells users what they're closing; "Success" tells them what the icon means.

#### ❌ Don't — Omit these props or use a generic "Close" / "Icon" label

> An unlabelled close button is a button with no name — useless to screen readers. A generic "Close" gives no context when heard out of order with other dismiss buttons on the page.

---

### Pair 5 — Pick the right surface: Toast for transient, AlertBanner for persistent, Modal for blocking, InlineNotification for embedded

**Decision:** Toast is one of four feedback surfaces in Oxygen. Pick by lifespan and disruption, not by which one you saw last.

**Grounded in:** `Toast-figma.md` — *"appears at the top corner of the UI below the top bar"* · `props.md` — `InlineNotification` is the in-layout sibling.

#### ✅ Do — Use Toast for ephemeral app-wide events; reach for AlertBanner / Modal / InlineNotification when the situation demands persistence, blocking, or embedded placement

> "Your changes were saved" → Toast. "Your VPN connection dropped — reconnect to continue" → AlertBanner. "Delete this customer? This cannot be undone." → Modal. A status badge inline with a settings row → InlineNotification or Tag.

#### ❌ Don't — Use Toast for content the user must address before continuing, or that must remain visible across navigation

> If dismissal means the user loses the only copy of important information, the surface is wrong.

---

### Pair 6 — `type="loading"` is for short, deterministic operations announced globally — not for long jobs or inline progress

**Decision:** A loading toast is a global, top-of-screen announcement that something is in flight. It should resolve into a success/error toast quickly.

**Grounded in:** `props.md` — `"loading"` is a `ToastType` value · `accessibility.md` — *"For `type="loading"`, use `aria-live="polite"` and update the content once the operation completes."*

#### ✅ Do — Use a loading toast for short, fire-and-forget operations whose outcome will replace it within a few seconds

> "Exporting…" → updates to "Export ready. Download" on completion.

#### ❌ Don't — Use a loading toast for an operation that takes 30+ seconds or for progress that lives next to a specific element

> Long-running work needs a determinate `ProgressBar`. Inline operations need an inline `Spinner` near the trigger, not a floating toast detached from context.

---

### Pair 7 — Write user-actionable copy in `title` and `description`; never paste raw error strings

**Decision:** `title` is a short user-facing headline; `description` is a single supporting sentence. Both should be plain language. Technical detail belongs behind an action button or in a details view.

**Grounded in:** `Toast-figma.md` (default Figma values model short user-facing copy) · `props.md` — `title` and `description` are sized for short text at a 320px container.

#### ✅ Do — Write `title` as a short outcome statement and `description` as one helpful supporting sentence

> *Title:* "Couldn't send message." *Description:* "Check your connection and try again." If technical detail matters, expose it behind an action button ("View details").

#### ❌ Don't — Drop raw error codes, stack traces, or JSON payloads into the toast body

> "Error: ECONNRESET at TCPConnectWrap.afterConnect..." is noise for end users and a wall of text for screen readers.
