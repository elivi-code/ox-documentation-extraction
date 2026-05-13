<!-- SKILL: usage-advisor -->
<!-- COMPONENT: Modal -->
<!-- DRAFTED: 2026-05-13 -->
<!-- MODE: open -->
<!-- GROUNDING: full -->
<!-- STATUS: DRAFT — approved pairs, ready for Figma push -->
---
component: Modal
package: "@8x8/oxygen-modal"
category: layout_overlay
role: usage_draft
role_description: "Approved Do/Don't pairs — scaffolding for the Figma examples page; NOT the canonical Modal-usage.md"
pipeline_stage: pre_review
audit_verdict: DRAFT
siblings:
  - "[[Modal/props]]"
  - "[[Modal/examples]]"
  - "[[Modal/tokens]]"
  - "[[Modal/accessibility]]"
  - "[[Modal/Modal-figma]]"
  - "[[Modal/Modal-pui]]"
  - "[[Modal/Modal-audit]]"
tags:
  - oxygen
  - component/Modal
  - role/usage_draft
  - stage/pre_review
  - category/layout_overlay
---
# Modal — Usage Guidelines (Draft)

> **Draft only.** Scaffolding for the `↳ Modal examples` Figma page.
> The canonical `Modal-usage.md` is produced by `figma-extract-usage` after the Figma page is filled.
> Six approved Do/Don't pairs — each anchored in a specific prop, accessibility rule, or internal precedent.

## Grounding summary

- **Files used:** `props.md`, `examples.md`, `tokens.md`, `accessibility.md`, `Modal-figma.md`, `Modal-pui.md`, `Modal-audit.md`
- **Files missing:** none
- **Internal precedent:**
  - `AlertBanner/alert-banner-usage.md:57` — *"User must complete an action before continuing and the whole UI is blocked → Modal / Dialog"*
  - `AlertBanner/alert-banner-usage.md:58` — *"Low-urgency informational status update that should not interrupt screen reader flow → Status region / Toast"*
  - `Button/Button-usage.md:221` (Pair 3) — *"Reserve destructive styling for irreversible actions … gate it with a confirmation dialog"*
  - `Button/Button-usage.md:128–129` — *"Destructive actions are usually placed left-most … Use `<ButtonGroup align='right' />` for dialogs"*

---

## Pair 1 — Use Modal only when the user must finish a task before continuing

**Decision:** A Modal blocks the entire UI. Reserve it for content the user genuinely cannot defer.
**Grounded in:** [accessibility.md:59-65](accessibility.md) (focus trap blocks the page); [Modal-figma.md:50-54](Modal-figma.md) (Custom Modal for tasks, Dialog Modal for confirmations).
**Internal precedent:** `AlertBanner/alert-banner-usage.md:57-58`.

### ✅ Do — Use Modal only when the user must finish a task before continuing
Reach for a Modal when the rest of the UI must wait — a destructive confirmation, a required form before access, a critical error blocking the workflow.

### ❌ Don't — Use Modal for status updates, low-urgency info, or content the user can defer
For non-blocking messages, use Toast, AlertBanner, or an inline status region. Modals interrupt screen readers and trap focus — reserve them for content the user must address right now.

---

## Pair 2 — Keep the focus trap on

**Decision:** Disabling `shouldUseFocusTrap` breaks keyboard navigation and screen-reader behaviour.
**Grounded in:** [props.md:84](props.md) `shouldUseFocusTrap` default `true`; [accessibility.md:65](accessibility.md) — *"Do not disable the focus trap (`shouldUseFocusTrap={false}`) unless you provide an equivalent mechanism. Disabling it breaks keyboard navigation for screen reader users."*

### ✅ Do — Leave `shouldUseFocusTrap` enabled and return focus to the trigger on close
Keep focus contained inside the dialog while it is open, and hand focus back via `focusAfterCloseItemRef` when it closes. This matches the WCAG dialog pattern.

### ❌ Don't — Disable the focus trap to allow background interactions
A modal that lets focus escape isn't really modal — keyboard and screen-reader users will lose track of where they are. If users need to interact with content behind the overlay, use a side panel or non-modal popover instead.

---

## Pair 3 — Overlay click needs a keyboard equivalent

**Decision:** `shouldCloseOnOverlayClick` defaults to `false`. If you turn it on, accessibility requires a non-mouse path to the same outcome.
**Grounded in:** [props.md:78](props.md); [accessibility.md:141-143](accessibility.md) — *"If you enable overlay click to close, ensure there is also a visible close mechanism (close button or Escape key) so keyboard-only users have an equivalent path."*

### ✅ Do — Pair `shouldCloseOnOverlayClick={true}` with a visible close button and `shouldCloseOnEsc={true}`
Overlay click is fine for dismissible, non-destructive dialogs — as long as keyboard users can reach the same outcome via Escape or a focusable close button.

### ❌ Don't — Enable overlay click as the only way to dismiss a modal
A keyboard-only user can't click the overlay. Without a close button or Escape support, they have no exit — that's a hard accessibility failure.

---

## Pair 4 — Destructive actions: name them, separate them, default to safe

