---
component: Label
status: partial
category: data_display
figma: "https://www.figma.com/design/5YihJ5WuDvnvrlrRMC4sBp?node-id=22230:37448"
variants: [Default, Required, Disabled, WithInfoBox, WithActionLink]
props:
  - value: ReactNode
  - htmlFor: string
  - isRequired: boolean
  - isDisabled: boolean
  - shouldWrapText: boolean
  - showTooltipOnOverflow: boolean
  - action: function
  - actionLabel: string
  - actionTarget: ActionTarget
  - otherActionProps: object
  - infoBoxText: ReactNode
  - infoBoxShowOn: enum
  - infoBoxButtonLabel: string
  - testId: string
subcomponents: ["[[Icon Button]]"]
related: ["[[Input]]", "[[Checkbox]]", "[[Select]]", "[[Button]]"]
patterns: ["[[Form]]"]
tokens: ["[[text/textColor01]]", "[[error/error01]]", "[[typography/body01]]", "[[typography/bodyBold01]]"]
spokes:
  - "[[Label.props]]"
  - "[[Label.anatomy]]"
  - "[[Label.tokens]]"
  - "[[Label.usage]]"
  - "[[Label.accessibility]]"
  - "[[Label.platform]]"
  - "[[Label.composition]]"
tags: [component, data_display, forms, interactive]
---

## Overview

Label renders as a native HTML `<label>` element that programmatically names a form control. When paired with an Input, Checkbox, or Select via `htmlFor`, it provides click-to-focus, screen-reader association, and required/disabled signalling. Optional features include an inline action link, an info box tooltip, and text overflow handling.

## Spokes

- [[Label.props]] — 14 props including value, htmlFor, isRequired; open stubs: `infoBoxShowOn` enum values (GAP-001), `action` type signature (GAP-002)
- [[Label.anatomy]] — 4 elements (H Stack, label text, required asterisk, Icon Button slot); 1 variant axis (mode: light/dark); 5 states; open stubs: GAP-015 (disabled Figma variant missing), GAP-016 (wrap/overflow no Figma variants)
- [[Label.tokens]] — 2 color tokens (`text/textColor01`, `error/error01`); 2 typography tokens (`typography/body01`, `typography/bodyBold01` at 14px); 3 hardcoded spacing values
- [[Label.usage]] — 8 Do/Don't pairs covering htmlFor association, required indicator, disabled pairing, truncation strategy, action link, info icon, label copy, placement; editorial (no published docs page or Figma examples page)
- [[Label.accessibility]] — keyboard, ARIA, focus management; WCAG 2.1 AA checklist (1.3.1, 1.4.3, 2.1.1, 2.4.6, 3.3.2, 4.1.2); content inferred — no MCP/Figma annotations (GAP-010, GAP-011)
- [[Label.platform]] — no PUI requirements
- [[Label.composition]] — Icon Button as internal sub-component (info slot); common pairings with Input, Select; Checkbox bundles its own label
