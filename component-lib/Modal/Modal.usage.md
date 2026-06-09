---
parent: "[[Modal]]"
section: usage
component: Modal
role: spoke
pipeline_stage: published
audit_verdict: partial
siblings:
  - "[[Modal]]"
  - "[[Modal.props]]"
  - "[[Modal.anatomy]]"
  - "[[Modal.tokens]]"
  - "[[Modal.accessibility]]"
  - "[[Modal.platform]]"
  - "[[Modal.composition]]"
tags:
  - oxygen
  - component/Modal
  - role/spoke
  - stage/published
---

<!-- STUB:GAP-001 source="Option A (canonical): push pairs below to Figma via figma-draw to create the '↳ Modal examples' page, then run figma-extract-usage to produce Modal-usage.md; Option B (current): using usage-advisor draft (2026-05-13, 7 approved pairs) grounded in props.md, accessibility.md, Modal-figma.md, and internal precedent until the Figma path completes" -->

> **Draft source.** These 7 Do/Don't pairs come from the usage-advisor skill (2026-05-13), not from figma-extract-usage. The canonical `Modal-usage.md` will replace this once the Figma examples page is created and extracted.

---

## Use Modal only when the user must finish a task before continuing

### ✅ Do — Use Modal only when the user must finish a task before continuing

Reach for a Modal when the rest of the UI must wait — a destructive confirmation, a required form before access, a critical error blocking the workflow.

### ❌ Don't — Use Modal for status updates, low-urgency info, or content the user can defer

For non-blocking messages, use Toast, AlertBanner, or an inline status region. Modals interrupt screen readers and trap focus — reserve them for content the user must address right now.

---

## Keep the focus trap on

### ✅ Do — Leave `shouldUseFocusTrap` enabled and return focus to the trigger on close

Keep focus contained inside the dialog while it is open, and hand focus back via `focusAfterCloseItemRef` when it closes. This matches the WCAG dialog pattern.

### ❌ Don't — Disable the focus trap to allow background interactions

A modal that lets focus escape isn't really modal — keyboard and screen-reader users will lose track of where they are. If users need to interact with content behind the overlay, use a side panel or non-modal popover instead.

---

## Overlay click needs a keyboard equivalent

### ✅ Do — Pair `shouldCloseOnOverlayClick={true}` with a visible close button and `shouldCloseOnEsc={true}`

Overlay click is fine for dismissible, non-destructive dialogs — as long as keyboard users can reach the same outcome via Escape or a focusable close button.

### ❌ Don't — Enable overlay click as the only way to dismiss a modal

A keyboard-only user can't click the overlay. Without a close button or Escape support, they have no exit — that's a hard accessibility failure.

---

## Destructive actions: name them, separate them, default to safe

### ✅ Do — Confirm irreversible actions with a Dialog Modal; label the destructive button with the verb, place it left, default focus on Cancel

Pair `isDestructive` with a clear verb ("Delete account", not "Yes"). The destructive action sits left of the primary; the safe default ("Cancel") receives initial focus.

### ❌ Don't — Label the destructive button "OK" or "Yes", or default focus on the destructive action

Ambiguous verbs hide the consequence. If the user can lose data, the button must say what will happen — "Delete", "Discard", "End call".

---

## Cap the footer at one primary + one secondary (plus optional tertiary text)

### ✅ Do — Limit footer actions to one primary, one secondary, and optionally one tertiary text button

Primary on the right, secondary to its left, optional tertiary text button as an escape hatch (e.g. "Learn more"). Stacking is reserved for narrow mobile widths.

### ❌ Don't — Stack three or more equally weighted buttons in the footer

If you need three peer actions, the decision belongs on a full page, not a modal. The footer atom is built around a single-decision hierarchy.

---

## Give users a way out unless a decision is truly required

### ✅ Do — Render the close button and keep `shouldCloseOnEsc={true}` for any modal that doesn't require a decision

Wire `onClose` on `ModalHeader`, leave Escape enabled, and customise `iconCloseTitle` to describe the dialog. _Exception — omit `onClose` only when the user must make an unrecoverable decision (terms acceptance, account-deletion confirmation)._

### ❌ Don't — Hide the close button AND disable Escape on routine dialogs

Forcing a decision is appropriate for "Save before leaving?" but hostile for ordinary flows. If no path out exists, screen-reader users are stranded.

---

## Match size to content, not to importance

### ✅ Do — Match size to content: Dialog Modal (`small`) for confirmations, `medium` for short forms, `big` only for multi-step flows

Most modals belong at `medium`. Use `small` for one-sentence confirmations. Reserve `big` for genuinely dense flows that won't fit at `medium`.

### ❌ Don't — Use `big` to add visual weight to an unimportant message

Bigger isn't more important — it's harder to read. Pick the smallest size that holds the content without crowding.

_Source: usage-advisor skill · Drafted 2026-05-13_
