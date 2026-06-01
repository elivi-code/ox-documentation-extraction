---
component: Button
status: draft
package: "@8x8/oxygen-button"
category: interaction
figma: "https://figma.com/file/5YihJ5WuDvnvrlrRMC4sBp?node-id=15653:16329"
variants: [primary, secondary, tertiary, tertiaryReversed, text, success, destructive]
props:
  - children: ReactNode
  - variant: ButtonVariant
  - size: ButtonSize
  - iconLeft: ReactNode
  - iconRight: ReactNode
  - isActive: boolean
  - isDisabled: boolean
  - isCircular: boolean
  - isDestructive: boolean
  - testId: string
  - theme: object
subcomponents: ["[[ButtonGroup]]", "[[DropdownButton]]", "[[IconButton]]"]
related: ["[[Tooltip]]", "[[Popover]]", "[[TextLink]]"]
patterns: ["[[Form]]", "[[Toolbar]]", "[[Dialog]]"]
tokens: ["[[token.action01]]", "[[token.action02]]", "[[token.action03]]", "[[token.hover15]]", "[[token.active14]]", "[[token.ui01]]", "[[token.textColor09]]", "[[token.disabled01]]", "[[token.disabled04]]"]
spokes:
  - "[[Button.props]]"
  - "[[Button.anatomy]]"
  - "[[Button.tokens]]"
  - "[[Button.usage]]"
  - "[[Button.accessibility]]"
  - "[[Button.platform]]"
  - "[[Button.composition]]"
tags: [component, interaction, actions, oxygen, component/Button]
---

# Button

## Overview

Triggers an action — submitting a form, opening a dialog, applying a setting, or changing state. The most visible affordance for "this is something you can do"; visual weight, colour, and placement together signal how important an action is. Primary actions use `variant="primary"` (one per surface); supporting actions use Secondary or Text. Ships alongside `ButtonGroup`, `DropdownButton`, and `IconButton`.

> ⛔ **Status: draft.** 3 unresolved figma/token CONFLICTs (GAP-001, GAP-002, GAP-003) remain — see [[Button.tokens]]. The token tables are authoritative for **Primary** only until a designer/token owner resolves them.

## Spokes

- [[Button.props]] — 11 Button props (children, variant, size …) plus ButtonGroup, DropdownButton, IconButton; ButtonVariant (7), ButtonSize (4), IconButtonSize (11) enums
- [[Button.anatomy]] — 4 elements, 7 Figma variant axes, 5 interaction states; Large size confirmed (48px)
- [[Button.tokens]] — ~40 tokens covering background, hover, active, text, tertiary, disabled; ⛔ 3 CONFLICTs
- [[Button.usage]] — 7 Do/Don't pairs covering hierarchy, text-button emphasis, destructive styling, icon labelling, sizing, split-vs-dropdown, disabled-vs-inline-error
- [[Button.accessibility]] — keyboard, ARIA (`aria-pressed`, `aria-label`), focus ring, WCAG 2.1 AA checklist
- [[Button.platform]] — no PUI requirements
- [[Button.composition]] — contains [[ButtonGroup]], [[DropdownButton]], [[IconButton]]; common with [[Tooltip]], [[Popover]]; used in [[Form]], [[Toolbar]], [[Dialog]]

## Open items

- ⛔ **GAP-001** (CONFLICT, blocker) — Secondary rest bg: Figma `action01` vs tokens.md `action02` → [[Button.tokens]]
- ⛔ **GAP-002** (CONFLICT, blocker) — Text active bg: Figma `active17` (inverted-only token) → [[Button.tokens]]
- ⛔ **GAP-003** (CONFLICT) — CSS `--actions/action09` vs semantic `action01` naming → [[Button.tokens]]
- 🔵 **GAP-005** (STUB) — PUI not extracted (likely none) → [[Button.platform]]
- ⏭️ 7 manual DOC_GAPs (GAP-007, 008, 014, 016, 017, 018, 019, 020) — defaults, fullWidth, disabled hex, Medium/Small dims, Figma variables, docs treatments, alignment copy, related list
