---
component: ProgressBar
status: partial
package: "@8x8/oxygen-loaders"
category: feedback_status
figma: "https://www.figma.com/design/5YihJ5WuDvnvrlrRMC4sBp?node-id=30880:55942"
variants:
  - loading
  - complete
props:
  - value: number
  - size: "enum | number | string"
  - text: string
  - fullWidth: boolean
  - testId: string
subcomponents: []
related:
  - "[[Spinner]]"
  - "[[SkeletonBlock]]"
  - "[[Toast]]"
  - "[[AlertBanner]]"
patterns: []
tokens:
  - "[[token.ui.ui01]]"
  - "[[token.actions.action04]]"
  - "[[token.success.success01]]"
  - "[[token.text.textcolor01]]"
  - "[[token.typography.body01]]"
spokes:
  - "[[ProgressBar.props]]"
  - "[[ProgressBar.anatomy]]"
  - "[[ProgressBar.tokens]]"
  - "[[ProgressBar.usage]]"
  - "[[ProgressBar.accessibility]]"
  - "[[ProgressBar.platform]]"
  - "[[ProgressBar.composition]]"
pipeline_stage: spec_ready
audit_verdict: YES
tags:
  - oxygen
  - component/ProgressBar
  - role/hub
  - stage/spec_ready
  - category/feedback_status
---

## Overview

ProgressBar communicates the status of an ongoing, determinate process through a horizontal fill (0–100%). Use it when the application can supply a real percentage — for uploads, downloads, or multi-step jobs with measurable progress. It is a passive display component: it does not accept keyboard focus and has no interaction states beyond the loading-to-complete visual transition (blue fill → green fill at `value === 100`).

## Spokes

- [[ProgressBar.props]] — 5 props including value, size, text, fullWidth
- [[ProgressBar.anatomy]] — 4 elements across 4 variants (2 status × 2 mode), 2 states
- [[ProgressBar.tokens]] — 5 tokens covering track background, loading fill, complete fill, label color, label typography
- [[ProgressBar.usage]] — 5 Do/Don't pairs covering determinate-only use, accessible names, color-only state, update cadence, completion label (editorial — WARN-003)
- [[ProgressBar.accessibility]] — keyboard (none), ARIA (role, aria-valuenow/min/max), labelling requirements; WCAG 1.4.11 track-bg contrast flag
- [[ProgressBar.platform]] — no PUI requirements
- [[ProgressBar.composition]] — no subcomponents; common with Spinner, SkeletonBlock, Toast
