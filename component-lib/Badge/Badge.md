---
component: Badge
status: draft
package: "@8x8/oxygen-badge"
category: data_display
figma: "https://figma.com/file/5YihJ5WuDvnvrlrRMC4sBp?node-id=2565:14"
variants: [Primary, Secondary, AIBadge]
props:
  - children: ReactNode
  - type: enum
  - size: enum
  - isInner: boolean
  - testId: string
subcomponents: []
related: ["[[IconButton]]", "[[ListItem]]", "[[Icon]]"]
patterns: ["[[Notifications]]"]
tokens: ["[[token.notification.notification01]]", "[[token.text.textcolor04]]", "[[token.typography.labelbold01]]"]
spokes:
  - "[[Badge.props]]"
  - "[[Badge.anatomy]]"
  - "[[Badge.tokens]]"
  - "[[Badge.usage]]"
  - "[[Badge.accessibility]]"
  - "[[Badge.platform]]"
  - "[[Badge.composition]]"
tags: [component, data_display, display]
---

## Overview

Badge is a passive display component that surfaces a notification count, a presence dot, or a mention indicator on a host element (icon button, list item, wrapper). It is never interactive and never focusable — the parent element carries the accessible name. `AIBadge` is a companion export that pairs a star icon with text for AI-feature labelling.

> **Status: draft** — `figma-extract` was never run for Badge (blocker `SOURCE_GAP` GAP-001). Anatomy, composition, and several token bindings (`secondary`, `AIBadge`, spacing) remain stubbed pending Figma extraction.

## Spokes

- [[Badge.props]] — 5 Badge props (children, type, size, isInner, testId) plus AIBadge
- [[Badge.anatomy]] — STUB: Figma layer tree absent; counter/dot/mention types referenced but unverified
- [[Badge.tokens]] — primary `notification01` background + labelBold01 typography; secondary/AIBadge/spacing tokens stubbed
- [[Badge.usage]] — 5 Do/Don't pairs covering counter values, dot badges, Badge-vs-AIBadge, conditional visibility, accessibility (MCP-derived; no Figma pairs)
- [[Badge.accessibility]] — keyboard (none — not focusable), ARIA (`aria-hidden` + parent label), WCAG checklist (dark-mode contrast open)
- [[Badge.platform]] — no PUI requirements
- [[Badge.composition]] — STUB: positioned on [[IconButton]] / [[ListItem]]; AIBadge composes a star [[Icon]]
