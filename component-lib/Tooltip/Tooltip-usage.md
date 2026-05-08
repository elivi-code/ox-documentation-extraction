---
component: Tooltip
package: "@8x8/oxygen-tooltip"
category: overlays_contextual
role: usage
role_description: "Usage guidelines — Do/Don't editorial guidance extracted from Figma examples page"
pipeline_stage: blocked
pipeline_note: "Audit verdict NO — resolve CONFLICTs before rewrite"
audit_verdict: NO
siblings:
  - "[[Tooltip/props]]"
  - "[[Tooltip/examples]]"
  - "[[Tooltip/tokens]]"
  - "[[Tooltip/accessibility]]"
  - "[[Tooltip/Tooltip-figma]]"
  - "[[Tooltip/Tooltip-pui]]"
  - "[[Tooltip/Tooltip-audit]]"
tags:
  - oxygen
  - component/Tooltip
  - role/usage
  - stage/blocked
  - category/overlays_contextual
---
<!-- SOURCE: Figma — ↳ Tooltip examples -->
<!-- PAGE: ↳ Tooltip examples -->
<!-- SECTION: Tooltip, Tooltip and Popover working together, Tooltip vs. Popover vs. Modal -->
<!-- EXTRACTED: 2026-05-05 -->
<!-- COMPONENT: Tooltip -->
<!-- PAIRS: 0 -->
<!-- NOTE: No ✅ Do / ❌ Don't card frames found on this page. Usage guidelines are text-based. Content extracted via Figma MCP metadata (Desktop Bridge not connected). -->

# Tooltip — Usage Guidelines

> **See also:** [props.md](./props.md) · [tokens.md](./tokens.md) ·
> [examples.md](./examples.md) · [Tooltip-figma.md](./Tooltip-figma.md)

Usage guidelines extracted from the Figma `↳ Tooltip examples` page. The page uses text-based sections rather than Do/Don't card frames.

---

## Overview

The Tooltip component displays contextual information when users hover over or focus on an element. Tooltips are designed to provide brief, supplementary information that helps users understand the purpose or function of UI elements.

Tooltips should only be used for short descriptions. Keep tooltip content concise and limited to a single sentence or brief phrase. If you need to provide longer explanations, consider using a popover, modal, or dedicated help section instead.

---

## When to use

- Explaining the purpose of an icon-only button
- Providing additional context for truncated text
- Clarifying abbreviations or technical terms
- Describing disabled elements

## When not to use

- Displaying long paragraphs or detailed instructions
- Presenting complex information that requires user interaction
- Showing critical information that users must read (tooltips can be easily missed)

---

## Best practices

**Keep it short:** Limit tooltip text to approximately 136 characters maximum. Users should be able to read and understand the content in 2–3 seconds.

**Be descriptive:** While brief, tooltips should still provide meaningful information. Avoid redundant text that simply repeats the label.

**Use plain language:** Write in clear, simple terms that all users can understand.

**Avoid essential information:** Never put critical information solely in a tooltip, as they may not be accessible to all users.

---

## Size

Max-width is 320px.

### Content length examples (from Figma)

| Label | Approx. width | Lines |
|-------|--------------|-------|
| Good — short and clear | ~91px | 1 |
| 50 characters | ~313px | 1 |
| 75 characters | 320px | 2 |
| 136 characters (maximum) | 320px | 3 |

---

## Tooltip and Popover working together

The Popover component displays rich, interactive content in a floating panel that appears when users click or interact with a trigger element. Unlike tooltips, popovers can contain longer text, formatted content, interactive elements, and remain visible until explicitly dismissed.

### Trigger state progression

| State | Component shown | Cursor |
|-------|----------------|--------|
| Trigger rest state | — | Default |
| Trigger on hover | Tooltip | Pointer (indicating actionable element) |
| Trigger on click | Popover | — |

### Hover vs focus trigger

The examples page also illustrates:
- **Hover state:** cursor is a Pointer arrow — tooltip appears
- **Focus state:** keyboard focus on trigger — tooltip appears (same content, no cursor)

---

## Tooltip vs. Popover vs. Modal

Comparison table extracted verbatim from the Figma examples page.

| Criteria | Tooltip | Popover | Modal |
|----------|---------|---------|-------|
| Content length | 136 characters | 2–4 paragraphs | Unlimited content |
| Interactivity | Non-interactive (read-only) | Interactive (buttons, forms, links) | Fully interactive workflows |
| Trigger method | Hover or focus | Click or tap | Click, action, or system event |
| Dismissal | Automatic (mouse out/blur) | Manual (click trigger again, click outside, close button, action completion, Esc) | Manual (click scrim, close button, action completion, Esc) |
| User attention | Passive, subtle | Moderate, contextual | High, demands focus |
| Blocks workflow | No | Partially (overlay, but page visible) | Yes (blocks entire page) |
| Position | Anchored to trigger element | Anchored to trigger element | Center of screen |
| Purpose | Quick hints and labels | Contextual details and options | Critical tasks and decisions |

---

## Gaps

No formal Do/Don't card frames (`✅ Do —` / `❌ Don't —`) were found on this page. The page uses text-based usage sections instead. Screenshots of Figma image blocks were not captured (Desktop Bridge required for `figma_take_screenshot`).

| Section | Missing |
|---------|---------|
| Do/Don't cards | None present — page uses text guidance only |
| Image block screenshots | Not captured — requires Desktop Bridge |

---

_Source: Figma examples page · Extracted 2026-05-05_
