---
parent: "[[Calendar]]"
section: tokens
---

## Tokens

<!-- STUB:GAP-002 source="Oxygen MCP returned no theme tokens for @8x8/oxygen-calendar. Resolve token names by running figma_get_variables on the UI-Foundations library file (iVY5nI8JAxM05Apnnvozzs) and cross-referencing CSS variable names in Calendar-figma.md." -->
<!-- STUB:GAP-007 source="Token names below were extracted from Figma's generated CSS (get_design_context), NOT confirmed from the UI-Foundations variables panel (iVY5nI8JAxM05Apnnvozzs). Run figma_get_variables to confirm names and resolve aliases. (depends on GAP-002)" -->

> ⚠️ **Token names are provisional.** The Oxygen MCP returned no component-scoped theme tokens for `@8x8/oxygen-calendar`. The names below (`--ui/*`, `--actions/*`, `--text/*`, `--interactive/*`) come from Figma's generated CSS output, not from the UI-Foundations variables panel (file key `iVY5nI8JAxM05Apnnvozzs`). Treat the table as authoritative for structure (which element/state maps to which role), but defer to UI-Foundations for the canonical token name once mapping is confirmed.

### Color & token bindings (states as columns, elements as rows)

| Element | Default | Hover | Selected | Disabled | Focus |
|---------|---------|-------|----------|----------|-------|
| Calendar background | `--ui/ui06` (white) | — | — | — | — |
| Calendar border | `--ui/ui01` (#ebeae1) | — | — | — | — |
| Calendar shadow | `--ui/shadow01` (rgba(41,41,41,0.25)) | — | — | — | — |
| Day number text | `--text/textcolor01` (#26252a) | `--text/textcolor01` | `--ui/ui06` (white) | `--text/textcolor06` | `--text/textcolor01` |
| Day cell background | transparent | `--ui/ui02` | `--actions/action01` (#0056e0) | transparent | transparent |
| Day cell focus ring | — | — | — | — | `--interactive/focus01` (#0056e0) |
| In-range day background | `--ui/ui01` (#ebeae1) | — | — | — | — |
| Current day dot | `--actions/action01` (#0056e0) | — | — | — | — |
| Dimmed day text | `--text/textcolor06` | — | — | — | — |
| Predefined range item text | `--text/textcolor01` | `--text/textcolor01` | `--text/textcolor01` | — | `--text/textcolor01` |
| Predefined range item background | transparent | `--ui/ui02` | `--ui/ui05` | — | `--ui/ui05` |
| Intraday toggle (ON) | `--actions/action01` (#0056e0) | — | — | — | — |
| Apply button background | `--actions/action09` (#0056e0) | — | — | — | — |
| Dividers | `--ui/ui01` (#ebeae1) | — | — | — | — |
| Month/Year dropdown text | `--text/textcolor01` | — | — | — | — |
| Navigation icon | `--text/textcolor01` | — | — | — | — |

### Text styles

| Element | Token | Size | Weight | Line height | Letter spacing |
|---------|-------|------|--------|-------------|---------------|
| Day number | `body01` | 14px | 400 (normal) | 20px | −0.06px |
| Month/Year in header | `body01` | 14px | 400 | 20px | −0.06px |
| Month/Year in dropdown | `bodybold01` | 14px | 600 (semi-bold) | 20px | −0.06px |
| Predefined ranges item | `body01` | 14px | 400 | 20px | −0.06px |
| Weekday header | `label01` | — | — | — | — |
| Action button labels | `bodybold01` | 14px | 600 | 20px | −0.06px |

### Effect styles

| Element | Type | Value |
|---------|------|-------|
| Calendar panel | drop-shadow | `0px 1px 1px var(--ui/shadow01)` |

---

## Day states reference

The following visual states correspond to token-driven styling (token names provisional, per the stubs above):

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

## Hardcoded values (no token binding)

Flagged in Figma extraction — these structural values are raw px, not tokenised:

- `Container.width`: `788px` (range) / `312px` (single)
- `Predefined ranges panel.width`: `148px`
- `Month column.width`: `280px`
- `Day cell.size`: `40px`
- `Container.border-radius`: `6px`
- `Navigation button.padding`: `6px`
- `Calendar gap`: `32px` (between months)
- `Month header padding-x`: `40px`
