---
parent: "[[Badge]]"
section: accessibility
---

## Component nature

Badge is a **passive/display** component. It is not interactive and must never receive keyboard focus. The parent element is responsible for carrying the accessible name that conveys the badge's meaning.

## ARIA guidance

| Scenario | Recommendation |
|----------|----------------|
| Counter badge on an icon button | Include the count in the parent's `aria-label`: `aria-label="Notifications, 4 unread"`. Add `aria-hidden="true"` to the `<Badge>` itself. |
| Dot badge (no counter) | `aria-hidden="true"` on the badge. Parent describes the state. |
| Mention badge (`@`) | Parent carries label: e.g. `aria-label="Messages, you have a mention"`. Badge: `aria-hidden="true"`. |
| Dynamically updating count | Add an `aria-live="polite"` visually-hidden region near the trigger to announce count changes without moving focus. |
| `AIBadge` | Decorative — add `aria-hidden="true"` unless the AI context is not already conveyed by surrounding content. |

### Accessible icon button with counter badge

```tsx
<button aria-label={`Notifications, ${count} unread`}>
  <BellIcon aria-hidden="true" />
  <Badge isInner aria-hidden="true">{count}</Badge>
</button>
```

### Live region for dynamic updates

```tsx
<>
  <button aria-label="Notifications">
    <BellIcon aria-hidden="true" />
    <Badge isInner aria-hidden="true">{count}</Badge>
  </button>
  {/* Visually hidden live region announces count changes */}
  <span className="sr-only" aria-live="polite" aria-atomic="true">
    {count > 0 ? `${count} unread notifications` : 'No unread notifications'}
  </span>
</>
```

## Keyboard interaction

None — Badge is not focusable. Ensure the **parent interactive element** (button, link, list item) is fully keyboard-accessible.

## Screen reader guidance

- Add `aria-hidden="true"` to `<Badge>` in all cases where the parent already describes the state.
- Never rely solely on the badge's visual appearance (colour or number) to convey information — always surface it in the parent's accessible name or a live region.
- For `type="secondary"` or `AIBadge`, verify whether the visual distinction is meaningful to screen reader users and annotate accordingly.

## WCAG 2.1 AA checklist

| Criterion | Requirement | Badge status |
|-----------|-------------|-------------|
| 1.4.3 Contrast (Minimum) | Text ≥ 4.5:1 | White on `#048284` ≈ 4.6:1 — **passes AA** |
| 1.4.3 Contrast (dark mode) | Text ≥ 4.5:1 | White on `#78CDCF` ≈ 1.7:1 — **check needed** (see GAP-002) |
| 1.4.11 Non-text Contrast | UI component ≥ 3:1 | Dot badge on white backgrounds — verify per usage context (see GAP-009) |
| 1.3.1 Info and Relationships | Info not conveyed by colour alone | Counter includes numeric text ✅; dot/mention require `aria-hidden` + parent label |
| 2.1.1 Keyboard | Non-interactive elements must not trap focus | ✅ Badge is not focusable |
| 4.1.2 Name, Role, Value | Interactive components need accessible names | N/A — Badge is not interactive; parent must carry the name |
| 4.1.3 Status Messages | Dynamic status must be announced without focus move | Use `aria-live="polite"` on a nearby region |

<!-- STUB:GAP-002 source="Confirm the actual dark-mode badge text colour by inspecting component source or Figma dark-theme frames. If white is used, escalate as an accessibility failure to the design system team. Update accessibility.md contrast row." -->
> **Source gap (major):** White text on dark-mode `notification01` (`#78CDCF`) yields ≈ 1.7:1 — below the 4.5:1 AA threshold. The dark theme may use a different text colour or darker background, but this is **unconfirmed**. Verify against Figma dark-theme frames / component source; escalate to the design system team if white is in fact used.

<!-- STUB:GAP-009 source="Calculate the contrast ratio of #048284 on #FFFFFF and #78CDCF on the dark-mode background. Record both ratios in the accessibility.md WCAG checklist. Update status to passes or fails as appropriate." -->
> **Source gap (minor):** WCAG 1.4.11 ratio for the dot badge (`#048284` on white) is listed as "verify per usage context" with no recorded calculation. Compute and record the confirmed ratio.
