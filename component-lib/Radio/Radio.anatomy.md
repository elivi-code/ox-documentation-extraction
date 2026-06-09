---
parent: "[[Radio]]"
section: anatomy
---

## Variants

| Variant | Description |
|---------|-------------|
| Vertical (default) | Radio items stacked vertically; `isHorizontal` not set on `RadioGroup` |
| Horizontal | Radio items in a row; set `isHorizontal` on `RadioGroup` |

Both the labelled `Radio` and the no-label `Radio Button Input` variant share the same state set and structural elements.

---

## States

| State | Trigger |
|-------|---------|
| Rest | Default unselected state |
| Hover | Pointer over the radio row |
| IsFocused | Keyboard focus ring visible |
| IsDisabled | `isDisabled={true}` on an unchecked Radio — greyed out, non-interactive |
| IsChecked – Rest | Selected; no active pointer/keyboard interaction |
| IsChecked – Hover | Selected + pointer over the row |
| IsChecked – IsFocused | Selected + keyboard focus ring active |
| IsChecked – IsDisabled | `isDisabled={true}` on a checked Radio |

---

## Anatomy elements

The published Oxygen docs page identifies four numbered anatomy parts:

1. **Group label** *(optional)* — accessible name of the `RadioGroup`; labels the `role="radiogroup"` container via `aria-labelledby` or `aria-label`.
2. **Unselected radio button** — open circle when `isChecked` is `false`.
3. **Selected radio button** — filled circle dot when `isChecked` is `true`.
4. **Label** — option text to the right of the input circle (left-to-right languages); maps to the `label` prop.

Two additional API-exposed elements not numbered in the docs page anatomy:

5. **Info icon button + tooltip** *(optional)* — rendered when `infoBoxText` is set; a separate keyboard focus stop with its accessible name supplied by `infoBoxButtonLabel`.
6. **Focus ring** — covers the entire Radio row (input + label area), not just the input circle. Required by WCAG 2.4.7 — never suppress with `outline: none`.

> **Hit area:** The focus ring encompasses the entire Radio Button row — from the Radio Button Input to the label. The whole row area is interactive, clickable, and responsive to hover actions.

---

<!-- STUB:GAP-001 source="Run /figma-extract Radio against UI-components nodes 51776:2800 and 50606:93474 to capture per-variant structural details, horizontal gap between input circle and label, and full visual anatomy from Figma." -->
