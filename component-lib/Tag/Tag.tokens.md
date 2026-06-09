---
parent: "[[Tag]]"
section: tokens
component: Tag
package: "@8x8/oxygen-tag"
role: tokens
pipeline_stage: doc_rewrite
audit_verdict: YES
siblings:
  - "[[Tag]]"
  - "[[Tag.props]]"
  - "[[Tag.anatomy]]"
  - "[[Tag.usage]]"
  - "[[Tag.accessibility]]"
  - "[[Tag.platform]]"
  - "[[Tag.composition]]"
tags: [component, data_display, role/tokens]
---

> **Source note:** `get-theme-tokens` with `search="tag"` returned 0 component-specific tokens — Tag reuses general UI tokens (`ui01`–`ui18`, `warning01`, `error01`, `focus01`, typography `label01`, spacing tokens). Values below are from `get-theme-tokens` queries on the specific token names referenced by Figma.

<!-- STUB:GAP-006 source="Re-run figma-extract with the Desktop Bridge plugin active and Figma Variables API available to confirm token bindings and collection structure." -->

> All token names were inferred from CSS variable fallback paths during extraction (e.g. `var(--ui/ui01, #ebeae1)`). Actual variable collection structure and binding assignments are unconfirmed — re-run with Desktop Bridge connected to verify.

---

## Background tokens (by `variant`)

| `variant` | Token | Light value | Dark value | Palette ref | General usage |
|---|---|---|---|---|---|
| `default` | `ui/ui01` | `#EBEAE1` | `#666666` | offwhite09 / gray05 | Primary border for cards, tertiary background, selected list-item state |
| `blue` | `ui/ui09` | `#CCDDF9` | `#CCDDF9` | blue09 (both modes) | Non-text UI element color |
| `grey` | `ui/ui10` | `#6C6862` | `#666666` | offwhite05 / gray05 | Non-text UI element color |
| `red` | `ui/ui16` | `#F5D3D6` | `#F5D3D6` | red09 (both modes) | Subtle background for error and busy status |
| `yellow` | `ui/ui17` | `#FEEFD1` | `#FEEFD1` | yellow11 (both modes) | Subtle background for warning and away status |
| `green` | `ui/ui18` | `#D2F3E1` | `#D2F3E1` | green09 (both modes) | Subtle background for success and available status |
| `yellow-emphasis` | `warning/warning01` | `#F8AE1A` | `#F8AE1A` | yellow06 (both modes) | Warning color for non-text UI elements |

> Most tag colors resolve to identical values across Light and Dark modes — only `default` and `grey` show visible mode variation. The visual contrast in Dark mode comes mainly from the surface tokens behind the tag.

---

## Text color tokens (by `variant`)

| `variant` | Token | Light value | Dark value | Palette ref |
|---|---|---|---|---|
| `default` | `text/textcolor01` | `#26252A` | `#FFFFFF` | offwhite02 / white |
| `grey` | `text/textcolor06` | `#FFFFFF` | `#FFFFFF` | white (both modes) |
| `blue`, `red`, `yellow`, `green`, `yellow-emphasis` | `text/textcolor07` | `#26252A` | `#292929` | offwhite02 / gray02 |

> Color variants always pair with `textcolor07` (dark text on light background); `default` uses `textcolor01` (mode-flipping); `grey` uses `textcolor06` (white inverted text).

---

## Error border (`hasError={true}`)

| Token | Light value | Dark value | Palette ref | Description |
|---|---|---|---|---|
| `error/error01` | `#CB2233` | `#F24D5F` | red05 / red07 | Error text and non-text error UI elements |

Applied as a 2 px solid border around the tag container when `hasError` is true (Figma `type=withActionError`).

---

## Focus ring tokens

| Element | Token | Light value | Dark value | Palette ref |
|---|---|---|---|---|
| Focus ring border | `interactive/focus01` | `#0056E0` | `#D7E3F9` | blue05 / blue10 |
| Focus ring inset gap | `ui/ui06` | `#FFFFFF` | `#171719` | white / purple01 |

Double-layer focus ring composition (8x8 standard pattern):

