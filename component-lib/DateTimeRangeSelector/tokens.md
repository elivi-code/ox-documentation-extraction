# DateTimeRangeSelector — Tokens

> **See also:** [props.md](props.md) · [examples.md](examples.md) · [accessibility.md](accessibility.md)

<!-- NOTE: Oxygen MCP returned no theme tokens for @8x8/oxygen-date-time-range-selector.
     The trigger input shares the Figma "Date picker" component set (node 80239:8235) with
     DateTimeSelector — see DateTimeRangeSelector-figma.md for CSS-derived token names.
     The calendar panel tokens are documented in the Calendar component (component-lib/Calendar/tokens.md). -->

## Theme tokens

No tokens returned by `mcp__oxygen-mcp__get-theme-tokens` for this package.

This component is composed of two tokenised sub-systems:

| Sub-system | Token source |
|------------|-------------|
| Trigger input (trigger button / input field) | Shared "Date picker" Figma design — see [DateTimeRangeSelector-figma.md](DateTimeRangeSelector-figma.md) |
| Calendar + time picker panel | `@8x8/oxygen-calendar` — see [Calendar tokens](../../Calendar/tokens.md) |

---

## Known visual states (trigger input)

| State | Expected token role |
|-------|---------------------|
| Rest | `--ui/ui05` background; `--text/textcolor02` placeholder |
| Hover | Surface change (token unconfirmed) |
| Focus | `--interactive/focus01` focus ring |
| Error (`hasError=true`) | `--error/error01` border + error area |
| Disabled (`isDisabled=true`) | Disabled surface/text |
| Filled | `--text/textcolor01` value text (verify) |

---

_Source: Oxygen MCP · Extracted 2026-05-08_
