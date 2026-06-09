---
component: Link
package: "@8x8/oxygen-link"
category: navigation
role: tokens
role_description: "Design tokens — color, spacing, and typography token bindings"
pipeline_stage: blocked
pipeline_note: "Audit verdict NO — resolve CONFLICTs before rewrite"
audit_verdict: NO
siblings:
  - "[[Link/props]]"
  - "[[Link/examples]]"
  - "[[Link/accessibility]]"
  - "[[Link/Link-figma]]"
  - "[[Link/Link-usage]]"
  - "[[Link/Link-audit]]"
tags:
  - oxygen
  - component/Link
  - role/tokens
  - stage/blocked
  - category/navigation
---
# Link — Tokens

> **See also:** [props.md](props.md) · [examples.md](examples.md) · [accessibility.md](accessibility.md)

## Color tokens

All tokens are semantic aliases. Values are resolved at theme level (light/dark).

### Default surface

| Token | Role | Light value | Dark value | Palette ref |
|-------|------|-------------|------------|-------------|
| `$action08` | Primary link color (rest) | `#0056E0` | `#99BBF3` | blue05 / blue08 |
| `$hover07` | Link hover color | `#246FE5` | `#99BBF3` | blue06 / blue08 |
| `$active14` | Link active color | `#003486` | `#ccddf9` | blue03 / blue09 |
| `$textColor08` | Visited link color | `#73348C` | `#FFFFFF` | violet05 / white |

### Inverted surface

| Token | Role | Light value | Dark value | Palette ref |
|-------|------|-------------|------------|-------------|
| `$action10` | Inverted link text color | `#99BBF3` | `#0056E0` | blue08 / blue05 |
| `$hover20` | Inverted link hover color | `#99BBF3` | `#0045B3` | blue08 / blue04 |
| `$active17` | Inverted link active color | `#CCDDF9` | `#003486` | blue09 / blue03 |

### Chat surface

Links in chat bubbles use different tokens based on the bubble surface:

| Surface token | Link token | Light value | Dark value | Context |
|--------------|------------|-------------|------------|---------|
| `$ui02` | `$action05` | — | — | Default/received bubble |
| `$ui13`, `$ui14` | `$action07` | `#003486` | `#D7E3F9` | Sent bubble surface |

> **Note:** `$action05` value not returned in the MCP token search for "link". Full value can be retrieved with a direct token lookup.

## Focus ring tokens

| Token | Role | Light value | Dark value |
|-------|------|-------------|------------|
| `$focus01` | Default surface focus ring outer shadow | `#0056e0` | `#d7e3f9` |
| `$ui06` | Default surface focus ring inner border | `#ffffff` | `#171719` |
| `$focus02` | Inverted surface focus ring outer shadow | `#d7e3f9` | `#0056e0` |
| `$ui07` | Inverted surface focus ring inner border | `#26252a` | `#f1f1f1` |

## Typography tokens

The Oxygen MCP did not return explicit typography tokens for `Link`. Based on usage docs:

| Variant | Typography token |
|---------|-----------------|
| Inline | Inherits from surrounding context (no fixed token) |
| Standalone | `$body02` (recommended) |

> **Data gap:** Typography token exact values for `$body02` were not included in this token query. Run `get-theme-tokens` with `search: "body02"` to retrieve.

_Source: Oxygen MCP · Extracted 2026-05-01_
