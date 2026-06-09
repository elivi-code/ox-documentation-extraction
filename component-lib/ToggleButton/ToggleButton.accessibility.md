---
parent: "[[ToggleButton]]"
section: accessibility
pipeline_stage: draft
tags:
  - oxygen
  - component/ToggleButton
  - role/spoke
  - section/accessibility
---

## ARIA role

`ToggleButton` renders as an `<input type="checkbox">` (via `SwitchBase`), with an associated `<label>` linked by `htmlFor`/`id`.

- **Role:** `checkbox` (native HTML semantics)
- **Checked state:** communicated via `aria-checked` (native checkbox behaviour)
- **Indeterminate state:** communicated via `aria-checked="mixed"` or the `indeterminate` property
- **Disabled:** communicated via `disabled` attribute — removes from tab order; screen readers announce "dimmed" or "unavailable"

> **WARN-001 (heuristic):** `aria-checked="mixed"` for `isIndeterminate` may be incorrect — native HTML checkbox `.indeterminate` does not automatically update `aria-checked`; it stays `false`. If `SwitchBase` sets `aria-checked` explicitly, this is correct. Verify against the `SwitchBase` implementation before shipping an indeterminate toggle to production.

## Info button

When `infoBoxText` is supplied, an additional icon button is rendered:
- **Must** receive `infoBoxButtonLabel` — this is the accessible `aria-label` for the button.
- Without `infoBoxButtonLabel`, the info button has no accessible name.

## Focus behaviour

> "The focus includes the entire Toggle item, from the Toggle Switch to the label. The whole area of the item is interactive, clickable, and responsive to hover actions."

- Focus ring encompasses the **entire component** (switch + label), not just the switch
- Visual: 2px outline using `--interactive/focus01` token
- The focus ring is a separate overlay element, not a CSS outline on the input
- On **Toggle Input** (switch only): focus ring surrounds the switch alone

## Keyboard interactions

| Key | Action |
|---|---|
| `Tab` | Moves focus to the toggle (or away from it) |
| `Space` | Toggles checked state when focused |
| `Tab` (with adjacent Icon Button) | Focus moves from Toggle to Icon Button as separate tab stops |

> "As separate elements, the Toggle and the Icon Button each have a different focus state. This means that when navigating with a keyboard, the focus will shift from one to the other."

## Responsive / zoom behaviour

| Scenario | Behaviour |
|---|---|
| Browser font scaling | Font size increases; toggle switch stays fixed at 40×24px, top-aligned |
| Browser zoom | Font size and toggle switch scale proportionally, maintaining relative layout |
| Multiline label | Toggle switch stays top-aligned when label wraps to multiple lines |

## Screen reader guidance

- The toggle label is the accessible name — keep labels concise and descriptive.
- When the toggle's function is obvious from context and no label is shown (Toggle Input variant), ensure the **parent container** provides an accessible label via `aria-label` or `aria-labelledby`.
- `isIndeterminate` should be used only when the toggle genuinely represents a mixed/partial state (e.g. a "select all" control where some children are selected).
- Avoid `isChecked` without a matching `onChange` — controlled toggles with no handler appear non-interactive to assistive technology.

## WCAG 2.1 AA checklist

| Criterion | Requirement | Status |
|---|---|---|
| 1.4.1 Use of Color | State must not rely on color alone | ✅ Knot position changes (left/right) in addition to color |
| 1.4.3 Contrast (Text) | 4.5:1 minimum for label text | ✅ `textcolor01` (#26252a on white) passes; disabled uses lower contrast by design |
| 1.4.11 Non-text Contrast | 3:1 for UI component boundaries | ⚠️ Default toggle base (#6c6862 on white) ≈ 4.6:1 — passes 3:1; the ⚠️ likely should be ✅. Confirm against actual background context (WARN-002). |
| 2.1.1 Keyboard | All functionality via keyboard | ✅ Tab + Space |
| 2.4.7 Focus Visible | Focus indicator clearly visible | ✅ 2px focus ring covering full toggle area |
| 3.3.2 Labels or Instructions | Inputs have visible labels | ✅ `label` prop; screen readers read it |
| 4.1.2 Name, Role, Value | Name, role, state programmatically determined | ✅ Native checkbox semantics |

> **WARN-002 (heuristic):** WCAG 1.4.11 is marked ⚠️ for default toggle base (#6c6862 on white). Calculated contrast ≈ 4.6:1 — passes the 3:1 minimum. The ⚠️ should be updated to ✅ pending confirmation of the actual background context in production.

_Source: Oxygen MCP + Figma MCP accessibility annotations · Extracted 2026-04-29_
