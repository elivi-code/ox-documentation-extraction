# Badge — Accessibility

> **See also:** [props.md](props.md) · [examples.md](examples.md) · [tokens.md](tokens.md)

---

## Component nature

Badge is a **passive/display** component. It is not interactive and must never receive keyboard focus. The parent element is responsible for carrying the accessible name that conveys the badge's meaning.

---

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

### Accessible dot badge

```tsx
<ListItem label="Meetings">
  <Badge size="small" aria-hidden="true" />
</ListItem>
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

---

## Keyboard interaction

None — Badge is not focusable. Ensure the **parent interactive element** (button, link, list item) is fully keyboard-accessible.

---

## Screen reader guidance

- Add `aria-hidden="true"` to `<Badge>` in all cases where the parent already describes the state.
- Never rely solely on the badge's visual appearance (colour or number) to convey information — always surface it in the parent's accessible name or a live region.
- For `type="secondary"` or `AIBadge`, verify whether the visual distinction is meaningful to screen reader users and annotate accordingly.

---

## WCAG 2.1 AA checklist

| Criterion | Requirement | Badge status |
|-----------|-------------|-------------|
| 1.4.3 Contrast (Minimum) | Text ≥ 4.5:1 | White on `#048284` ≈ 4.6:1 — **passes AA** |
| 1.4.3 Contrast (dark mode) | Text ≥ 4.5:1 | White on `#78CDCF` ≈ 1.7:1 — **check needed** (dark mode text colour may differ) |
| 1.4.11 Non-text Contrast | UI component ≥ 3:1 | Dot badge on white backgrounds — verify per usage context |
| 1.3.1 Info and Relationships | Info not conveyed by colour alone | Counter includes numeric text ✅; dot/mention require `aria-hidden` + parent label |
| 2.1.1 Keyboard | Non-interactive elements must not trap focus | ✅ Badge is not focusable |
| 4.1.2 Name, Role, Value | Interactive components need accessible names | N/A — Badge is not interactive; parent must carry the name |
| 4.1.3 Status Messages | Dynamic status must be announced without focus move | Use `aria-live="polite"` on a nearby region |

> **Dark mode note:** The dark `notification01` value (`#78CDCF`) is a lighter teal — if white text is used in dark mode, the contrast ratio will be insufficient. Verify that the dark theme uses a different text colour or a darker background for the Badge.

---

_Source: Oxygen MCP (`@8x8/oxygen-badge`) · Figma node 2565:14 · Inferred from component nature · Extracted 2026-04-29_
