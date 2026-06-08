---
component: TextArea
status: draft
category: form_inputs
package: "@8x8/oxygen-textarea"
figma: "https://www.figma.com/design/5YihJ5WuDvnvrlrRMC4sBp/UI-components?node-id=21562-34985"
variants:
  - Mode: [Light, Dark]
  - Size: [Large, Medium, Small]
  - State: [Rest, Focus, Disabled]
  - Error: [False, True]
  - ReadOnly: [False, True]
  - Filled: [False, True]
props:
  - theme: Partial<Theme>
  - ref: React.Ref<HTMLTextAreaElement>
  - id: string
  - name: string
  - placeholder: string
  - autoComplete: string
  - autoFocus: boolean
  - value: string
  - rows: number
  - cols: number
  - minLength: number
  - maxLength: number
  - resize: enum
  - testId: string
  - isDisabled: boolean
  - isReadOnly: boolean
  - hasError: boolean
  - onBlur: function
  - onChange: function
  - onFocus: function
  - onKeyUp: function
  - onKeyDown: function
  - aria-label: string
  - aria-labelledby: string
  - aria-describedby: string
  - aria-invalid: boolean|string
  - aria-required: boolean|string
  - required: boolean
subcomponents: []
related:
  - "[[TextField]]"
patterns: []
tokens:
  - "[[token.ui.ui05]]"
  - "[[token.interactive.disabled01]]"
  - "[[token.interactive.focus01]]"
  - "[[token.error.error01]]"
  - "[[token.text.textcolor01]]"
  - "[[token.text.textcolor02]]"
  - "[[token.interactive.disabled04]]"
  - "[[token.typography.body01]]"
  - "[[token.typography.bodyBold01]]"
  - "[[token.typography.body02]]"
  - "[[token.typography.label01]]"
spokes:
  - "[[TextArea.props]]"
  - "[[TextArea.anatomy]]"
  - "[[TextArea.tokens]]"
  - "[[TextArea.usage]]"
  - "[[TextArea.accessibility]]"
  - "[[TextArea.platform]]"
  - "[[TextArea.composition]]"
audit: "[[textarea-audit]]"
tags:
  - oxygen
  - component/TextArea
  - category/form_inputs
  - status/draft
---

## Overview

Multi-line free-form text input built on a native `<textarea>` element. Supports controlled and uncontrolled value patterns, configurable resize behaviour, error and read-only states, and a character-count API via `minLength`/`maxLength`. Light and dark mode are controlled at the `OxygenProvider` theme level — there is no `mode` prop. The component renders only the input box; label, hint text, and error message are consumer-composed external elements.

## Spokes

- [[TextArea.props]] — 28 props including value, rows, hasError, resize, isDisabled, aria-label, aria-invalid
- [[TextArea.anatomy]] — 17 elements across 72 variant combinations (Mode × Size × State × Error × ReadOnly × Filled), 5 states
- [[TextArea.tokens]] — 11 tokens covering background, border, label, placeholder/input, hint, error, disabled; dark mode values resolved
- [[TextArea.usage]] — 8 Do/Don't pairs covering input type, labelling, hints, readonly vs disabled, error state, rows sizing, resize, character counters (draft — pending Figma examples page)
- [[TextArea.accessibility]] — keyboard, ARIA, focus management
- [[TextArea.platform]] — no PUI requirements
- [[TextArea.composition]] — no Oxygen subcomponents; composed with external `<label>`, hint, and error elements; single-line alternative is [[TextField]]

## Open items

| ID | Type | Spoke | Summary |
|----|------|-------|---------|
| GAP-007 | CONFLICT | anatomy, props | Figma `Size` axis (Large/Medium/Small) has no `size` prop — confirm rows/cols intent with component owner |
| GAP-008 | CONFLICT | props | Figma `Mode` axis (Light/Dark) has no `mode` prop — confirm theme-provider control |
| GAP-009 | CONFLICT | anatomy, props | Figma `Filled` axis has no Oxygen prop — confirm derived state from `value !== ''` |
| GAP-001 | STUB | usage | `textarea-usage.md` absent — run `figma-extract-usage` once Figma examples page exists |
| GAP-004 | STUB | tokens | `tokens.md` dark mode note is stale — dark values resolved in figma.md but tokens.md needs re-extraction |
| GAP-006 | SKIP | tokens | Filled=True input text color not verified — inspect Figma node 21722:35590 |
| GAP-011 | STUB | anatomy | Medium/Small input box heights are approximate — verify via `get_design_context` |
