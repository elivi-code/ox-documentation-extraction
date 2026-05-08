---
component: ToggleButton
package: "@8x8/oxygen-toggleButton"
category: form_inputs
role: tokens
role_description: "Design tokens — color, spacing, and typography token bindings"
pipeline_stage: blocked
pipeline_note: "Audit verdict NO — resolve CONFLICTs before rewrite"
audit_verdict: NO
siblings:
  - "[[ToggleButton/props]]"
  - "[[ToggleButton/examples]]"
  - "[[ToggleButton/accessibility]]"
  - "[[ToggleButton/ToggleButton-figma]]"
  - "[[ToggleButton/ToggleButton-pui]]"
  - "[[ToggleButton/ToggleButton-audit]]"
tags:
  - oxygen
  - component/ToggleButton
  - role/tokens
  - stage/blocked
  - category/form_inputs
---
# ToggleButton — Tokens

> **See also:** [props.md](./props.md) · [examples.md](./examples.md) · [accessibility.md](./accessibility.md) · [ToggleButton-figma.md](./ToggleButton-figma.md)

---

## OX theme tokens (from Oxygen MCP)

| Token | Light value | Dark value | Reference | Usage |
|-------|------------|-----------|-----------|-------|
| `ui33` | `#6C6862` | `#858585` | `colorPalette.offwhite05` / `colorPalette.gray06` | Background color for toggle base (default/off state) |

---

## Design tokens (from Figma design context)

Tokens observed as CSS custom properties in the Figma-generated code. Grouped by element.

### Toggle Base (pill background)

| State | Token | Light value | Dark value |
|-------|-------|------------|-----------|
| Default (off) | `--ui/ui33` | `#6c6862` | `#858585` |
| On / checked | `--actions/action01` | `#0056e0` | `#4687ed` |
| Disabled (off or on) | `--ui/ui33` | `#6c6862` | `#858585` |

### Toggle Knot (thumb)

The knot uses image assets with three variants:
- **Normal**: white/standard knot
- **Disabled – Light mode**: muted knot
- **Disabled – Dark mode**: muted knot (dark palette)

No token bindings on the knot itself — rendered as image assets.

### Focus ring

| Element | Token | Light value | Dark value | Notes |
|---------|-------|------------|-----------|-------|
| Toggle Input focus ring | `--interactive/focus01` | `#0056e0` | `#d7e3f9` | `box-shadow: 0 0 0 2px` |
| Toggle (full) focus ring border | `--ui/ui06` | `white` | `#171719` | 1px border on focus ring overlay |
| Toggle (full) focus ring shadow | `--interactive/focus01` | `#0056e0` | `#d7e3f9` | `box-shadow: 0 0 0 2px` |

### Label text

| State | Token | Light value | Dark value |
|-------|-------|------------|-----------|
| Default | `--text/textcolor01` | `#26252a` | `white` |
| Disabled | `--interactive/disabled02` | `#c8c8bd` | `#666666` |
| Required asterisk | `--actions/action03` | `#cb2233` | `#d83848` |

### Toggle Group — Feedback area

| Element | Token | Light value | Dark value |
|---------|-------|------------|-----------|
| Error message text | `--error/error01` | `#cb2233` | `#f24d5f` |
| Helper text | `--text/textcolor02` | `#6c6862` | `#c2c2c2` |

### Toggle Group — Slot placeholder

| Element | Token | Light value | Dark value |
|---------|-------|------------|-----------|
| Slot background | `--ui/ui23` | `#e7e3ff` | `#3c2f8e` |
| Slot border | `--ui/ui22` | `#0056e0` | `#ccddf9` |

---

## Typography tokens

| Token | Weight | Size | Line height | Letter spacing | Used on |
|-------|--------|------|-------------|----------------|---------|
| `typography/body01` | 400 (Regular) | 14px | 20px | −0.06px | Label text |
| `typography/bodyBold01` | 600 (Semi Bold) | 14px | 20px | −0.06px | Required asterisk |
| `typography/label01` | 400 (Regular) | 12px | 16px | 0px | Helper/error message |
| `typography/heading01` | 600 (Semi Bold) | 20px | 28px | 0.0289px | Slot heading (Toggle Group) |

Font family: `typography/body01/font-family` → Inter (Regular / Semi Bold)

---

## Spacing (from Figma guidelines)

| Usage | Value | Token |
|-------|-------|-------|
| Gap between toggle switch and label | 12px | — |
| Gap between stacked Toggle items | 8px | `$spacing03` |
| Gap between Toggle and adjacent Icon Button | 4px | `$spacing02` |
| Label vertical padding | 2px top + 2px bottom | — |
| Toggle Group internal gap | 12px | — |

---

_Source: Oxygen MCP + Figma MCP · Extracted 2026-04-29_
