---
component: TimeSelector
status: draft
package: "@8x8/oxygen-time-selector"
category: date_time
figma: "https://figma.com/file/5YihJ5WuDvnvrlrRMC4sBp?node-id=32598:56953"
variants:
  - Small
  - Medium
  - Large (design-only — not in code API)
props:
  - value: TimeValue
  - onChange: function
  - onOpen: function
  - onClose: function
  - size: TimeSelectorSize
  - timeDisplayFormat: string
  - placeholder: string
  - hasError: boolean
  - isDisabled: boolean
  - isLeftIconVisible: boolean
  - iconLeft: ReactNode
  - id: string
  - testId: string
  - portalRef: RefObject
subcomponents:
  - "[[Icon Button]]"
related:
  - "[[Calendar]]"
  - "[[TextField]]"
  - "[[Select]]"
  - "[[Radio]]"
patterns:
  - "[[Forms]]"
tokens:
  - "[[token.ui.ui05]]"
  - "[[token.interactive.disabled01]]"
  - "[[token.interactive.focus01]]"
  - "[[token.error.error01]]"
  - "[[token.text.textColor01]]"
  - "[[token.text.textColor02]]"
  - "[[token.interactive.disabled04]]"
  - "[[token.typography.body01]]"
  - "[[token.typography.bodybold01]]"
  - "[[token.typography.label01]]"
  - "[[token.typography.font-family.sans]]"
spokes:
  - "[[TimeSelector.props]]"
  - "[[TimeSelector.anatomy]]"
  - "[[TimeSelector.tokens]]"
  - "[[TimeSelector.usage]]"
  - "[[TimeSelector.accessibility]]"
  - "[[TimeSelector.platform]]"
  - "[[TimeSelector.composition]]"
pipeline_stage: draft
audit_verdict: "NO"
audit_note: "2 unresolved CONFLICTs (GAP-001, GAP-002) — Size=Large present in Figma but absent from code API; Figma and code defaults differ. Proceeding with CONFLICT markers."
tags:
  - oxygen
  - component/TimeSelector
  - role/hub
  - stage/draft
  - category/date_time
---

## Overview

TimeSelector is a composite time-of-day input combining a text field with a dropdown picker — users can open the picker to select a time or type directly into the input. It ships as a controlled component (`value` + `onChange`) with optional label, hint, left icon, and error state wrappers following the Forms pattern. Use it in scheduling flows, report filters, and forms wherever a specific hour-and-minute value is required.

> ⚠️ **2 unresolved CONFLICTs:** Figma exposes `Size=Large` (48 px input, `$body02` typography) as the Figma default, but the code `TimeSelectorSize` enum only accepts `"small" | "default"` (where `"default"` ≡ Figma Medium). The Figma and code defaults therefore differ. See GAP-001 / GAP-002 in the audit.

---

## Spokes

- [[TimeSelector.props]] — 14 props including value, onChange, size, hasError, isDisabled
- [[TimeSelector.anatomy]] — 4 elements (label, input, hint, error area) across 3 sizes × 4 states (rest, focus, disabled, error); Size=Large is design-only — CONFLICTs GAP-001/002 unresolved
- [[TimeSelector.tokens]] — 11 tokens covering background, border, text, and typography; names sourced from Figma variable casing (GAP-007 — cross-reference against OX package before publishing)
- [[TimeSelector.usage]] — 6 Do/Don't pairs covering when to use, value control, format+timezone, error state, disabled state, sizing
- [[TimeSelector.accessibility]] — keyboard, ARIA, focus management (all inferred — GAP-008; WCAG 2.1 AA checklist included)
- [[TimeSelector.platform]] — no PUI requirements
- [[TimeSelector.composition]] — Icon Button structural sub-component in label area; used inside Forms pattern; pairs with Calendar for date+time