```css
border: 2px solid var(--interactive/focus01);
box-shadow: inset 0 0 0 4px var(--ui/ui06);
border-radius: 1000px;
```

The inset shadow creates a white/dark gap between the focus border and the element. See [[Tag.accessibility]] for usage context.

---

## Typography tokens (label)

The tag label uses the `$label01` text style.

| Token | Value (both modes) | Description |
|---|---|---|
| `typography/label01/font-family` | `Inter, sans-serif` | Font family |
| `typography/label01/font-size` | `0.75rem` (12 px) | Label font size |
| `typography/label01/line-height` | `1rem` (16 px) | Label line height |
| `typography/label01/font-weight` | `400` (normal) | Label font weight |
| `typography/label01/letter-spacing` | `normal` (0 px) | Letter spacing |

```css
font: var(--typography/label01);
```

---

## Spacing tokens

| Token | Value | Used for |
|---|---|---|
| `spacing/spacing01` | `2px` | Vertical padding (top + bottom) |
| `spacing/spacing02` | `4px` | Internal gap between icon / avatar / label / close button; also spacing between adjacent tags |
| `spacing/spacing03` | `8px` | Horizontal padding (default type); right padding leading edge of `withAction` type |

> Spacing values are hardcoded px in Figma — no Figma Variables binding confirmed. The token names represent conceptual mappings, not verified variable bindings.

---

## Sizing (from Figma — not token-bound)

| Property | Value | Notes |
|---|---|---|
| Height | `24px` | Fixed across all variants — no token binding |
| Border radius | `15px` | Pill shape — no token binding |
| Padding vertical | `2px` | Conceptually `spacing01` |
| Padding horizontal (default) | `8px` | Conceptually `spacing03` |
| Padding right (withAction) | `4px` | Conceptually `spacing02` |
| Avatar diameter | `24px` | Fills the full tag height |
| Leading icon | `16×16px` | `iconSizeXS` — from Code Connect, not token data |

---

## Close button tokens

<!-- STUB:GAP-005 source="Inspect CloseButton.tsx source (packages/tag/src/components/CloseButton.tsx) or run get-theme-tokens with relevant search terms to identify the × icon color token. Add a 'Close button tokens' section to this file." -->

> The close button (×) is a sub-component (`CloseButton.tsx`). Its icon color token and hover/pressed state tokens are not captured — extraction covered only container-level tokens.

---

## Token summary

| Token | Light value | Dark value | Used for |
|---|---|---|---|
| `ui/ui01` | `#EBEAE1` | `#666666` | `variant="default"` background |
| `ui/ui09` | `#CCDDF9` | `#CCDDF9` | `variant="blue"` background |
| `ui/ui10` | `#6C6862` | `#666666` | `variant="grey"` background |
| `ui/ui16` | `#F5D3D6` | `#F5D3D6` | `variant="red"` background |
| `ui/ui17` | `#FEEFD1` | `#FEEFD1` | `variant="yellow"` background |
| `ui/ui18` | `#D2F3E1` | `#D2F3E1` | `variant="green"` background |
| `warning/warning01` | `#F8AE1A` | `#F8AE1A` | `variant="yellow-emphasis"` background |
| `text/textcolor01` | `#26252A` | `#FFFFFF` | `variant="default"` text |
| `text/textcolor06` | `#FFFFFF` | `#FFFFFF` | `variant="grey"` text |
| `text/textcolor07` | `#26252A` | `#292929` | All other variants' text |
| `interactive/focus01` | `#0056E0` | `#D7E3F9` | Focus ring border |
| `ui/ui06` | `#FFFFFF` | `#171719` | Focus ring inset gap |
| `error/error01` | `#CB2233` | `#F24D5F` | `hasError` border |
| `typography/label01` | 12 px / 400 / 16 px | (same) | Label text style |
| `spacing/spacing01` | `2px` | `2px` | Vertical padding |
| `spacing/spacing02` | `4px` | `4px` | Internal gap + tag-to-tag spacing |
| `spacing/spacing03` | `8px` | `8px` | Horizontal padding |

---

_Source: Oxygen MCP (`get-theme-tokens`) · Figma node 8083:8359 · Extracted 2026-05-01_
