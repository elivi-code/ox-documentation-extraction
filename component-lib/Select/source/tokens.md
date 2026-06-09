---
component: Select
package: "@8x8/oxygen-select"
category: form_inputs
role: tokens
role_description: "Design tokens — color, spacing, and typography token bindings"
pipeline_stage: blocked
pipeline_note: "Audit verdict NO — resolve CONFLICTs before rewrite"
audit_verdict: NO
siblings:
  - "[[Select/props]]"
  - "[[Select/examples]]"
  - "[[Select/accessibility]]"
  - "[[Select/select-pui]]"
  - "[[Select/Select-audit]]"
tags:
  - oxygen
  - component/Select
  - role/tokens
  - stage/blocked
  - category/form_inputs
---
# Select — Tokens

> **See also:** [props.md](props.md) · [examples.md](examples.md) · [accessibility.md](accessibility.md)

## Theme tokens

The Select component is styled via the Oxygen theme system provided by `@8x8/oxygen-config` and `@8x8/oxygen-constants`. The following global tokens apply directly to Select states:

| Token | Light value | Dark value | Reference | Usage |
|-------|-------------|------------|-----------|-------|
| `ui01` | `#EBEAE1` | `#666666` | `colorPalette.offwhite09` (light) / `colorPalette.gray05` (dark) | Primary border color for cards and dividers, tertiary background, **selected state background color for list items** |

> **Note:** Only `ui01` was returned by the MCP token search for "select". Additional component-level tokens (input border, focus ring, error colour, disabled opacity) are defined internally in the select package's styled-components and are not exposed as standalone theme tokens.

## Sizes

| Size prop value | Figma label | Input height |
|-----------------|-------------|-------------|
| `'small'` | Small | 76px |
| `'default'` | Medium | 84px |
| `'large'` | Large | 92px |

## States × Tokens mapping

| State | Visual indicator | Token / style |
|-------|-----------------|---------------|
| Rest | Default border | Internal border token |
| Hover | Highlighted border | Internal hover token |
| Focus | Blue focus ring | Internal focus ring |
| Disabled | Reduced opacity, no interaction | Internal disabled opacity |
| Read-only | Muted appearance, non-editable | Internal read-only style |
| Error | Red border + error message below | Internal error colour |
| Open | Elevated shadow on popover | Internal popover shadow |

## Modes

| Mode | Description |
|------|-------------|
| Light | Default; white/light background |
| Dark | Inverted; dark background. Token values shift (e.g. `ui01` goes from `#EBEAE1` to `#666666`) |

_Source: Oxygen MCP · Extracted 2026-04-29_
