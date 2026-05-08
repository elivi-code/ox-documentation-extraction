---
component: Label
package: "@8x8/oxygen-label"
category: data_display
role: tokens
role_description: "Design tokens — color, spacing, and typography token bindings"
pipeline_stage: blocked
pipeline_note: "Audit verdict NO — resolve CONFLICTs before rewrite"
audit_verdict: NO
siblings:
  - "[[Label/props]]"
  - "[[Label/examples]]"
  - "[[Label/accessibility]]"
  - "[[Label/Label-figma]]"
  - "[[Label/label-pui]]"
  - "[[Label/label-audit]]"
tags:
  - oxygen
  - component/Label
  - role/tokens
  - stage/blocked
  - category/data_display
---
# Label — Tokens

> **See also:** [props.md](props.md) · [examples.md](examples.md) · [accessibility.md](accessibility.md)

## Typography tokens

| Token | Light value | Dark value | Description |
|-------|-------------|------------|-------------|
| `label01` | Inter, 0.75rem / 1rem, weight 400 | same | Default label typography set |
| `labelBold01` | Inter, 0.75rem / 1rem, weight 600 | same | Bold label typography set |

### `label01` detail

```json
{
  "fontFamily": "Inter, sans-serif",
  "fontSize": "0.75rem",
  "lineHeight": "1rem",
  "fontWeight": 400,
  "letterSpacing": "normal"
}
```

### `labelBold01` detail

```json
{
  "fontFamily": "Inter, sans-serif",
  "fontSize": "0.75rem",
  "lineHeight": "1rem",
  "fontWeight": 600,
  "letterSpacing": "normal"
}
```

## Color tokens

| Token | Light value | Dark value | Description |
|-------|-------------|------------|-------------|
| `textColor01` | `#26252A` | `#FFFFFF` | Default primary text color used for label text |

> **Note:** `textColor01` references `colorPalette.offwhite02` in light mode and `colorPalette.white` in dark mode.

## Token usage notes

- `label01` applies to standard (non-bold) label text.
- `labelBold01` applies when the label uses a bold weight variant (e.g. section headers pairing with form fields).
- The Label component inherits `textColor01` for its text in both themes.
- No component-scoped variant or size table was returned by the MCP — tokens above are theme-level matches.

_Source: Oxygen MCP · Extracted 2026-05-01_
