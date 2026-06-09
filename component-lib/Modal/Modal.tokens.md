---
parent: "[[Modal]]"
section: tokens
component: Modal
role: spoke
pipeline_stage: published
audit_verdict: partial
siblings:
  - "[[Modal]]"
  - "[[Modal.props]]"
  - "[[Modal.anatomy]]"
  - "[[Modal.usage]]"
  - "[[Modal.accessibility]]"
  - "[[Modal.platform]]"
  - "[[Modal.composition]]"
tags:
  - oxygen
  - component/Modal
  - role/spoke
  - stage/published
---

## Theme token coverage

No theme tokens were returned by `get-theme-tokens` for the Modal component. The component uses a `theme` prop (populated by the internal OX theme provider via `@8x8/oxygen-config` and `@8x8/oxygen-constants`) rather than standalone CSS custom properties registered in the design token system.

Design tokens were extracted from Figma instead — see the Figma token bindings sections below.

<!-- STUB:GAP-002 source="Re-run get-theme-tokens with broader search terms ('ui06', 'shadow01', 'textcolor', 'action09') to confirm canonical token names; cross-reference against @8x8/oxygen-tokens registry and update with authoritative paths" -->

> **WARN-003:** All token names below use Figma CSS variable syntax (`--ui/ui06`, `--text/textcolor01`, etc.). These may differ from `@8x8/oxygen-tokens` canonical paths. Verify before using in implementation.

---

## Design tokens identified in Figma

### Surface tokens

| Token | Element | Light value | Dark value |
|-------|---------|-------------|-----------|
| `--ui/ui06` | Modal background (header, content, footer) | `white` | `#171719` |
| `--ui/ui01` | Footer divider; desktop dark border | `#ebeae1` | `#666` |
| `--ui/shadow01` | Box shadow | `rgba(41,41,41,0.25)` | `#141414` |

### Typography tokens

| Token | Element | Style |
|-------|---------|-------|
| `--typography/heading01/*` | Modal title | `font-size: 20px`, `font-weight: 600`, `line-height: 28px`, `letter-spacing: 0.0289px` |
| `--typography/body01/*` | Slot/content body text | `font-size: 14px`, `font-weight: 400`, `line-height: 20px`, `letter-spacing: -0.06px` |
| `--typography/bodyBold01/*` | Footer action buttons text | `font-size: 14px`, `font-weight: 600`, `line-height: 20px`, `letter-spacing: -0.06px` |

### Text color tokens

| Token | Element | Light value | Dark value |
|-------|---------|-------------|-----------|
| `--text/textcolor01` | Modal title, Dialog message | `#26252a` | `white` |
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

## Color and token bindings — Figma detail

### Modal container background

| Element | Token | Light value | Dark value |
|---------|-------|-------------|-----------|
| Header background | `--ui/ui06` | `white` | `#171719` |
| Content background | `--ui/ui06` | `white` | `#171719` |
| Footer background | `--ui/ui06` | `white` | `#171719` |

### Shadow and border

| Element | Token | Light value | Dark value |
|---------|-------|-------------|-----------|
| Box shadow (desktop) | `--ui/shadow01` | `rgba(41,41,41,0.25)` | `#141414` |
| Border (desktop, dark only) | `--ui/ui01` | _(no border)_ | `#666` |

> Desktop light: `box-shadow: 0px 2px 20px 0px var(--ui/shadow01)` — no border.
> Desktop dark: `box-shadow: 0px 2px 20px 9px var(--ui/shadow01)` + `1px solid border`.

### Footer buttons

| Element | Token | Light value | Dark value |
|---------|-------|-------------|-----------|
| Text button label | `--actions/action08` | `#0056e0` | `#99bbf3` |
| Secondary button background | `--actions/action02` | `#26252a` | `#c2c2c2` |
| Secondary button label | `--text/textcolor09` | `white` | `black` |
| Primary button background | `--actions/action09` | `#0056e0` | `#4687ed` |
| Primary button label | `--text/textcolor09` | `white` | `black` |
| Footer divider | `--ui/ui01` | `#ebeae1` | **`#666` ⚠ hardcoded** |

---

## Typography detail

| Token | Element | Size | Weight | Line height | Letter spacing |
|-------|---------|------|--------|------------|---------------|
| `typography/heading01` | Modal title | `20px` | `600` | `28px` | `0.0289px` |
| `typography/body01` | Dialog message, Slot body | `14px` | `400` | `20px` | `-0.06px` |
| `typography/bodyBold01` | Footer button labels | `14px` | `600` | `20px` | `-0.06px` |

---

## Size variants

Sizes are controlled via the `size` prop on `Modal` / `ModalPortal`. No MCP token data was returned for sizes; widths below are inferred from Figma:

| Figma variant | Desktop width | Mobile width |
|--------------|-------------|-------------|
| Custom Modal | `664px` | `320px` |
| Dialog Modal | `664px` | `320px` |

<!-- STUB:GAP-007 source="Resolve GAP-004 first (confirm size prop → px mapping for small/medium/big from component owner), then update this table with the three size presets and their pixel values" -->

> `width` and `height` props accept any CSS string and override the preset `size`.

---

## Spacing

Observed in Figma (raw values — not confirmed as token-bound):

| Zone | Value |
|------|-------|
| Header padding | `16px` |
| Content padding | `16px` |
| Footer padding | `16px` |
| Footer button gap | `12px` |
| Header title–icon gap | `8px` |
| Corner radius | `6px` |
| Scrollbar width | `12px` |

<!-- STUB:GAP-008 source="Component owner confirms which spacing values are hardcoded vs token-bound; populate a token column once confirmed; depends on GAP-002 (canonical token name resolution)" -->

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

<!-- STUB:GAP-009 source="Confirm with design whether these values should be tokenised; if intentionally hardcoded, add a reasoning note in Modal-figma.md; if token candidates exist, add them to this table" -->

_Source: Oxygen MCP + Figma MCP · Extracted 2026-05-01_
