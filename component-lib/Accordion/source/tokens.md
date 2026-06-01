---
component: Accordion
package: "@8x8/oxygen-accordion"
category: layout_overlay
role: tokens
role_description: "Design tokens — color, spacing, and typography token bindings"
pipeline_stage: spec_ready
pipeline_note: "Audit verdict YES/PARTIAL — doc-rewrite can run"
audit_verdict: YES
siblings:
  - "[[Accordion/props]]"
  - "[[Accordion/examples]]"
  - "[[Accordion/accessibility]]"
  - "[[Accordion/accordion-figma]]"
  - "[[Accordion/accordion-audit]]"
tags:
  - oxygen
  - component/Accordion
  - role/tokens
  - stage/spec_ready
  - category/layout_overlay
---
# Accordion — Tokens

> **See also:** [props.md](./props.md) · [examples.md](./examples.md) · [accessibility.md](./accessibility.md) · [accordion-figma.md](./accordion-figma.md)

---

> **Note:** The Oxygen MCP returned no theme tokens for the `accordion` package
> (0 matches for search term `"accordion"`). All token data below was sourced
> from Figma design inspection of nodes `44417:100356` (_header_ atom `8298:8979`).

---

## Color tokens

### Header background

| State | Token | Light value | Dark value |
|-------|-------|-------------|------------|
| Rest / Focus | `--ui/ui06` | `#ffffff` | `#171719` |
| Hover | `--ui/ui05` | `#f4f3ee` | `#2f2e32` |
| Disabled | `--ui/ui06` | `#ffffff` | `#171719` |

### Title text

| State | Token | Light value | Dark value |
|-------|-------|-------------|------------|
| Rest / Hover / Focus | `--text/textcolor01` | `#26252a` | `#ffffff` |
| Disabled | `--interactive/disabled04` | `#8d8b7e` | `#858585` |

### Secondary text (right side)

| State | Token | Light value | Dark value |
|-------|-------|-------------|------------|
| Rest / Hover / Focus | `--text/textcolor02` | `#6c6862` | `#c2c2c2` |
| Disabled | `--interactive/disabled04` | `#8d8b7e` | `#858585` |

### Focus ring

| State | Token | Light value | Dark value |
|-------|-------|-------------|------------|
| Focus | `--interactive/focus01` | `#0056e0` | `#d7e3f9` |

### Divider

| Element | Token | Light value | Dark value |
|---------|-------|-------------|------------|
| Bottom separator | `--ui/ui01` | `#ebeae1` | `#666666` |

### AI Badge (optional, `AIBadge?` toggle)

| Element | Token | Light value | Dark value |
|---------|-------|-------------|------------|
| Badge background | `--ui/ui23` | `#e7e3ff` | `#3c2f8e` |
| Badge text | `--text/textcolor10` | `#4a3da4` | `#e7e3ff` |

---

## Typography tokens

| Element | Token | Size | Weight | Line height | Letter spacing |
|---------|-------|------|--------|-------------|----------------|
| Title | `--typography/bodyBold01` | `14px` | `600 (SemiBold)` | `20px` | `-0.06px` |
| Secondary text | `--typography/label01` | `12px` | `400 (Regular)` | `16px` | `0px` |

Font family tokens:

| Token | Usage |
|-------|-------|
| `--typography/bodyBold01/font-family` | Title font family (`Inter:Semi_Bold`) |
| `--typography/font-family/sans` | Secondary text font family (`Inter:Regular`) |

---

## Figma variant matrix

| Figma property | Values | Default |
|---------------|--------|---------|
| `mode` | `light`, `dark` | `light` |
| `isOpen?` | `true`, `false` | `false` |
| `divider?` | `true`, `false` | `true` |
| `scrollbar?` | `true`, `false` | `false` |

Header atom (`_header`) additional properties:

| Figma property | Values | Default |
|---------------|--------|---------|
| `state` | `rest`, `hover`, `focus`, `disabled` | `rest` |
| `icon?` | `true`, `false` | `true` |
| `rightText?` | `true`, `false` | `true` |
| `AIBadge?` | `true`, `false` | `false` |

---

_Source: Oxygen MCP + Figma design inspection · Extracted 2026-04-28_
