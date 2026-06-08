---
component: DateTimeSelector
package: "@8x8/oxygen-date-time-selector"
category: date_time
role: tokens
role_description: "Design token bindings — colors, spacing, typography per component state"
pipeline_stage: spec_ready
pipeline_note: "Audit verdict YES/PARTIAL — doc-rewrite can run"
audit_verdict: "YES"
siblings:
  - "[[DateTimeSelector/props]]"
  - "[[DateTimeSelector/examples]]"
  - "[[DateTimeSelector/accessibility]]"
  - "[[DateTimeSelector/DateTimeSelector-figma]]"
  - "[[DateTimeSelector/DateTimeSelector-usage]]"
  - "[[DateTimeSelector/DateTimeSelector-audit]]"
tags:
  - oxygen
  - component/DateTimeSelector
  - role/tokens
  - stage/spec_ready
  - category/date_time
---

# DateTimeSelector — Tokens

> **See also:** [props.md](props.md) · [examples.md](examples.md) · [accessibility.md](accessibility.md)

<!-- NOTE: Oxygen MCP returned no theme tokens for @8x8/oxygen-date-time-selector.
     Token values are sourced from Figma design context (DateTimeSelector-figma.md) once extracted.
     See GAP note below. -->

## Theme tokens

No tokens returned by `mcp__oxygen-mcp__get-theme-tokens` for this package.

Token names for DateTimeSelector are expected to follow the UI-Foundations semantic token convention
(`--ui/*`, `--text/*`, `--interactive/*`, `--actions/*`) — refer to [DateTimeSelector-figma.md](DateTimeSelector-figma.md)
for token bindings extracted from the Figma design context.

---

## Tokens from Figma (CSS-derived)

> CSS-derived from Figma design context (`get_design_context`). Pending confirmation against UI-Foundations variable panel (`iVY5nI8JAxM05Apnnvozzs`). See GAP-002.

### Color tokens

| Token | Element | State | Hex (observed) |
|-------|---------|-------|----------------|
| `--ui/ui05` | Dropdown background | Rest, Focus, Error | `#f4f3ee` |
| `--text/textcolor01` | Label text, Filled value text | All | `#26252a` |
| `--text/textcolor02` | Placeholder text, Hint text | Rest, Focus | `#6c6862` |
| `--error/error01` | Required `*`, Error border, Error message | Error | `#cb2233` |
| `--interactive/focus01` | Focus ring | Focus | `#0056e0` |

> Hover and Disabled state token values not confirmed — see GAP-008.

### Typography tokens

| Token | Element | Size | Weight | Line height | Letter spacing |
|-------|---------|------|--------|-------------|----------------|
| `body01` | Label | 14px | 400 | 20px | −0.06px |
| `bodybold01` | Required asterisk | 14px | 600 | 20px | −0.06px |
| `body02` | Placeholder / value | 16px | 400 | 24px | +0.0121px |
| `label01` | Hint text, Error text | 12px | 400 | 16px | 0px |

### Hardcoded values (no token binding)

| Property | Value |
|----------|-------|
| Dropdown width | 320px |
| Dropdown border radius | 6px |
| Container gap | 4px |
| Text / icon gap | 8px |
| Error border width | 2px |
| Icon Button border radius | 6px |
| Icon Button padding | 2px |

---

## Known states

Based on the Figma component set (Mode × Size × State × Error × Filled), the following visual states exist:

| State | Expected token role |
|-------|---------------------|
| Rest | Default surface + border |
| Hover | Hover surface |
| Focus | Focus ring (`--interactive/focus01`) |
| Disabled | Disabled text/surface |
| Error (True) | Error border/icon |
| Error (False) | Standard border |
| Filled (True) | Filled input surface |
| Filled (False) | Empty input surface |

---

_Source: Oxygen MCP · Extracted 2026-05-08_
