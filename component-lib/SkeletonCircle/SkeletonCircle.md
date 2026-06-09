---
component: SkeletonCircle
status: draft
package: "@8x8/oxygen-skeletons"
category: feedback_status
figma: "https://figma.com/file/5YihJ5WuDvnvrlrRMC4sBp?node-id=31984:56124"
variants:
  - "xlarge (80px)"
  - "large (48px)"
  - "medium (40px)"
  - "small (32px / 28px)"
  - "xsmall (24px / 22px / 20px / 16px)"
props:
  - mode: enum
  - size: enum
subcomponents: []
related:
  - "[[SkeletonBlock]]"
  - "[[Spinner]]"
patterns: []
tokens:
  - "[[--ui/ui02]]"
  - "[[ui01]]"
  - "[[spacing03]]"
spokes:
  - "[[SkeletonCircle.props]]"
  - "[[SkeletonCircle.anatomy]]"
  - "[[SkeletonCircle.tokens]]"
  - "[[SkeletonCircle.usage]]"
  - "[[SkeletonCircle.accessibility]]"
  - "[[SkeletonCircle.platform]]"
  - "[[SkeletonCircle.composition]]"
role: hub
pipeline_stage: draft
audit_verdict: NO
siblings:
  - "[[SkeletonCircle.props]]"
  - "[[SkeletonCircle.anatomy]]"
  - "[[SkeletonCircle.tokens]]"
  - "[[SkeletonCircle.usage]]"
  - "[[SkeletonCircle.accessibility]]"
  - "[[SkeletonCircle.platform]]"
  - "[[SkeletonCircle.composition]]"
  - "[[SkeletonCircle-audit]]"
tags:
  - oxygen
  - component/SkeletonCircle
  - role/hub
  - stage/draft
  - category/feedback_status
---

## Overview

`SkeletonCircle` is a fully-rounded content placeholder from `@8x8/oxygen-skeletons` that appears while an **avatar** or **individual icon** is loading. It is the circular counterpart to [[SkeletonBlock]] — both components share the `--ui/ui02` fill token and animate between `ui01` and `ui02` to convey activity. The consumer is responsible for mounting and unmounting the skeleton; the component itself is purely presentational with no loading-state awareness.

> **Draft status:** 1 CONFLICT (GAP-001 — `size` prop format unverified against `@8x8/oxygen-skeletons` source) and multiple SOURCE_GAPs remain open. Resolve the CONFLICT before treating any prop documentation as authoritative.

---

## Spokes

- [[SkeletonCircle.props]] — 2 props (mode, size) — **CONFLICT**: React format unverified; 9 Figma size values 80px→16px
- [[SkeletonCircle.anatomy]] — 18 variants across 9 size × 2 mode axes; single leaf node, no children, no boolean toggles
- [[SkeletonCircle.tokens]] — 3 tokens (--ui/ui02 fill, ui01/ui02 animation); spacing03 (8px gap); 1 hardcoded value (100px border-radius); all from CSS fallback, unconfirmed from source library
- [[SkeletonCircle.usage]] — 6 Do/Don't pairs covering sizing, shape selection, list consistency, pairing with Block, aria-busy pattern, reduced motion
- [[SkeletonCircle.accessibility]] — keyboard (non-interactive), ARIA (aria-busy on parent), screen reader (parent label), animation (prefers-reduced-motion)
- [[SkeletonCircle.platform]] — no PUI requirements
- [[SkeletonCircle.composition]] — no subcomponents; used alongside [[SkeletonBlock]] in contact rows, comment cards, and list items
