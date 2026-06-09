---
component: Select
status: draft
category: form_inputs
figma: "https://figma.com/file/5YihJ5WuDvnvrlrRMC4sBp?node-id=2105:2"
variants: [Light, Dark, Large, Medium, Small, Rest, Hover, Focus, Disabled, Read-only, Open, Error]
props:
  - options: "SelectOption[]"
  - action: "(() => void) | string"
  - actionLabel: "string | number"
  - components: object
  - forwardedRef: "React.Ref<any>"
  - hasCheckbox: boolean
  - hasError: boolean
  - hasIcons: boolean
  - hasSelectableInput: boolean
  - hasShortMultiDisplay: boolean
  - hideSelectedOptions: boolean
  - iconLeft: "React.ComponentType | React.ReactNode"
  - infoBoxText: string
  - infoBoxButtonLabel: string
  - isAsync: boolean
  - isClearable: boolean
  - isCreatable: boolean
  - isDisabled: boolean
  - isLoading: boolean
  - isMulti: boolean
  - isRequired: boolean
  - labelValue: string
  - loadingMessage: string
  - loadOptions: function
  - multipleSelectMaxRows: number
  - noOptionsMessage: function
  - onBlur: function
  - onChange: function
  - otherActionProps: object
  - placeholder: "React.ReactNode"
  - shouldWrapLabel: boolean
  - size: enum
  - testId: string
  - inputProps: "React.InputHTMLAttributes<HTMLInputElement>"
  - theme: object
  - menuPortalTarget: "HTMLElement | null"
  - menuPlacement: enum
subcomponents: ["VirtualMenuList", "ClearIndicator", "DropdownIndicator", "SingleValue", "MultiValue", "ValueContainer"]
related: ["[[Radio]]", "[[Checkbox]]", "[[ToggleButton]]", "[[Tooltip]]", "[[Modal]]"]
patterns: ["[[Form]]"]
tokens: ["[[token.ui01]]"]
spokes:
  - "[[Select.props]]"
  - "[[Select.anatomy]]"
  - "[[Select.tokens]]"
  - "[[Select.usage]]"
  - "[[Select.accessibility]]"
  - "[[Select.platform]]"
  - "[[Select.composition]]"
pipeline_stage: doc_rewrite
audit_verdict: NO
open_conflicts:
  - "GAP-002: isAsync type — boolean (get-component-info) vs IsAsync (get-component-props)"
  - "GAP-003: ref= used in examples vs forwardedRef= in props table"
tags:
  - oxygen
  - component/Select
  - role/hub
  - stage/doc_rewrite
  - category/form_inputs
---

## Overview

A select element for picking one or multiple options from a popover list, built on [react-select](https://react-select.com/components) — all react-select props pass through. Use for lists of more than five options, searchable or async-loaded content, and multi-select chip patterns. For five or fewer options use [[Radio]] (single) or [[Checkbox]] (multiple) instead.

> ⚠️ **Two unresolved CONFLICTs:** `isAsync` type is `boolean` in one MCP endpoint and `IsAsync` in another (GAP-002); `forwardedRef` is documented in props but examples use standard `ref=` (GAP-003). Resolve before publishing externally.

## Spokes

- [[Select.props]] — 37 props including options, isAsync, isMulti, hasError, size, menuPortalTarget; 2 CONFLICTs (isAsync type, ref/forwardedRef); 1 manual gap (SelectOption type shape)
- [[Select.anatomy]] — 5 variant axes (~80 Figma variants), 9 states; anatomy derived from metadata only — no figma.md yet (STUB:GAP-001)
- [[Select.tokens]] — 1 confirmed token (ui01 — selected-option row background); 7 state tokens pending figma-extract (STUB:GAP-011)
- [[Select.usage]] — 8 Do/Don't pairs covering option-count threshold, multi-select, async loading, Select-in-Modal, labelling, error pairing, clearability, placeholder length
- [[Select.accessibility]] — keyboard, ARIA, focus; inferred from react-select + WAI-ARIA combobox pattern; DOM confirmation pending (STUB:GAP-012)
- [[Select.platform]] — no PUI requirements
- [[Select.composition]] — 6 sub-component overrides via `components` prop; member of Form and Modal patterns
