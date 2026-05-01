# Modal — Tokens

> **See also:** [props.md](props.md) · [examples.md](examples.md) · [accessibility.md](accessibility.md) · [Modal-figma.md](Modal-figma.md)

## Theme token coverage

No theme tokens were returned by `get-theme-tokens` for the Modal component. The component uses a `theme` prop (populated by the internal OX theme provider via `@8x8/oxygen-config` and `@8x8/oxygen-constants`) rather than standalone CSS custom properties registered in the design token system.

Design tokens were extracted from Figma instead — see [Modal-figma.md](Modal-figma.md) for the full token mapping.

---

## Design tokens identified in Figma

The following CSS custom properties were observed in the Figma design context for the Modal component:

### Surface tokens

| Token | Element | Notes |
|-------|---------|-------|
| `--ui/ui06` | Modal background (header, content, footer) | `white` in light mode; `#171719` in dark mode |
| `--ui/ui01` | Footer divider; dark mode border | `#ebeae1` in light; `#666` in dark |
| `--ui/shadow01` | Box shadow | `rgba(41,41,41,0.25)` in light; `#141414` in dark |

### Typography tokens

| Token | Element | Style |
|-------|---------|-------|
| `--typography/heading01/*` | Modal title | `font-size: 20px`, `font-weight: 600`, `line-height: 28px`, `letter-spacing: 0.0289px` |
| `--typography/body01/*` | Slot/content body text | `font-size: 14px`, `font-weight: 400`, `line-height: 20px`, `letter-spacing: -0.06px` |
| `--typography/bodyBold01/*` | Footer action buttons text | `font-size: 14px`, `font-weight: 600`, `line-height: 20px`, `letter-spacing: -0.06px` |

### Text color tokens

| Token | Element | Light value | Dark value |
|-------|---------|-------------|-----------|
| `--text/textcolor01` | Modal title | `#26252a` | `white` |
| `--text/textcolor02` | Content body text | `#6c6862` | `#c2c2c2` |
| `--text/textcolor09` | Button labels | `white` | `black` |

### Action tokens (Footer buttons)

| Token | Element | Light value | Dark value |
|-------|---------|-------------|-----------|
| `--actions/action02` | Secondary button background | `#26252a` | `#c2c2c2` |
| `--actions/action08` | Text button label | `#0056e0` | `#99bbf3` |
| `--actions/action09` | Primary button background | `#0056e0` | `#4687ed` |

### Slot placeholder tokens (design spec only)

| Token | Element | Light value | Dark value |
|-------|---------|-------------|-----------|
| `--ui/ui22` | Slot border (dashed) | `#0056e0` | `#ccddf9` |
| `--ui/ui23` | Slot background | `#e7e3ff` | `#3c2f8e` |

---

## Size variants

Sizes are controlled via the `size` prop on `Modal` / `ModalPortal`. No MCP token data was returned for sizes; widths are inferred from Figma:

| Size | Desktop width | Mobile width |
|------|-------------|-------------|
| Custom Modal (desktop) | `664px` | `320px` |
| Dialog Modal (desktop) | `664px` | `320px` |

> `width` and `height` props accept any CSS string and override the preset `size`.

---

## Spacing

Observed in Figma (raw values — not confirmed as tokens):

| Zone | Value |
|------|-------|
| Header padding | `16px` |
| Content padding | `16px` |
| Footer padding | `16px` |
| Footer button gap | `12px` |
| Header icon gap | `8px` |
| Corner radius | `6px` |
| Scrollbar width | `12px` |

> **Audit note:** Padding and gap values appear as hardcoded raw pixels in the Figma context. No spacing token bindings were resolved.

---

## Hardcoded values flagged

The following values appear hardcoded in the Figma design (not tokenised):

| Property | Element | Value |
|----------|---------|-------|
| Divider color (dark mode) | Footer divider | `#666` |
| Scrollbar background (light) | Scrollbar container | `#fafafa` |
| Scrollbar border (light) | Scrollbar container | `#e8e8e8` |
| Scrollbar thumb (light) | Scrollbar indicator | `#c1c1c1` |
| Scrollbar thumb (dark) | Scrollbar indicator | `#858585` |
| Corner radius | Modal container | `6px` |

_Source: Oxygen MCP + Figma MCP · Extracted 2026-05-01_
