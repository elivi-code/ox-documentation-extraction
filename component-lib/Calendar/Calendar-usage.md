# Calendar — Usage Guidelines

> **See also:** [props.md](./props.md) · [examples.md](./examples.md) ·
> [tokens.md](./tokens.md) · [accessibility.md](./accessibility.md)

---

<!-- NOTE: The Figma "↳ Calendar examples" page (node 69971:10137) contains usage
     illustration sections but NO ✅ Do / ❌ Don't editorial cards following the
     standard figma-draw template convention. The sections below document the
     annotated demonstrations found on the page verbatim. -->

## Page sections

The `↳ Calendar examples` Figma page is organised into five sections:

| Section | Description |
|---------|-------------|
| Date picker examples | Default range and single calendar in light mode |
| Date picker range responsive | Breakpoint demonstrations (992→769, 768→541, 540→320) with/without predefined ranges panel |
| Popovers inside Date picker | Predefined ranges popover, time popover, month picker popover |
| 90 days limit | Disabled date states, tooltip behaviour on hover/focus |
| Intraday | Intraday toggle on/off and intraday info tooltip |

---

## Annotations from Figma (verbatim)

### Popovers inside Date picker

> **Predefined ranges popover sizing:** For predefined ranges popover, the max-height is set to 400px, the width is set to 300px.

> **Predefined ranges trigger:** Predefined ranges list will appear on click on the dropdown button.

> **Time / month / year popovers:** For time, month and year popovers, the max-height is set to 240px.

### 90 days limit

> **Context:** Some reports have a limit of 90 days for stored data.

> **Disabled dates:** If the dates are not in the 90 days segment, the state for those dates will be disabled.

> **Tooltip on hover:** On hover — tooltip is displayed.

> **Tooltip on focus:** On focus — tooltip is displayed.

> **90-day boundary indicator:** Persistent details. *(references a Marker component placed at the 90-day boundary in the calendar grid)*

---

## Breakpoint behaviour

| Breakpoint range | Predefined ranges | Layout |
|-----------------|------------------|--------|
| 992 → 769px | Visible | Dual month + ranges panel |
| 992 → 769px | Hidden | Dual month only |
| 768 → 541px | Visible | Dual month + ranges panel |
| 768 → 541px | Hidden | Dual month, narrower |
| 540 → 320px | Visible | Single month + stacked ranges |
| 540 → 320px | Hidden | Single month only |

---

## Gaps

| Type | Description |
|------|-------------|
| Missing Do/Don't cards | The examples page contains no `✅ Do —` or `❌ Don't —` frames — editorial Do/Don't guidance has not been created for Calendar |
| No screenshots | Desktop Bridge not connected; card-level screenshots unavailable |

---

_Source: Figma `↳ Calendar examples` page (node 69971:10137) · Extracted 2026-05-08_
