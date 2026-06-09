---
parent: "[[Spinner]]"
section: tokens
component: Spinner
pipeline_stage: draft
siblings:
  - "[[Spinner]]"
  - "[[Spinner.props]]"
  - "[[Spinner.anatomy]]"
  - "[[Spinner.usage]]"
  - "[[Spinner.accessibility]]"
  - "[[Spinner.platform]]"
  - "[[Spinner.composition]]"
tags:
  - oxygen
  - component/Spinner
  - role/tokens
---

## Theme tokens

<!-- STUB:GAP-006 source="Resolve token bindings from UI-Foundations library (file key iVY5nI8JAxM05Apnnvozzs) using figma_execute + getVariableByIdAsync on the Spinner variant nodes — expected categories: stroke colour, track colour, text colour, animation timing" -->

No dedicated theme tokens were returned by the Oxygen MCP for the `Spinner` component or the `loaders` package. The Variables API required an Enterprise plan and returned a permissions error; the figma-console Desktop Bridge was offline during extraction.

The spinner's visual appearance (stroke colour, stroke width, animation speed) is controlled via the `strokeWidth` prop and inherits from the surrounding theme context rather than component-level tokens.

**Known gap:** Token names for spinner colours should be resolved from the UI-Foundations token library (file key `iVY5nI8JAxM05Apnnvozzs`) using `getVariableByIdAsync` on the spinner node properties.

## Color & token bindings (Figma)

<!-- STUB:GAP-007 source="Re-run figma-extract for Spinner once Variables API access or Desktop Bridge is available — populate stroke colour, track colour, and text colour token bindings from UI-Foundations library" -->

Token bindings for the Spinner stroke, track, and text colours could not be extracted from Figma. Both the Variables API and the figma-console Desktop Bridge were unavailable during extraction.

### Text styles

<!-- STUB:GAP-009 source="Resolve text style token (likely a body/caption token from UI-Foundations library) alongside GAP-007 resolution" -->

The typography token for the supporting text label was not extracted — the Styles API returned 0 styles for this file.

## Size reference

Named sizes are resolved from the `spinnerSize` enum inside `@8x8/oxygen-loaders`:

| Prop value | Context |
|------------|---------|
| `"small"` | Inline / compact (cards, dropdowns) |
| `"default"` | General / full-page |
| `"large2x"` | Large / prominent display |
| `number` | Arbitrary pixel size passed directly |

_Source: Oxygen MCP · Extracted 2026-05-05_
