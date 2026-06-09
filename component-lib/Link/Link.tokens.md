---
component: Link
parent: "[[Link]]"
section: tokens
pipeline_stage: draft
siblings:
  - "[[Link.props]]"
  - "[[Link.anatomy]]"
  - "[[Link.usage]]"
  - "[[Link.accessibility]]"
  - "[[Link.platform]]"
  - "[[Link.composition]]"
tags:
  - oxygen
  - component/Link
  - role/spoke-tokens
---

## Color tokens

All tokens are semantic aliases resolved at theme level (light/dark).

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

| Surface token | Link token | Light value | Dark value | Context |
|--------------|------------|-------------|------------|---------|
| `$ui02` | `$action05` | — | — | Default/received bubble |
| `$ui13`, `$ui14` | `$action07` | `#003486` | `#D7E3F9` | Sent bubble surface |

<!-- STUB:GAP-008 source="Run get-theme-tokens with search: 'action05' and populate the light/dark values for the $action05 row in the chat surface table." -->

## Focus ring tokens

| Token | Role | Light value | Dark value |
|-------|------|-------------|------------|
| `$focus01` | Default surface focus ring outer shadow | `#0056e0` | `#d7e3f9` |
| `$ui06` | Default surface focus ring inner border | `#ffffff` | `#171719` |
| `$focus02` | Inverted surface focus ring outer shadow | `#d7e3f9` | `#0056e0` |
| `$ui07` | Inverted surface focus ring inner border | `#26252a` | `#f1f1f1` |

Focus ring implementation: `border: 1px solid <ui06/ui07>` + `box-shadow: 0 0 0 2px <focus01/focus02>`.

## Typography tokens

| Variant | Typography token |
|---------|-----------------|
| Inline | Inherits from surrounding context (no fixed token) |
| Standalone | `$body02` (recommended) |

<!-- STUB:GAP-009 source="Run get-theme-tokens with search: 'body02' and add size, weight, and line-height values to the typography token table." -->
