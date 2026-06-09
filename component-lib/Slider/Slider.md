---
component: Slider
status: draft
category: form_inputs
package: "@8x8/oxygen-slider"
figma: "https://www.figma.com/file/5YihJ5WuDvnvrlrRMC4sBp?node-id=22902:37514"
variants:
  - Single-thumb
  - Range (isMultiple)
  - Track-draggable range (isMultiple + isTrackDraggable)
props:
  - value: RangeType
  - minValue: number
  - maxValue: number
  - step: number
  - isDisabled: boolean
  - isMultiple: true
  - isTrackDraggable: boolean
  - ariaLabel: string
  - onDragStart: "() => void"
  - onDragEnd: "() => void"
  - onChange: "(props: RangeType) => void"
  - expandTrackAreaBy: string
  - expandKnobAreaBy: string
  - testId: string
subcomponents: []
related:
  - "[[Dropdown]]"
  - "[[Switch]]"
patterns:
  - "[[AudioVolume]]"
tokens:
  - "[[token.ui.ui04]]"
  - "[[token.actions.action01]]"
  - "[[token.interactive.disabled04]]"
  - "[[token.ui.ui03]]"
  - "[[token.interactive.focus01]]"
  - "[[token.ui.ui06]]"
  - "[[token.text.textcolor01]]"
  - "[[token.interactive.disabled01]]"
spokes:
  - "[[Slider.props]]"
  - "[[Slider.anatomy]]"
  - "[[Slider.tokens]]"
  - "[[Slider.usage]]"
  - "[[Slider.accessibility]]"
  - "[[Slider.platform]]"
  - "[[Slider.composition]]"
audit_verdict: PARTIAL
pipeline_stage: spec_ready
tags:
  - oxygen
  - component/Slider
  - role/hub
  - stage/spec_ready
  - category/form_inputs
---

## Overview

`Slider` (`@8x8/oxygen-slider`) lets users select a value on a horizontal track by dragging a thumb or clicking the track. The canonical pattern is audio volume control — the Figma reference is literally the "Audio Volume" layout (left icon → track → right icon). It supports a single-thumb mode, a two-thumb range mode (`isMultiple`), and a draggable filled track (`isTrackDraggable`). `value` is the only required prop; the component is fully controlled.

> **Status: draft.** `slider-figma.md` is absent (GAP-001, blocker) — the anatomy spoke is stub-populated from partial Figma data embedded during combined extraction. Run `figma-extract` against node `22902:37514` to resolve and upgrade to `partial` or `complete`.

## Spokes

- [[Slider.props]] — 14 props including value (RangeType), isMultiple, isDisabled; 5 props have empty source descriptions (GAP-004); 13 of 14 defaults undocumented (GAP-003)
- [[Slider.anatomy]] — STUB: slider-figma.md absent (GAP-001 blocker); 7 known elements (label, left icon, track, active fill, inactive fill, thumb, right icon), 3 functional variants, 5 states derived from partial Figma data
- [[Slider.tokens]] — 8 named tokens covering active track, focus ring, label, typography; 2 SVG-asset stubs (inactive track background GAP-005, thumb fill/stroke GAP-006); full state × mode matrix present
- [[Slider.usage]] — 6 Do/Don't pairs (editorial draft — no Figma examples page; WARN-003) covering control selection, precision vs. approximation, range mode, labelling, touch hit areas, value readout
- [[Slider.accessibility]] — keyboard (8 keys), ARIA (6 attributes including aria-valuetext added GAP-007), focus ring (Light + Dark), WCAG 2.1 AA checklist (9 criteria)
- [[Slider.platform]] — no PUI requirements (confirmed by engineer)
- [[Slider.composition]] — no subcomponents; Audio Volume is the canonical layout pattern; related to [[Dropdown]] (discrete options) and [[Switch]] (binary)