**Decision:** A Dialog Modal exists specifically to confirm irreversible actions ([Modal-figma.md:74-80](Modal-figma.md)). The destructive button must say what will happen.
**Grounded in:** [props.md:60-65](props.md) `ModalFooter`; [Modal-figma.md:109-117](Modal-figma.md) footer atom.
**Internal precedent:** `Button/Button-usage.md:221` (Pair 3) · `Button/Button-usage.md:128–129`.

### ✅ Do — Confirm irreversible actions with a Dialog Modal; label the destructive button with the verb, place it left, default focus on Cancel
Pair `isDestructive` with a clear verb ("Delete account", not "Yes"). The destructive action sits left of the primary; the safe default ("Cancel") receives initial focus.

### ❌ Don't — Label the destructive button "OK" or "Yes", or default focus on the destructive action
Ambiguous verbs hide the consequence. If the user can lose data, the button must say what will happen — "Delete", "Discard", "End call".

---

## Pair 5 — Cap the footer at one primary + one secondary (plus optional tertiary text)

**Decision:** The footer atom is built around a single-decision hierarchy ([Modal-figma.md:109-117](Modal-figma.md)).
**Grounded in:** [Modal-figma.md:109-117](Modal-figma.md) footer atom variants — `textButton`, `secondaryButton`, `stacked?` booleans imply one primary + at most two supporting actions.

### ✅ Do — Limit footer actions to one primary, one secondary, and optionally one tertiary text button
Primary on the right, secondary to its left, optional tertiary text button as an escape hatch (e.g. "Learn more"). Stacking is reserved for narrow mobile widths.

### ❌ Don't — Stack three or more equally weighted buttons in the footer
If you need three peer actions, the decision belongs on a full page, not a modal. The footer atom is built around a single-decision hierarchy.

---

## Pair 6 — Give users a way out unless a decision is truly required

**Decision:** `ModalHeader`'s close icon is rendered only when `onClose` is wired ([props.md:122](props.md)) — that makes dismissibility a deliberate choice.
**Grounded in:** [props.md:122](props.md) — *"close icon is only rendered when this is a function"*; [props.md:77](props.md) `shouldCloseOnEsc` default `true`.

### ✅ Do — Render the close button and keep `shouldCloseOnEsc={true}` for any modal that doesn't require a decision
Wire `onClose` on `ModalHeader`, leave Escape enabled, and customise `iconCloseTitle` to describe the dialog. *Exception — omit `onClose` only when the user must make an unrecoverable decision (terms acceptance, account-deletion confirmation).*

### ❌ Don't — Hide the close button AND disable Escape on routine dialogs
Forcing a decision is appropriate for "Save before leaving?" but hostile for ordinary flows. If no path out exists, screen-reader users are stranded.

---

## Pair 7 — Match size to content, not to importance

**Decision:** `size` exposes `small | medium | big` ([props.md:80](props.md)); widths are `320px` mobile / `664px` desktop ([Modal-figma.md:197-200](Modal-figma.md)).
**Grounded in:** [props.md:80-82](props.md); [Modal-figma.md:74-80](Modal-figma.md) (Dialog Modal = small).

### ✅ Do — Match size to content: Dialog Modal (`small`) for confirmations, `medium` for short forms, `big` only for multi-step flows
Most modals belong at `medium`. Use `small` for one-sentence confirmations. Reserve `big` for genuinely dense flows that won't fit at `medium`.

### ❌ Don't — Use `big` to add visual weight to an unimportant message
Bigger isn't more important — it's harder to read. Pick the smallest size that holds the content without crowding.

---

## Axes presented but skipped (audit trail)

| Axis | Reason skipped |
|------|----------------|
| Scroll vs. truncate inside `ModalContent` | Mechanical — picked by content length, not editorial intent. Falls out of Pair 7 size guidance. |
| Modal stacking / nesting | No evidence of a stacking pattern in `examples.md` or `Modal-figma.md`. Heuristic-only. |
| Title + `aria-labelledby` wiring | Mechanical — already prescribed in `accessibility.md:38-49`. Belongs in dev docs. |
| Shadow / border (`hasShadow`) | Stylistic, no editorial choice — leave default. |
| `targetNode` portal target | Mechanical — implementation concern. |
| Pair 2 candidate B (initial focus / aria-labelledby specifics) | Duplicates accessibility.md prescriptions. Dev-doc territory. |
| Pair 3 candidate B (softer "don't enable for forms") | Dilutes the hard a11y rule in 3A. Dropped to keep 3A unambiguous. |
| Pair 7 candidate B (`width`/`height` override discipline) | Developer concern, not editorial. |

## Axes flagged as ungrounded

_None — every approved pair traces to a specific prop, accessibility rule, Figma annotation, or internal precedent quote._

---

## Next steps

1. ✅ **Approved pairs locked in** (7 cards — 1, 2, 3, 4, 5, 6, 7 above).
2. **Push to Figma** — invoke `figma-draw` to create the `↳ Modal examples` page in Figma with one labeled card per approved pair (`✅ Do — {reason}` / `❌ Don't — {reason}`). Then drop in Modal component instances and finalise wording in Figma.
3. **Then** — `figma-extract-usage` can run against the filled Figma page and produce the canonical `Modal-usage.md`.
