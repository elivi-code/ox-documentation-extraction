---
parent: "[[Tooltip]]"
section: accessibility
---

## Accessibility

Tooltip follows the **WAI-ARIA Tooltip pattern** (`role="tooltip"`).

---

## ARIA role and attributes

| Attribute | Value | Notes |
|-----------|-------|-------|
| `role` | `tooltip` | Applied to the tooltip container element |
| `aria-describedby` | `{tooltip-id}` | Automatically added to the trigger element, linking it to the tooltip content |

The `disableDescribedBy` prop suppresses the `aria-describedby` binding — only use this when the trigger already has an explicit `aria-label` or when the tooltip content duplicates visible text.

---

## Keyboard interactions

| Key | Behaviour |
|-----|-----------|
| `Tab` | Moves focus to the trigger element |
| Focus on trigger | Shows the tooltip (equivalent to hover) |
| `Escape` | Closes the tooltip |
| `Tab` (away) | Hides the tooltip when focus leaves the trigger |

> **Note:** When `showOn="click"`, the tooltip opens on `Enter` / `Space` on the trigger (standard button semantics). Ensure the trigger is a native interactive element or has `role="button"` with `tabIndex={0}`.

---

## Screen reader guidance

- The tooltip content (`title` prop) is exposed via `aria-describedby`, not `aria-label`. Screen readers announce the trigger's own label first, then the tooltip as supplementary description.
- **Do not** put the only meaningful label for an element inside the tooltip. Use `aria-label` on the trigger directly for primary labels (e.g. icon buttons).
- Tooltip content should be **plain text** only. Interactive elements (links, buttons) inside tooltips are inaccessible for keyboard-only and screen reader users.

---

## Content constraints

- Maximum 140 characters (English) — keeps announcements brief.
- Use `disableDescribedBy` only when the tooltip duplicates information already present in the accessible name.
- Avoid `ReactNode` rich content that includes interactive elements — use a popover or modal instead.

---

## WCAG 2.1 AA checklist

| Criterion | Status | Notes |
|-----------|--------|-------|
| 1.3.1 Info and Relationships | Pass | `role="tooltip"` + `aria-describedby` convey relationship programmatically |
| 1.4.3 Contrast (Minimum) | Verify | Tooltip text/background contrast must meet 4.5:1 — see GAP-013 |
| 1.4.13 Content on Hover or Focus | Pass | Tooltip persists on hover (interactive by default); `disableInteractive` opts out |
| 2.1.1 Keyboard | Pass | Tooltip activates on focus; dismisses with Escape |
| 2.1.2 No Keyboard Trap | Pass | Tooltip is purely descriptive; focus stays on trigger |
| 2.4.3 Focus Order | Pass | Trigger is naturally in tab order |
| 4.1.2 Name, Role, Value | Pass | `role="tooltip"` + `aria-describedby` correctly implemented |
| 4.1.3 Status Messages | N/A | Tooltip is not a status message |

<!-- STUB:GAP-013 source="Calculate contrast ratio for Light (#ffffff text on #26252a background) and Dark (#292929 text on #f1f1f1 background) modes. Both should meet 4.5:1 (WCAG 1.4.3). Update checklist row to Pass or flag as Fail. Resolve GAP-011 (token verification) first." -->

---

## Do / Don't

**Do:**
- Use Tooltip to describe icon buttons without visible labels.
- Pair with focusable triggers (buttons, links, inputs).
- Keep content brief and supplementary.

**Don't:**
- Put links, buttons, or other interactive content inside the tooltip.
- Use tooltip for critical information users must act on — use helper text or inline content instead.
- Apply `disableDescribedBy` unless you have an explicit alternative accessible description.

---

## Figma accessibility annotations

No ARIA role, focus order, or keyboard interaction annotations are present in the Figma component.

<!-- STUB:GAP-019 source="Request designer to add ARIA role, focus behaviour, and keyboard interaction annotations to the Tooltip Figma component. See Tooltip.anatomy for current Figma annotation status." -->
