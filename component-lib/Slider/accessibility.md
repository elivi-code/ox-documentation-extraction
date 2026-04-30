# Slider — Accessibility

> **See also:** [props.md](props.md) · [examples.md](examples.md) · [tokens.md](tokens.md) · [slider-pui.md](slider-pui.md)

## ARIA role

The Slider thumb renders as `role="slider"`. The component uses the `ariaLabel` prop to set
`aria-label` on the thumb element when no visible label is associated with it.

For accessible labelling, either:
- Pass `ariaLabel` (e.g. `ariaLabel="Ring volume"`)
- Or place a visible `<label>` and associate it via `htmlFor` / `aria-labelledby`

## Required ARIA attributes (on thumb element)

| Attribute | Source | Example |
|-----------|--------|---------|
| `aria-label` | `ariaLabel` prop | `"Ring volume"` |
| `aria-valuenow` | Derived from `value` | `50` |
| `aria-valuemin` | Derived from `minValue` | `0` |
| `aria-valuemax` | Derived from `maxValue` | `100` |
| `aria-disabled` | Derived from `isDisabled` | `true` |

For range mode (`isMultiple`), each thumb should carry its own `aria-label`
(e.g. "Minimum volume", "Maximum volume").

## Keyboard interaction

| Key | Action |
|-----|--------|
| `ArrowRight` / `ArrowUp` | Increment value by `step` (default: 1) |
| `ArrowLeft` / `ArrowDown` | Decrement value by `step` |
| `Home` | Set value to `minValue` |
| `End` | Set value to `maxValue` |
| `Page Up` | Large step increment (typically 10 × step) |
| `Page Down` | Large step decrement |
| `Tab` | Move focus to thumb |
| `Shift+Tab` | Move focus away from thumb |

## Focus indicator

Figma specifies a visible focus ring on the thumb:
- **Light mode:** `2px solid` `--interactive/focus01` (`#0056e0`) with a `4px` white inner shadow
- **Dark mode:** `2px solid` `--interactive/focus01` (`#d7e3f9`) with a `4px` `#171719` inner shadow
- Border-radius: `1000px` (fully rounded)

The focus ring meets WCAG 2.1 AA contrast requirements in both modes.

## Screen reader guidance

- The component communicates the current value, minimum, and maximum to screen readers via
  `aria-valuenow`, `aria-valuemin`, and `aria-valuemax`.
- When the value changes, screen readers announce the new `aria-valuenow` automatically.
- If the slider controls audio volume, include contextual text (e.g. label "Ring volume") so
  the screen reader announces what is being adjusted.
- Disabled sliders should still be reachable by screen readers (though not keyboard-operable)
  so users are aware of the control.

## Touch / pointer

- The `expandTrackAreaBy` and `expandKnobAreaBy` props increase the invisible hit area of the
  track and thumb — use them on mobile to meet the WCAG 2.5.5 Target Size (44×44 CSS pixel)
  success criterion.
- The thumb expands visually to 32×32 px on Hover/Active states, providing additional visual
  feedback.

## WCAG 2.1 AA checklist

| Criterion | Notes |
|-----------|-------|
| **1.3.1 Info and Relationships** | `role="slider"` with `aria-valuemin/max/now` conveys semantics |
| **1.4.1 Use of Color** | State changes (active track colour) are also indicated by thumb position, not colour alone |
| **1.4.3 Contrast (Minimum)** | Label uses `--text/textcolor01`; verify final token values meet 4.5:1 |
| **1.4.11 Non-text Contrast** | Track and thumb must achieve 3:1 contrast against background — verify disabled states |
| **2.1.1 Keyboard** | Full arrow-key control, Home/End supported |
| **2.4.7 Focus Visible** | Focus ring defined in both Light and Dark modes (see tokens) |
| **2.5.3 Label in Name** | `ariaLabel` should match or contain the visible label text |
| **2.5.5 Target Size** | Default thumb is 16px; use `expandKnobAreaBy` on touch to reach 44px |
| **4.1.2 Name, Role, Value** | `aria-label`, `aria-valuenow/min/max`, `aria-disabled` all present |

_Source: Oxygen MCP + Figma (UI-components · 5YihJ5WuDvnvrlrRMC4sBp) · Extracted 2026-04-29_
