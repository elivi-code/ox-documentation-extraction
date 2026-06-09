---
component: Link
parent: "[[Link]]"
section: anatomy
pipeline_stage: draft
siblings:
  - "[[Link.props]]"
  - "[[Link.tokens]]"
  - "[[Link.usage]]"
  - "[[Link.accessibility]]"
  - "[[Link.platform]]"
  - "[[Link.composition]]"
tags:
  - oxygen
  - component/Link
  - role/spoke-anatomy
---
<!-- source: figma-only -->

## Anatomy

Elements from the Standalone Link component set layer tree (Figma node 58315:113).

| # | Type | Name | Role | Notes |
|---|------|------|------|-------|
| 1 | text | label (`<p>`) | Content element | Link text; always present |
| 2 | instance | `pop-out` (icon) | Optional slot | Controlled by `hasIcon` boolean; hidden by default |
| 3 | frame | Focus ring | Structural / decorative | Visible in Focus and Active states only; absolute-positioned overlay |

**Container:** horizontal auto-layout flex row, gap 4px, `items-start`.

<!-- STUB:GAP-013 source="Locate the Inline Link Figma frame (possibly within a separate page or usage examples canvas) and run figma-extract on that node. If no dedicated Inline component exists, document explicitly in Link-figma.md." -->

## Variant axes

| Property | Values | Default |
|----------|--------|---------|
| `mode` | `Light`, `Dark` | `Light` |
| `isInverted` | `true`, `false` | `false` |
| `state` | `Rest`, `Hover`, `Focus`, `Active` | `Rest` |
| `size` | `Small`, `Large` | `Small` |

<!-- STUB:GAP-005 source="Confirm hasIcon is Figma-only. If so, add a clarifying note to source/Link-figma.md: hasIcon has no React prop equivalent — the icon slot is controlled by passing/omitting the icon prop." -->

## States

| State | Trigger | Visual change |
|-------|---------|---------------|
| Rest | Default | No decoration; `action08` / `action10` text color |
| Hover | Pointer over | Underline added; color shifts to `hover15` / `hover20` |
| Focus | Keyboard Tab | Underline added; color same as Rest; focus ring appears (inner border + 2px outer shadow) |
| Active | Pointer down / Enter | Underline added; color shifts to `active14` / `active17`; focus ring visible |

## Size variants

| Variant | Font size | Line height | Icon size |
|---------|-----------|-------------|-----------|
| Small | 14px | 20px | 20×20px |
| Large | 16px | 24px | 24×24px |

## Structure & spacing

| Property | Token | Value | Notes |
|----------|-------|-------|-------|
| Gap (text ↔ icon) | — | 4px (hardcoded) | Between label and icon |
| Focus ring inset | — | `inset-0` (full overlay) | Absolute positioned |
| Focus ring border-radius | — | 2px (hardcoded) | `rounded-[2px]` |

**Hardcoded values:** container `gap: 4px`, focus ring `border-radius: 2px`, and icon inner vector inset `12.5%` have no token binding.

<!-- STUB:GAP-014 source="Re-run figma-extract with Desktop Bridge plugin active to obtain token coverage percentage." -->
<!-- STUB:GAP-015 source="Re-run figma_get_styles with Desktop Bridge plugin active to retrieve named text and effect styles." -->
<!-- STUB:GAP-016 source="Confirm isDisabled intentionality with component owner. If intentionally unsupported, add a note to props spoke. If handled via CSS pointer-events, document the recommended implementation pattern." -->
