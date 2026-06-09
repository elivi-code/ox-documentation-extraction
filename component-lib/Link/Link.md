---
component: Link
status: draft
version: stable
category: navigation
figma: "https://figma.com/file/5YihJ5WuDvnvrlrRMC4sBp?node-id=58315:113"
variants:
  - Inline
  - Standalone
  - Inverted
  - Chat
props:
  - children: ReactNode
  - href: string
  - icon: ReactNode
  - isChat: boolean
  - standalone: false
  - size: never
  - testId: string
subcomponents: []
related:
  - "[[Button]]"
  - "[[Icon]]"
patterns:
  - "[[Form]]"
  - "[[Typography]]"
tokens:
  - "[[token.action08]]"
  - "[[token.hover07]]"
  - "[[token.action10]]"
  - "[[token.hover20]]"
  - "[[token.active14]]"
  - "[[token.active17]]"
  - "[[token.textColor08]]"
  - "[[token.focus01]]"
  - "[[token.focus02]]"
  - "[[token.ui06]]"
  - "[[token.ui07]]"
  - "[[token.action05]]"
  - "[[token.action07]]"
  - "[[token.body02]]"
spokes:
  - "[[Link.props]]"
  - "[[Link.anatomy]]"
  - "[[Link.tokens]]"
  - "[[Link.usage]]"
  - "[[Link.accessibility]]"
  - "[[Link.platform]]"
  - "[[Link.composition]]"
tags:
  - component
  - navigation
  - interactive
---

## Overview

`Link` is a navigation component wrapping the HTML `<a>` element. It provides two structural variants: **Inline**, which integrates with surrounding text by inheriting its typography, and **Standalone**, which has explicit size control (Small/Large) using the `$body02` token. Both variants support an optional icon slot and a chat-surface mode (`isChat`) that switches to accessible color tokens for chat bubble surfaces.

## Spokes

- [[Link.props]] — 7 props including children, href, icon; standalone/size reflect inline-only Storybook export (GAP-003 stub)
- [[Link.anatomy]] — 3 elements (label, icon slot, focus ring) across 2 size variants (Small/Large) and 4 states; inline variant undocumented in Figma (GAP-013)
- [[Link.tokens]] — 14 tokens covering default/inverted/chat color, focus ring, typography; $action05 and $body02 values pending MCP lookup
- [[Link.usage]] — 5 Do/Don't pairs covering link-vs-button, external links, chat surface, inline-vs-standalone, icon usage
- [[Link.accessibility]] — keyboard, ARIA, focus; content inferred from HTML semantics (not officially sourced, GAP-019)
- [[Link.platform]] — no PUI requirements
- [[Link.composition]] — icon slot (ReactNode); related to [[Button]], [[Form]], [[Typography]]
