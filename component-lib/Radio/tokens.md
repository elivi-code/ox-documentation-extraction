---
component: Radio
package: "@8x8/oxygen-radio"
category: form_inputs
role: tokens
role_description: "Design tokens — color, spacing, and typography token bindings"
pipeline_stage: extracted
pipeline_note: "Core files present; audit not yet run"
siblings:
  - "[[Radio/props]]"
  - "[[Radio/examples]]"
  - "[[Radio/accessibility]]"
tags:
  - oxygen
  - component/Radio
  - role/tokens
  - stage/extracted
  - category/form_inputs
---
# Radio — Tokens

> **See also:** [Props](props.md) · [Examples](examples.md) · [Accessibility](accessibility.md)

## Theme Tokens

No dedicated Radio-specific theme tokens were returned by the Oxygen MCP token search.

The Radio component uses general Oxygen design tokens for its visual states. The spacing between Radio Button items in a group is controlled by:

| Token | Value | Usage |
|-------|-------|-------|
| `$spacing(2)` | `8px` | Gap between Radio Button items in a `RadioGroup` |

> This gap value was confirmed via Figma design specs (node 50606:93474).

---

## Variants

| Variant | Description |
|---------|-------------|
| Vertical (default) | Radio items stacked vertically; controlled by `RadioGroup` default |
| Horizontal | Radio items in a row; set `isHorizontal` on `RadioGroup` |

---

## States

| State | Applies to |
|-------|------------|
| Rest | Default unselected state |
| Hover | Mouse over the radio item |
| IsFocused | Keyboard focus ring visible |
| IsDisabled | `isDisabled={true}` — greyed out, non-interactive |
| IsChecked – Rest | Selected, no interaction |
| IsChecked – Hover | Selected + mouse over |
| IsChecked – IsFocused | Selected + keyboard focus |
| IsChecked – IsDisabled | Selected + disabled |

Both `Radio` (with label) and `Radio Button Input` (without label) share the same state set.

---

## Dark mode

The component renders correctly in both light and dark themes. No extra configuration is needed — theming is handled automatically by the Oxygen design system token layer.

_Source: Oxygen MCP + Figma (UI-components · nodes 51776:2800, 50606:93474) · Extracted 2026-04-29_
