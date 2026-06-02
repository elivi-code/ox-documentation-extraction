---
component: Calendar
package: "@8x8/oxygen-calendar"
category: date_time
role: tokens
role_description: "Design token bindings — colors, spacing, typography per component state"
pipeline_stage: blocked
pipeline_note: "Audit verdict NO — CONFLICTs must be resolved first"
audit_verdict: "NO"
siblings:
  - "[[Calendar/props]]"
  - "[[Calendar/examples]]"
  - "[[Calendar/accessibility]]"
  - "[[Calendar/Calendar-figma]]"
  - "[[Calendar/Calendar-usage]]"
  - "[[Calendar/Calendar-audit]]"
tags:
  - oxygen
  - component/Calendar
  - role/tokens
  - stage/blocked
  - category/date_time
---

# Calendar — Tokens

> **See also:** [props.md](props.md) · [examples.md](examples.md) · [accessibility.md](accessibility.md)

## Theme tokens

The Oxygen MCP returned **no theme tokens** for the `calendar` package. This is a known gap — Calendar likely consumes lower-level color and spacing tokens (e.g. `primary`, `neutral`, `interactive`) rather than registering component-scoped tokens.

To resolve: check the `UI-Foundations` Figma library (file key `iVY5nI8JAxM05Apnnvozzs`) for any calendar-specific token definitions, or inspect the component's compiled CSS for applied token names.

---

## Day states reference

The following visual states are documented in the usage guidelines; they correspond to token-driven styling but token names are not exposed by the MCP:

| State | Description |
|-------|-------------|
| Rest | Default day cell |
| Current day | Today's date — visually distinct |
| Disabled | Not selectable; tooltip may appear via `disabledDateTooltip` |
| Selected | The chosen date (single mode) or start/end of range |
| Hover | Cursor over a valid date |
| Focused date | Keyboard focus indicator |
| Day in previous/next month | Passive day completing the grid row (`isPassive: true`) |
| Selected start/end day | Range endpoints (range mode) |
| Selected date range | In-range days between start and end (range mode) |

---

_Source: Oxygen MCP · Extracted 2026-05-08_
