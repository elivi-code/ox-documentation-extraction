# Slider — Tokens

> **See also:** [props.md](props.md) · [examples.md](examples.md) · [accessibility.md](accessibility.md) · [slider-pui.md](slider-pui.md)

> **Note:** The Oxygen MCP token search returned no results for "slider". All tokens below
> were extracted directly from the Figma design (UI-components, node `22902:37514`).

---

## Track tokens

| Element | Token | Light value | Dark value |
|---------|-------|-------------|------------|
| Active track — Default/Hover | `--ui/ui04` | `#26252a` | `white` |
| Active track — Active/Focus | `--actions/action01` | `#0056e0` | `#4687ed` |
| Inactive (background) track | `--ui/ui03` (Disabled 0%) | `#aba999` | `#858585` |
| Active track — Disabled 50% | `--interactive/disabled04` | `#8d8b7e` | `#858585` |
| Active track — Disabled 0% | `--ui/ui03` | `#aba999` | `#858585` |

## Track geometry

| Property | Value |
|----------|-------|
| Track height | `4px` |
| Track border-radius | `4px` |

## Thumb (Handle) tokens

| State | Light | Dark |
|-------|-------|------|
| Default / Rest | SVG asset | SVG asset |
| Hover / Active overlay | SVG ripple asset | SVG ripple asset |
| Disabled | SVG asset (muted) | SVG asset (muted) |

## Focus ring tokens

| Token | Light value | Dark value |
|-------|-------------|------------|
| `--interactive/focus01` | `#0056e0` | `#d7e3f9` |
| `--ui/ui06` (inner shadow) | `white` | `#171719` |

Focus ring spec: `2px solid` border, `inset 0px 0px 0px 4px` inner shadow, `border-radius: 1000px`.

## Thumb geometry

| State | Size |
|-------|------|
| Default | 16×16 px |
| Hover / Active (expanded) | 32×32 px (includes ripple overlay) |
| Focus | 24×24 px (Focus ring extends to `inset: -4px`) |

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

## States summary

| State | Track fill colour | Thumb | Label |
|-------|------------------|-------|-------|
| Default (Light) | `--ui/ui04` | Normal 16px | `--text/textcolor01` |
| Default (Dark) | `--ui/ui04` (white) | Normal 16px | `--text/textcolor01` |
| Hover (Light) | `--ui/ui04` | Expanded 32px + ripple | `--text/textcolor01` |
| Hover (Dark) | `--ui/ui04` (white) | Expanded 32px + ripple | `--text/textcolor01` |
| Active (Light) | `--actions/action01` #0056e0 | Expanded 32px + ripple | `--text/textcolor01` |
| Active (Dark) | `--actions/action01` #4687ed | Expanded 32px + ripple | `--text/textcolor01` |
| Focus (Light) | `--actions/action01` #0056e0 | 24px + focus ring #0056e0 | `--text/textcolor01` |
| Focus (Dark) | `--actions/action01` #4687ed | 24px + focus ring #d7e3f9 | `--text/textcolor01` |
| Disabled (Light) | `--interactive/disabled04` | Normal 16px (muted) | `--interactive/disabled01` |
| Disabled (Dark) | `--interactive/disabled04` | Normal 16px (muted) | `--interactive/disabled01` |

_Source: Figma (UI-components · 5YihJ5WuDvnvrlrRMC4sBp · node 22902:37514) · Extracted 2026-04-29_
