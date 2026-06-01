---
parent: "[[AlertBanner]]"
component: AlertBanner
section: anatomy
role: spoke-anatomy
pipeline_stage: rewritten
audit_verdict: NO
tags:
  - oxygen
  - component/AlertBanner
  - role/spoke/anatomy
  - stage/rewritten
---

# AlertBanner — Anatomy

## Element structure

Extracted from the Figma layer tree (component set `13899:15489`).

| # | Type | Name | Role | Notes |
|---|------|------|------|-------|
| 1 | frame (COMPONENT_SET) | Alert banner | Structural — top-level container | Dashed-border Figma component-set boundary; 4 variants inside |
| 2 | component | mode=light, breakpoint=> 576 | Variant | Desktop light; HORIZONTAL layout; 1200 × 56 px |
| 3 | component | mode=dark, breakpoint=> 576 | Variant | Desktop dark; HORIZONTAL layout; 1200 × 56 px |
| 4 | component | mode=light, breakpoint=< 576 | Variant | Mobile light; VERTICAL layout; 576 × 104 px |
| 5 | component | mode=dark, breakpoint=< 576 | Variant | Mobile dark; VERTICAL layout; 576 × 104 px |
| 6 | instance | Warning icon | Content element — fixed | Circle warning icon; accessible label exposed via `iconAriaLabel` prop |
| 7 | text / frame | Message (children) | Content element — React children slot | Body text; maps to `children` prop |
| 8 | instance | Action button | Optional slot | Secondary button; shown only when `actionText` is set |

<!-- STUB:GAP-001 source="Run figma-extract with the Figma Desktop Bridge plugin active, or manually inspect node 13899:15489 children in the Figma file to confirm inner anatomy. Rows 6–8 are inferred from screenshot and Oxygen props." -->

## Variant axes

| Property | Values | Default |
|----------|--------|---------|
| `mode` | light, dark | light |
| `breakpoint` | > 576, < 576 | > 576 |

These axes are design-time layout aids only — no consumer-facing prop. See [[AlertBanner.props]] for the API surface and CONFLICT-001 for the open question on automatic handling.

## Boolean toggles

| Property | Default | Notes |
|----------|---------|-------|
| Action button visible | false (hidden) | Shown when `actionText` prop is provided |

<!-- STUB:GAP-002 source="Confirm the Figma boolean property name (e.g. 'Show action', 'hasAction') via Desktop Bridge and update Boolean toggles entry. Name inferred from screenshot behaviour." -->

## Layout direction by variant

| Variant | Width | Height | Direction |
|---------|-------|--------|-----------|
| breakpoint > 576 | 1200 px | 56 px | HORIZONTAL — icon · message · button in a single row |
| breakpoint < 576 | 576 px | 104 px | VERTICAL — icon + message stacked above button |

Auto-layout sizing: `layoutSizingHorizontal = FIXED`, `layoutSizingVertical = HUG` (desktop); `counterAxisSizingMode = FIXED` (mobile).

<!-- STUB:GAP-010 source="Inspect auto-layout cross-axis and primary-axis alignment on variant frames in Figma. Children not resolved in API response." -->

## Interaction states

The component set contains only `mode` and `breakpoint` variant axes. No hover, focus, pressed, or loading states were found in the Figma layer tree. The action button (Secondary button) inherits its own interaction states from the Button component.

## Sidebar annotation frame

A non-component documentation frame at `48956:2083` (off-canvas) contains a "Stable" status badge, links to Storybook, and a support contact. This frame is Figma-side annotation only — not part of the rendered component.
