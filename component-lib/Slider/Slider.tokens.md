---
component: Slider
parent: "[[Slider]]"
section: tokens
role: spoke
pipeline_stage: spec_ready
audit_verdict: PARTIAL
siblings:
  - "[[Slider]]"
  - "[[Slider.props]]"
  - "[[Slider.anatomy]]"
  - "[[Slider.usage]]"
  - "[[Slider.accessibility]]"
  - "[[Slider.platform]]"
  - "[[Slider.composition]]"
tags:
  - oxygen
  - component/Slider
  - role/spoke
  - section/tokens
  - stage/spec_ready
---

<!-- source: figma-only -->

> **Token source:** The Oxygen MCP token search returned no results for "slider". All tokens below were extracted directly from the Figma design (UI-components, node `22902:37514`). Two element categories (inactive track background, thumb fill/stroke) remain unresolved — see GAP-005 and GAP-006 below.

## Track tokens

| Element | Token | Light value | Dark value |
|---------|-------|-------------|------------|
| Active track — Default/Hover | `--ui/ui04` | `#26252a` | `white` |
| Active track — Active/Focus | `--actions/action01` | `#0056e0` | `#4687ed` |
| Active track — Disabled (50% opacity) | `--interactive/disabled04` | `#8d8b7e` | `#858585` |
| Active track — Disabled (0% opacity) | `--ui/ui03` | `#aba999` | `#858585` |
| Inactive (background) track | <!-- STUB:GAP-005 source="Request token annotation from design team for inactive track background, or cross-reference SVG imgSliderTrack hex against Oxygen token palette" --> _unresolved — SVG asset_ | — | — |

## Track geometry

| Property | Value |
|----------|-------|
| Height | `4px` |
| Border-radius | `4px` |

## Thumb (Handle) tokens

<!-- STUB:GAP-006 source="Inspect Figma Handle node fills via figma-console use_figma, or request token annotations from design team for thumb fill/stroke tokens" -->

> **GAP-006 — Thumb tokens unresolved.** Thumb fill and stroke colours are delivered as SVG image assets in the Figma MCP response (`imgHandle`, `imgHandle1`–`imgHandle5`). No CSS variable names are bound to the thumb visuals. The table below reflects geometry only.

| State | Size | Appearance |
|-------|------|------------|
| Default / Rest | 16×16 px | SVG asset |
| Hover / Active (expanded) | 32×32 px | SVG asset + ripple overlay |
| Focus | 24×24 px | SVG asset + focus ring |
| Disabled | 16×16 px | SVG asset (muted) |

## Focus ring tokens

| Token | Light value | Dark value |
|-------|-------------|------------|
| `--interactive/focus01` (border) | `#0056e0` | `#d7e3f9` |
| `--ui/ui06` (inner shadow) | `white` | `#171719` |

Focus ring spec: `2px solid` border, `inset 0px 0px 0px 4px` inner shadow, `border-radius: 1000px`.

## Label tokens

| State | Token | Light value | Dark value |
|-------|-------|-------------|------------|
| Enabled | `--text/textcolor01` | `#26252a` | `white` |
| Disabled | `--interactive/disabled01` | `#c8c8bd` | `#c2c2c2` |

## Typography — label

| Token | Value |
|-------|-------|
| `--typography/body01/font-family` | `'Inter:Regular', sans-serif` |
| `--typography/body01/font-weight` | `400` (normal) |
| `--typography/body01/font-size` | `14px` |
| `--typography/body01/line-height` | `20px` |
| `--typography/body01/letter-spacing` | `-0.06px` |

## Layout / spacing

| Property | Value |
|----------|-------|
| Gap between icon and track | `16px` |
| Track vertical padding (within slider row) | `6px` top + `6px` bottom |
| Icon size | `20×20 px` |

## Full state × mode matrix

| State | Mode | Track fill token | Thumb | Label token |
|-------|------|-----------------|-------|-------------|
| Default | Light | `--ui/ui04` (`#26252a`) | Normal 16px | `--text/textcolor01` |
| Default | Dark | `--ui/ui04` (`white`) | Normal 16px | `--text/textcolor01` |
| Hover | Light | `--ui/ui04` (`#26252a`) | Expanded 32px + ripple | `--text/textcolor01` |
| Hover | Dark | `--ui/ui04` (`white`) | Expanded 32px + ripple | `--text/textcolor01` |
| Active | Light | `--actions/action01` (`#0056e0`) | Expanded 32px + ripple | `--text/textcolor01` |
| Active | Dark | `--actions/action01` (`#4687ed`) | Expanded 32px + ripple | `--text/textcolor01` |
| Focus | Light | `--actions/action01` (`#0056e0`) | 24px + focus ring `#0056e0` | `--text/textcolor01` |
| Focus | Dark | `--actions/action01` (`#4687ed`) | 24px + focus ring `#d7e3f9` | `--text/textcolor01` |
| Disabled | Light | `--interactive/disabled04` (`#8d8b7e`) | Normal 16px (muted) | `--interactive/disabled01` |
| Disabled | Dark | `--interactive/disabled04` (`#858585`) | Normal 16px (muted) | `--interactive/disabled01` |

_Source: Figma (UI-components · 5YihJ5WuDvnvrlrRMC4sBp · node 22902:37514) · Extracted 2026-04-29_
