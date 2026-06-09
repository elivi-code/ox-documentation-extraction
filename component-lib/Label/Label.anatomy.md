---
parent: "[[Label]]"
section: anatomy
---

<!-- source: figma-only -->

## Anatomy

The Figma component is `_base_form_label` (node `22230:37448`). The showcase frame (`33680:62952`) is a documentation frame; prefer the inner component for re-extractions.

### Elements

| # | Type | Name | Role | Notes |
|---|------|------|------|-------|
| 1 | frame | H Stack | Structural | Horizontal flex container; holds text and optional asterisk |
| 2 | text | Label text | Content element | Label string; driven by `value` prop |
| 3 | text | `*` (required asterisk) | Optional slot | Shown when `isRequired = true` |
| 4 | instance | Icon Button | Optional slot | Info/help button; shown when `infoBoxText` is provided |

### Icon Button sub-element

| # | Type | Name | Role | Notes |
|---|------|------|------|-------|
| 1 | frame | Icon Button wrapper | Structural | 2px padding, 6px corner radius (hardcoded) |
| 2 | instance | TypeIcon | Fixed sub-component | Size = `iconSizeM`; mode follows parent |

## Variant axes

### Mode

| Value | Notes |
|-------|-------|
| `light` (default) | Light surface — `text/textColor01` = `#26252a` |
| `dark` | Dark surface — `text/textColor01` = `#ffffff` |

> Mode is a Figma-only axis; in Oxygen the theme is controlled by the design system theme provider, not a `mode` prop on `Label`.

### Boolean toggles (Figma component properties)

| Property | Default | Code equivalent |
|----------|---------|-----------------|
| `information` | `true` | Icon Button slot visible when `infoBoxText` (+ `infoBoxButtonLabel`) are provided |
| `isRequired` | `true` | Asterisk slot visible when `isRequired={true}` |

> **GAP-017 resolved 2026-06-08:** Figma's `information` boolean is a simplified design-side representation. In code, the info icon appears when `infoBoxText` and `infoBoxButtonLabel` are provided — confirmed via Storybook. There is no separate boolean prop on the React `Label` component.

## States

| State | Trigger | Visual change |
|-------|---------|---------------|
| Default | none | Label text in `text/textColor01`; horizontal layout |
| Required | `isRequired={true}` | Red asterisk `*` in `error/error01` to the right of label text |
| With info | `infoBoxText` set | Icon Button slot appears to the right of label text |
| Hover (info icon) | Pointer over Icon Button | Inherits Icon Button component hover styles |
| Disabled | `isDisabled={true}` | Label visually muted |

<!-- STUB:GAP-015 source="Designer must add isDisabled variant to _base_form_label Figma component — disabled visual treatment (muted color token) is not documented in Figma or MCP" -->
<!-- STUB:GAP-016 source="Designer must add shouldWrapText and showTooltipOnOverflow Figma variants — these React-level behaviours have no Figma representation on the current node" -->

## Spacing

All spacing values are hardcoded — no token bindings were found.

| Property | Value | Element |
|----------|-------|---------|
| Gap | `4px` | H Stack: between label text and Icon Button |
| Padding | `2px` (all sides) | Icon Button wrapper |
| Border-radius | `6px` | Icon Button wrapper |
| Icon size | `iconSizeM` | Icon inside Icon Button |

## Layout

- Direction: horizontal (H Stack)
- Alignment: `items-center`, `content-stretch`
- Width: component fills available space; Figma showcase shows 68px for the component symbol
- Text wrapping: not represented as a Figma variant — see `shouldWrapText` prop in [[Label.props]]

_Source: Figma MCP · figma-console MCP (Desktop Bridge) · Extracted 2026-05-01 · GAP-017 resolved 2026-06-08_
