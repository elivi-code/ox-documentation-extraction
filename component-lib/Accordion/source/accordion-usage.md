---
component: Accordion
package: "@8x8/oxygen-accordion"
category: layout_overlay
role: usage
role_description: "Usage guidelines — authored from oxygen.8x8.com usage page + Best-Practices-derived Do/Don't pairs (no Figma Do/Don't frames exist)"
pipeline_stage: spec_ready
pipeline_note: "Audit verdict YES — GAP-001 partially addressed; Do/Don'ts are derived, not Figma-sourced"
audit_verdict: YES
siblings:
  - "[[Accordion/props]]"
  - "[[Accordion/examples]]"
  - "[[Accordion/tokens]]"
  - "[[Accordion/accessibility]]"
  - "[[Accordion/accordion-figma]]"
  - "[[Accordion/accordion-audit]]"
tags:
  - oxygen
  - component/Accordion
  - role/usage
  - stage/spec_ready
  - category/layout_overlay
---
<!-- SOURCE: oxygen.8x8.com/components/accordion/usage (website screenshot, verbatim) -->
<!-- OXYGEN MCP: get-component-docs returns README (props only) — no usage-page text -->
<!-- FIGMA EXAMPLES PAGE: 79430:614 — contains no ✅ Do / ❌ Don't frames (audit GAP-001) -->
<!-- EXTRACTED: 2026-05-11 -->
<!-- COMPONENT: Accordion -->
<!-- PAIRS: 3 (derived 1:1 from Best Practices — not Figma-sourced) -->

# Accordion — Usage Guidelines

> **See also:** [props.md](./props.md) · [tokens.md](./tokens.md) ·
> [examples.md](./examples.md) · [accordion-figma.md](./accordion-figma.md) ·
> [accessibility.md](./accessibility.md)

An accordion is a panel that is used to show and hide content.

---

## Anatomy

![Accordion anatomy — collapsed and expanded states with labelled parts](./accordion-usage-website.png)
<!-- SCREENSHOT TO BE ADDED: save the oxygen.8x8.com/components/accordion/usage screenshot to ./accordion-usage-website.png -->

1. **Collapsed accordion** — header row only; content panel is hidden.
2. **Expanded accordion** — header row plus content panel below.
3. **Icon** *(optional)* — leading icon slot. Controlled by `iconLeft` prop.
4. **Title** — primary label. Maps to the `title` prop.
5. **Secondary information** *(optional)* — right-aligned text. Maps to the `text` prop.
6. **Arrow icon** — chevron indicating expansion state. Rotates 180° when expanded.
7. **Divider** — bottom separator line between accordion rows.
8. **Content** — the rendered children inside the expanded panel.

> For token-level anatomy and the `_header` atom variant axes see
> [accordion-figma.md#anatomy](./accordion-figma.md#anatomy).

---

## Overview

Accordions are a set of panels stacked vertically; each panel can be expanded or collapsed to show or hide additional information.

---

## Behavior

### States

Header interaction states demonstrated on the Figma examples page:

1. **Rest — Collapsed**
2. **Rest — Expanded**
3. **Hover — Collapsed**
4. **Hover — Expanded**

> For token bindings per state (background, text, focus ring) see
> [accordion-figma.md#interaction-states](./accordion-figma.md#interaction-states)
> and [accordion-figma.md#color--token-bindings](./accordion-figma.md#color--token-bindings).

### Fixed height accordion

Accordions can be set to have a fixed height. In this case, only one accordion can be opened at a time.

Two sub-variants exist:

1. Accordion with scrollbar
2. Accordion without scrollbar

Enable fixed-height mode via `AccordionGroup hasFixedHeight`. See
[examples.md — Fixed-height group](./examples.md#fixed-height-group-one-open-at-a-time).

### Scroll content

If the accordion height is fixed, the information in the content area is scrollable. When the accordion doesn't have a fixed height set, the height is determined by the length of the content when expanded.

Scrolling behaviour can be overridden explicitly with the `isContentScrollable` prop.

### Nested accordion

Accordion can contain other accordions inside the content. The maximum allowed is two nested accordions.

See [examples.md — Nested accordion (max 2 levels)](./examples.md#nested-accordion-max-2-levels).

---

## Best practices

- The title of the accordion must reflect the content inside the collapsed accordion.
- Avoid putting important information in the content of collapsed accordions.
- Offer the option to "expand all" and "collapse all". It is not applicable when the accordions have a fixed height.

---

## Expand all / Collapse all

For variable-height accordion groups, provide `Collapse all` and `Expand all` controls above the group so users can preview or hide all content at once.

This control is **not applicable when the accordions have a fixed height** (only one accordion can be open at a time in that mode).

---

## When to use

- When you want to reduce clutter and want to display information one section at a time and hide information that is not relevant.
- When the content is long and the window real estate is limited.

## When not to use

- When the page permits all the data from the accordion to be visible and doesn't conflict with the user's workflow.
- When the information must be structured in a deep hierarchy with multiple sublevels — in such cases, consider using tabs.

---

## Do / Don't

<!-- DERIVED FROM BEST PRACTICES — NOT FROM FIGMA Do/Don't FRAMES -->
<!-- The Figma examples page (79430:614) contains no ✅ Do / ❌ Don't card frames. -->
<!-- These three pairs mirror the website's Best Practices section 1:1. -->

### Pair 1 — Title accuracy

| | Guidance |
|---|---|
| ✅ **Do** | Make the title reflect the content inside the collapsed accordion. A scannable title lets users decide whether to expand. |
| ❌ **Don't** | Use vague or unrelated titles ("More info", "Details") that don't preview what's inside. Users must expand every accordion to know what it contains. |

### Pair 2 — Content importance

| | Guidance |
|---|---|
| ✅ **Do** | Use the accordion for secondary or supplementary information that users may skip without consequence. |
| ❌ **Don't** | Hide critical, time-sensitive, or required-to-act information inside a collapsed accordion. Users may miss it entirely. |

### Pair 3 — Group controls

| | Guidance |
|---|---|
| ✅ **Do** | Offer "Expand all" and "Collapse all" controls for variable-height accordion groups so users can scan everything at once. |
| ❌ **Don't** | Add "Expand all" / "Collapse all" to fixed-height accordion groups — only one accordion can be open at a time, so the controls have no meaningful effect. |

---

## Related

**Patterns:** Forms

---

## Gaps

| Source | Status | Notes |
|--------|--------|-------|
| Figma `↳ Accordion examples` (`79430:614`) | No Do/Don't frames | Audit GAP-001. Designer must add `✅ Do` / `❌ Don't` frames to enable `figma-extract-usage`. |
| Oxygen MCP `get-component-docs` | Props only | The README content surfaced by the MCP does not include the editorial usage-page copy that renders at oxygen.8x8.com. |
| `accordion-usage-website.png` | Pending save | Add the website screenshot to `component-lib/Accordion/accordion-usage-website.png` so the Anatomy section renders. |
| Do/Don't pairs | Derived | Three pairs above are editorial inversions of the Best Practices section, not extracted from Figma. They should be replaced by Figma-sourced pairs when the designer fills the examples page. |

---

_Source: oxygen.8x8.com/components/accordion/usage (website) + Oxygen MCP · Extracted 2026-05-11_
