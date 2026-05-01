# Tag — Design Tokens

> **See also:** [props.md](props.md) · [examples.md](examples.md) · [accessibility.md](accessibility.md) · [Tag-figma.md](Tag-figma.md)

> **Note:** `get-theme-tokens` with `search="tag"` returned **0 component-specific tokens** —
> the Tag component reuses general UI tokens (`ui01`–`ui18`, `warning01`, `error01`, `focus01`,
> typography `label01`, spacing tokens). All token values below come from `get-theme-tokens`
> queries on the specific token names referenced by Figma.

---

## Background tokens (by `variant`)

| `variant` | Token | Light value | Dark value | Palette reference | General usage |
|-----------|-------|-------------|------------|-------------------|---------------|
| `default` | `ui/ui01` | `#EBEAE1` | `#666666` | offwhite09 / gray05 | Primary border for cards, tertiary background, selected list-item state |
| `blue` | `ui/ui09` | `#CCDDF9` | `#CCDDF9` | blue09 (both modes) | Color for non-text UI elements |
| `grey` | `ui/ui10` | `#6C6862` | `#666666` | offwhite05 / gray05 | Color for non-text UI elements |
| `red` | `ui/ui16` | `#F5D3D6` | `#F5D3D6` | red09 (both modes) | Subtle background for error and busy status |
| `yellow` | `ui/ui17` | `#FEEFD1` | `#FEEFD1` | yellow11 (both modes) | Subtle background for warning and away status |
| `green` | `ui/ui18` | `#D2F3E1` | `#D2F3E1` | green09 (both modes) | Subtle background for success and available status |
| `yellow-emphasis` | `warning/warning01` | `#F8AE1A` | `#F8AE1A` | yellow06 (both modes) | Warning color for non-text UI elements |

> **Pattern:** Most tag colors resolve to identical values across Light and Dark modes — only `default` and `grey` show real mode variation. The visual contrast in Dark mode comes mainly from the surface tokens behind the tag, not the tag color itself.

---

## Text color tokens (by `variant`)

| `variant` | Token | Light value | Dark value | Palette reference | General usage |
|-----------|-------|-------------|------------|-------------------|---------------|
| `default` | `text/textcolor01` | `#26252A` | `#FFFFFF` | offwhite02 / white | Default primary text — body, headers, input labels |
| `grey` | `text/textcolor06` | `#FFFFFF` | `#FFFFFF` | white (both modes) | Text color on dark color backgrounds |
| `blue`, `red`, `yellow`, `green`, `yellow-emphasis` | `text/textcolor07` | `#26252A` | `#292929` | offwhite02 / gray02 | Text color on light color backgrounds |

> **Pattern:** Color tags always pair with `textcolor07` (dark text on light background); only `default` uses `textcolor01` (mode-flipping); only `grey` uses `textcolor06` (white inverted text).

---

## Error border (`hasError={true}`)

| Token | Light value | Dark value | Palette reference | Description |
|-------|-------------|------------|-------------------|-------------|
| `error/error01` | `#CB2233` | `#F24D5F` | red05 / red07 | Error text and non-text error UI elements |

Applied as a 2px solid border around the tag container when `hasError` is true (Figma `type=withActionError`).

---

## Focus ring tokens (`isFocused={true}` or keyboard focus)

| Element | Token | Light value | Dark value | Palette reference | Description |
|---------|-------|-------------|------------|-------------------|-------------|
| Focus ring border | `interactive/focus01` | `#0056E0` | `#D7E3F9` | blue05 / blue10 | Primary focus border for all interactive UI elements |
| Focus ring inset gap | `ui/ui06` | `#FFFFFF` | `#171719` | white / purple01 | Primary background surface — used as the inset shadow that creates the white/dark gap between the focus border and the element |

Composition:
```css
border: 2px solid var(--interactive/focus01);
box-shadow: inset 0 0 0 4px var(--ui/ui06);
border-radius: 1000px;
```

---

## Typography tokens (label)

The Tag label uses the `label01` text style.

| Token | Value (both modes) | Description |
|-------|---------|-------------|
| `typography/label01/font-family` | `Inter, sans-serif` | Font family |
| `typography/label01/font-size` | `0.75rem` (12px) | Label font size |
| `typography/label01/line-height` | `1rem` (16px) | Label line height |
| `typography/label01/font-weight` | `400` (normal) | Label font weight |
| `typography/label01/letter-spacing` | `normal` | Letter spacing |

```css
font: var(--typography/label01);
/* or individually: */
font-family: var(--typography/label01/font-family);
font-size: var(--typography/label01/font-size);
font-weight: var(--typography/label01/font-weight);
line-height: var(--typography/label01/line-height);
letter-spacing: var(--typography/label01/letter-spacing);
```

---

## Spacing tokens (placement and internal)

| Token | Value | Used for |
|-------|-------|----------|
| `spacing/spacing01` | `2px` | Vertical padding (top + bottom) |
| `spacing/spacing02` | `4px` | Internal gap between icon/avatar/label/close button. **Also: spacing between adjacent tags** (per `usage` doc). |
| `spacing/spacing03` | `8px` | Horizontal padding (default type), and right padding of withAction type's leading edge |

> **Hardcoded values flagged in Figma:** the Tag's height (24px), border-radius (15px), and individual padding values are not bound to Figma Variables. They map conceptually to `spacing01` (2px V padding) and `spacing03` (8px H padding) but the binding is implicit.

---

## Sizing (from Figma — not token-bound)

| Property | Value | Notes |
|----------|-------|-------|
| Height | `24px` | Fixed across all variants — no token binding found |
| Border radius | `15px` | Pill shape — no token binding found |
| Padding (vertical) | `2px` | Maps to `spacing01` |
| Padding (horizontal, default) | `8px` | Maps to `spacing03` |
| Padding (right, withAction) | `4px` | Maps to `spacing02` |
| Avatar diameter | `24px` | Fills the full tag height |
| Leading icon size | `16×16px` (`iconSizeXS`) | From Code Connect — not from token data |

---

## Token summary

| Token | Light value | Dark value | Used for |
|-------|-------------|------------|----------|
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
| `typography/label01` | 12px / 400 / 16px | (same) | Label text style |
| `spacing/spacing01` | `2px` | `2px` | Vertical padding |
| `spacing/spacing02` | `4px` | `4px` | Internal gap + tag-to-tag spacing |
| `spacing/spacing03` | `8px` | `8px` | Horizontal padding |

---

_Source: Oxygen MCP (`get-theme-tokens`) · Figma node 8083:8359 · Extracted 2026-05-01_
