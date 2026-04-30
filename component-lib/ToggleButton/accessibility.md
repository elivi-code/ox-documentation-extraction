# ToggleButton — Accessibility

> **See also:** [props.md](./props.md) · [examples.md](./examples.md) · [tokens.md](./tokens.md) · [ToggleButton-figma.md](./ToggleButton-figma.md)

---

## ARIA role

`ToggleButton` renders as an `<input type="checkbox">` under the hood (via `SwitchBase`), with an associated `<label>` linked by `htmlFor`/`id`.

- **Role:** `checkbox` (native HTML semantics)
- **Checked state:** communicated via `aria-checked` (native checkbox behaviour)
- **Indeterminate state:** communicated via `aria-checked="mixed"` or `indeterminate` property
- **Disabled:** communicated via `disabled` attribute — removes from tab order; screen readers announce "dimmed" or "unavailable"

---

## Info button

When `infoBoxText` is supplied, an additional icon button is rendered:
- Must receive `infoBoxButtonLabel` — this is the accessible `aria-label` for the button
- Without `infoBoxButtonLabel`, the info button has no accessible name

---

## Focus behaviour (from Figma annotations)

> "The focus includes the entire Toggle item, from the Toggle Switch to the label. The whole area of the item is interactive, clickable, and responsive to hover actions."

- Focus ring encompasses the **entire component** (switch + label), not just the switch
- Visual: 2px outline using `--interactive/focus01` token
- The focus ring is a separate overlay element, not a CSS outline on the input

---

## Keyboard interactions

| Key | Action |
|-----|--------|
| `Tab` | Moves focus to the toggle (or away from it) |
| `Space` | Toggles checked state when focused |
| `Tab` (with adjacent Icon Button) | Focus moves from Toggle to Icon Button as separate tab stops |

> **Figma note:** "As separate elements, the Toggle and the Icon Button each have a different focus state. This means that when navigating with a keyboard, the focus will shift from one to the other."

---

## Responsive / zoom behaviour (from Figma annotations)

| Scenario | Behaviour |
|----------|-----------|
| Browser font scaling | Font size increases, but **toggle switch size does not scale** — switch stays at fixed 40×24px, aligned to top |
| Browser zoom | Both font size **and** toggle switch scale proportionally, maintaining relative layout |
| Multiline label | When label wraps to multiple lines, toggle switch **stays aligned to the top** |

---

## Screen reader guidance

- The toggle label is the accessible name — keep labels concise and descriptive
- When the toggle's function is obvious from context and no label is shown (Toggle Input variant), ensure the **parent container** provides an accessible label via `aria-label` or `aria-labelledby`
- `isIndeterminate` should be used only when the toggle genuinely represents a mixed/partial state (e.g. a "select all" control where some children are selected)
- Avoid using `isChecked` without a matching `onChange` — controlled toggles with no handler will appear non-interactive to AT

---

## WCAG 2.1 AA checklist

| Criterion | Requirement | Status |
|-----------|-------------|--------|
| 1.4.1 Use of Color | State must not rely on color alone | ✅ Knot position changes (left/right) in addition to color |
| 1.4.3 Contrast (Text) | 4.5:1 minimum for label text | ✅ `textcolor01` (#26252a on white) passes; disabled uses lower contrast (by design) |
| 1.4.11 Non-text Contrast | 3:1 for UI component boundaries | ⚠️ Default toggle base (#6c6862 on white) — verify contrast ratio on actual backgrounds |
| 2.1.1 Keyboard | All functionality via keyboard | ✅ Tab + Space |
| 2.4.7 Focus Visible | Focus indicator clearly visible | ✅ 2px focus ring covering full toggle area |
| 3.3.2 Labels or Instructions | Inputs have visible labels | ✅ `label` prop required; inform screen readers |
| 4.1.2 Name, Role, Value | Name, role, state programmatically determined | ✅ Native checkbox semantics |

---

_Source: Oxygen MCP + Figma MCP accessibility annotations · Extracted 2026-04-29_
