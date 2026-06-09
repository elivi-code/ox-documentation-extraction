---
component: SkeletonBlock
status: draft
package: "@8x8/oxygen-skeletons"
category: feedback_status
figma: "https://figma.com/file/5YihJ5WuDvnvrlrRMC4sBp?node-id=31984:56109"
variants:
  - "40px - heading02"
  - "28px - heading01"
  - "24px - bulletList01"
  - "22px - body02"
  - "20px - body01"
  - "16px - label01"
  - "custom - image"
props:
  - size: enum
  - mode: enum
subcomponents: []
related:
  - "[[SkeletonCircle]]"
patterns: []
tokens:
  - "[[token.ui01]]"
  - "[[token.ui02]]"
  - "[[token.spacing03]]"
spokes:
  - "[[SkeletonBlock.props]]"
  - "[[SkeletonBlock.anatomy]]"
  - "[[SkeletonBlock.tokens]]"
  - "[[SkeletonBlock.usage]]"
  - "[[SkeletonBlock.accessibility]]"
  - "[[SkeletonBlock.platform]]"
  - "[[SkeletonBlock.composition]]"
tags: [component, feedback_status, loading]
---

## Overview

`SkeletonBlock` is a rectangular content placeholder that appears while text, images, or block-level elements are loading. It ships seven size variants whose names encode both height and the Oxygen text style being replaced (e.g. `20px - body01`, `custom - image`), eliminating layout shift when real content paints. Pair it with [[SkeletonCircle]] — exported from the same `@8x8/oxygen-skeletons` package — to skeleton avatars and icons in the same layout.

> **Draft status:** 1 CONFLICT (GAP-001 — SkeletonCircle `size` value format) and 7 SOURCE_GAPs (prop names, tokens, Figma enrichment) remain open. Props are Figma variant axes — React prop names unconfirmed (GAP-002).

---

## Spokes

- [[SkeletonBlock.props]] — 2 props (size, mode — Figma axes, React names unconfirmed via GAP-002); CONFLICT on SkeletonCircle size enum format (GAP-001)
- [[SkeletonBlock.anatomy]] — 14 variants across 7 sizes × 2 modes (Light/Dark), 0 interactive states; single leaf `div` with no children
- [[SkeletonBlock.tokens]] — 3 tokens (ui01, ui02, spacing03) covering animation fade, background fill, and text-line gap; border-radius (6px) hardcoded without token binding
- [[SkeletonBlock.usage]] — 6 Do/Don't pairs covering size matching, image vs text usage, spacing03, Block+Circle card combination, aria-busy, and prefers-reduced-motion
- [[SkeletonBlock.accessibility]] — keyboard (none), ARIA (aria-busy on parent), screen reader, animation (prefers-reduced-motion); all guidance inferred — unverified against implementation (GAP-010)
- [[SkeletonBlock.platform]] — no PUI requirements (display component; unconfirmed via MCP — GAP-004)
- [[SkeletonBlock.composition]] — leaf node, no subcomponents; sibling [[SkeletonCircle]]; used in card, list-row, and paragraph patterns
