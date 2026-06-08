---
component: Input
status: draft
category: form_inputs
figma: "https://figma.com/design/5YihJ5WuDvnvrlrRMC4sBp?node-id=2072:14"
variants: [TextInput, TextArea, SearchInput]
props:
  - size: enum
  - suffix: string
  - iconLeft: ReactNode
  - iconRight: ReactNode
  - focus: boolean
  - fixed: boolean
  - hasError: boolean
  - isDisabled: boolean
  - isReadOnly: boolean
  - isRequired: boolean
  - fullWidth: boolean
  - inputRef: ref
  - testId: string
  - autoSuffixWidth: boolean
  - autoPrefixWidth: boolean
  - inputProps: object
subcomponents: []
related: ["[[TextField]]", "[[TextArea]]", "[[Select]]", "[[Radio]]", "[[Checkbox]]", "[[DateTimeSelector]]", "[[DateTimeRangeSelector]]", "[[Slider]]"]
patterns: ["[[Forms]]"]
tokens: ["[[token.ui.ui05]]", "[[token.hover.hover06]]", "[[token.interactive.disabled01]]", "[[token.interactive.focus01]]", "[[token.text.textColor01]]", "[[token.text.textColor02]]", "[[token.error.error01]]", "[[token.typography.body01]]", "[[token.typography.bodyBold01]]", "[[token.typography.body02]]", "[[token.typography.label01]]"]
spokes:
  - "[[Input.props]]"
  - "[[Input.anatomy]]"
  - "[[Input.tokens]]"
  - "[[Input.usage]]"
  - "[[Input.accessibility]]"
  - "[[Input.platform]]"
  - "[[Input.composition]]"
pipeline_stage: partial
audit_verdict: NO
tags: [component, form_inputs, interactive]
---

## Overview

Single-line text field for free-form user input. The Input canvas ships three Figma component sets — Text input, Text area, and Search input — all backed by the same `@8x8/oxygen-input` package. `Input` renders the raw field only; wrap with `TextField` for a complete form row with label, hint, and error region.

## Spokes

- [[Input.props]] — 16 props including size (enum), iconLeft/iconRight (ReactNode), isReadOnly (boolean); **1 CONFLICT** on isReadOnly × Search input
- [[Input.anatomy]] — 3 component sets (Text input, Text area, Search input), 8 sub-component element types, 8 interaction states
- [[Input.tokens]] — 11 tokens covering background (ui05, hover06, disabled01, focus01), text (textColor01, textColor02), error01, and 4 typography tokens
- [[Input.usage]] — 8 Do/Don't pairs covering label/placeholder, error state, size selection, icon semantics, required fields, isDisabled vs isReadOnly, placeholder contrast
- [[Input.accessibility]] — keyboard, ARIA, focus management; placeholder contrast ~4.97:1 PASS; focus ring ~5.54:1 PASS
- [[Input.platform]] — no PUI requirements
- [[Input.composition]] — raw field, wrap with [[TextField]]; 8 related components; ingredient of [[Forms]] pattern
