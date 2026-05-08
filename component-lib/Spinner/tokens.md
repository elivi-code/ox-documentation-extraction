---
component: Spinner
package: "@8x8/oxygen-loaders"
category: feedback_status
role: tokens
role_description: "Design tokens — color, spacing, and typography token bindings"
pipeline_stage: blocked
pipeline_note: "Audit verdict NO — resolve CONFLICTs before rewrite"
audit_verdict: NO
siblings:
  - "[[Spinner/props]]"
  - "[[Spinner/examples]]"
  - "[[Spinner/accessibility]]"
  - "[[Spinner/Spinner-figma]]"
  - "[[Spinner/Spinner-audit]]"
tags:
  - oxygen
  - component/Spinner
  - role/tokens
  - stage/blocked
  - category/feedback_status
---
# Spinner — Tokens

> **See also:** [props.md](props.md) · [examples.md](examples.md) · [accessibility.md](accessibility.md)

## Theme tokens

No dedicated theme tokens were returned by the Oxygen MCP for the `Spinner` component or the `loaders` package. The spinner's visual appearance (stroke color, stroke width, animation speed) is controlled via the `strokeWidth` prop and inherits from the surrounding theme context rather than component-level tokens.

**Source gap:** If token names are expected to exist (e.g. for color or animation customisation), they should be verified directly in the Oxygen token library or Figma variables.

## Size reference

Named sizes are resolved from the `spinnerSize` enum inside `@8x8/oxygen-loaders`. From examples:

| Prop value | Context |
|------------|---------|
| `"small"` | Inline / compact (cards, dropdowns) |
| `"default"` | General / full-page |
| `"large2x"` | Large / prominent display |
| `number` | Arbitrary pixel size passed directly |

_Source: Oxygen MCP · Extracted 2026-05-05_
