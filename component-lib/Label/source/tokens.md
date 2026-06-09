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
  - "[[Label/label-usage]]"
  - "[[Label/label-audit]]"
tags:
  - oxygen
  - component/Label
  - role/tokens
  - stage/blocked
  - category/data_display
---
# Label — Tokens

> **See also:** [props.md](props.md) · [examples.md](examples.md) · [accessibility.md](accessibility.md) · [label-usage.md](label-usage.md)

## Typography tokens

> **GAP-008 resolved 2026-06-08:** Figma source is authoritative. `@8x8/oxygen-label` uses `typography/body01` / `typography/bodyBold01` (14px). The MCP-returned `label01` / `labelBold01` (12px) were incorrect global theme matches — they do not apply to this component.

| Token | Family | Size | Line height | Weight | Letter spacing | Element |
|-------|--------|------|-------------|--------|----------------|---------|
| `typography/body01` | Inter | 14px | 20px | 400 (Regular) | −0.06px | Label text |
| `typography/bodyBold01` | Inter | 14px | 20px | 600 (SemiBold) | −0.06px | Required asterisk |

### Superseded MCP tokens (do not use)

The MCP returned `label01` / `labelBold01` (0.75rem / 12px) as matches for this component. These are global theme tokens that do not apply to `@8x8/oxygen-label`. Confirmed incorrect via Figma source comparison (GAP-008).

## Color tokens

| Token | Light value | Dark value | Description |
|-------|-------------|------------|-------------|
| `textColor01` | `#26252A` | `#FFFFFF` | Default primary text color used for label text |
| `error/error01` | `#cb2233` | `#f24d5f` | Required indicator (`*`) color when `isRequired` is `true` |

> **Note:** `textColor01` references `colorPalette.offwhite02` in light mode and `colorPalette.white` in dark mode.

## Token usage notes

- `label01` applies to standard (non-bold) label text.
- `labelBold01` applies when the label uses a bold weight variant (e.g. section headers pairing with form fields).
- The Label component inherits `textColor01` for its text in both themes.
- No component-scoped variant or size table was returned by the MCP — tokens above are theme-level matches.

_Source: Oxygen MCP · Extracted 2026-05-01_
