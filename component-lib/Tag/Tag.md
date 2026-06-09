---
component: Tag
role: hub
pipeline_stage: doc_rewrite
status: draft
package: "@8x8/oxygen-tag"
category: data_display
figma: "https://www.figma.com/design/5YihJ5WuDvnvrlrRMC4sBp?node-id=8083:8359"
variants:
  - Standard Tag (7 colors × 2 types = 28 Figma variants)
  - Avatar Tag (5 colors × 3 types = 30 Figma variants)
props:
  - children: ReactNode
  - variant: enum
  - avatar: object
  - action: function
  - actionProps: object
  - hasError: boolean
  - isFocused: boolean
  - testId: string
subcomponents:
  - "[[CloseButton]]"
  - "[[Avatar]]"
related:
  - "[[Select]]"
patterns:
  - "[[RAG]]"
tokens:
  - "[[token.ui.ui01]]"
  - "[[token.ui.ui09]]"
  - "[[token.ui.ui10]]"
  - "[[token.ui.ui16]]"
  - "[[token.ui.ui17]]"
  - "[[token.ui.ui18]]"
  - "[[token.warning.warning01]]"
  - "[[token.text.textcolor01]]"
  - "[[token.text.textcolor06]]"
  - "[[token.text.textcolor07]]"
  - "[[token.interactive.focus01]]"
  - "[[token.ui.ui06]]"
  - "[[token.error.error01]]"
  - "[[token.typography.label01]]"
  - "[[token.spacing.spacing01]]"
  - "[[token.spacing.spacing02]]"
  - "[[token.spacing.spacing03]]"
spokes:
  - "[[Tag.props]]"
  - "[[Tag.anatomy]]"
  - "[[Tag.tokens]]"
  - "[[Tag.usage]]"
  - "[[Tag.accessibility]]"
  - "[[Tag.platform]]"
  - "[[Tag.composition]]"
audit: "[[Tag-audit]]"
tags: [component, data_display, interactive]
---

## Overview

Pill-shaped label component used to categorize content, display metadata, filter items, or indicate status. Two visual forms — Standard Tag (with optional leading icon) and Avatar Tag (with fixed avatar) — are selected automatically by the presence of the `avatar` prop. Either form can be display-only or carry a remove (×) button via the `action` prop. The `variant` prop controls background and text color across seven values on Standard Tag and five on Avatar Tag.

## Spokes

- [[Tag.props]] — 8 props including variant, avatar, action, actionProps
- [[Tag.anatomy]] — Standard Tag (5 elements) and Avatar Tag (6 elements); 7 Standard variants / 5 Avatar variants; 3 states (default, withAction, withActionError)
- [[Tag.tokens]] — 17 tokens covering background, text color, focus ring, error border, typography, spacing
- [[Tag.usage]] — 6 Do/Don't pairs covering label length, form selection, RAG colors, accessibility, tag spacing, hasError semantics (editorial — pending Figma Do/Don't card frames)
- [[Tag.accessibility]] — keyboard, ARIA, focus management (inferred — no official Oxygen a11y source)
- [[Tag.platform]] — no PUI requirements
- [[Tag.composition]] — sub-components [[CloseButton]] and [[Avatar]]; inside [[Select]] multi-selection; RAG pattern with Standard Tag variants
