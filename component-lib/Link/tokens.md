# Link — Tokens

> **See also:** [props.md](props.md) · [examples.md](examples.md) · [accessibility.md](accessibility.md)

## Color tokens

All tokens are semantic aliases. Values are resolved at theme level (light/dark).

### Default surface

| Token | Role | Light value | Dark value | Palette ref |
|-------|------|-------------|------------|-------------|
| `$action08` | Primary link color (rest) | `#0056E0` | `#99BBF3` | blue05 / blue08 |
| `$hover07` | Link hover color | `#246FE5` | `#99BBF3` | blue06 / blue08 |
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

## Typography tokens

The Oxygen MCP did not return explicit typography tokens for `Link`. Based on usage docs:

| Variant | Typography token |
|---------|-----------------|
| Inline | Inherits from surrounding context (no fixed token) |
| Standalone | `$body02` (recommended) |

> **Data gap:** Typography token exact values for `$body02` were not included in this token query. Run `get-theme-tokens` with `search: "body02"` to retrieve.

_Source: Oxygen MCP · Extracted 2026-05-01_
