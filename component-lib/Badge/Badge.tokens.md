---
parent: "[[Badge]]"
section: tokens
---

## Colour tokens

### `notification01` — Badge background

| Mode | Token | Value | Palette reference |
|------|-------|-------|-------------------|
| Light | `notification01` | `#048284` | `colorPalette.turquoise05` |
| Dark | `notification01` | `#78CDCF` | `colorPalette.turquoise10` |

**Usage:** Background colour for the primary Badge type. Also used for unread message indicators and update notifications across the design system.

```css
background-color: var(--notification/notification01);
```

<!-- STUB:GAP-003 source="After running figma-extract (GAP-001), inspect the secondary variant fills in Figma. Identify and document the token bindings. Update tokens.md with a secondary colour row." -->
> **Source gap:** `type="secondary"` is a documented visual variant in [[Badge.props]] but has **no token binding** for background, text, or border. Resolve via `figma-extract`.

<!-- STUB:GAP-004 source="After running figma-extract (GAP-001), inspect the AIBadge frame fills. Identify token bindings and add an AIBadge section to tokens.md." -->
> **Source gap:** `AIBadge` (star icon + text) has **no token bindings** for background, border, icon colour, or text colour. Resolve via `figma-extract`.

## Typography tokens (counter label)

The counter label uses the `labelBold01` text style.

| Token | Role | Fallback |
|-------|------|---------|
| `--typography/font-family/sans` | Font family | `Inter` |
| `--typography/labelbold01/font-size` | Font size | `12px` |
| `--typography/labelbold01/font-weight` | Font weight | `600` (semibold) |
| `--typography/labelbold01/line-height` | Line height | `16px` |
| `--typography/labelbold01/letter-spacing` | Letter spacing | `0px` |

**Text colour:** `var(--text/textcolor04)` → white

## Sizing (from Figma design specs)

| Figma type | Height | Min-width | Width | H-padding | Border radius |
|-----------|--------|-----------|-------|-----------|--------------|
| `counter` | 16px | 16px | dynamic | 4px each side | 32px (pill) |
| `mention` | 16px | 16px | 16px | none | 32px (pill) |
| `dot` | 12px | 12px | 12px | none | 32px (full circle) |

Code `size` prop maps approximately as:

| `size` prop | Likely Figma equivalent |
|-------------|------------------------|
| `'small'` | `dot` (12×12px) |
| `'medium'` | `counter` / `mention` (16px height) |
| `'big'` | Larger counter variant |

<!-- STUB:GAP-005 source="After running figma-extract with Desktop Bridge (GAP-001), use getVariableByIdAsync to resolve spacing fills. Map values to Oxygen spacing scale tokens and update the tokens.md sizing table." -->
> **Source gap:** All sizing values above are **raw pixel values** from Figma specs — no Oxygen spacing/radius token names are mapped. Resolve via `figma-extract` + Variables API.

<!-- STUB:GAP-008 source="After running figma-extract (GAP-001), inspect the AIBadge frame for sizing and spacing values. Add an AIBadge row to the tokens.md sizing table." -->
> **Source gap:** `AIBadge` dimensions (height, padding, icon gap, font size) are **not documented**. Resolve via `figma-extract`.

## Token summary

| Token | Value (light) | Value (dark) | Usage |
|-------|--------------|--------------|-------|
| `notification/notification01` | `#048284` | `#78CDCF` | Badge background |
| `text/textcolor04` | `white` | `white` | Counter text |
| `typography/labelbold01/font-size` | `12px` | `12px` | Counter label size |
| `typography/labelbold01/font-weight` | `600` | `600` | Counter label weight |
| `typography/labelbold01/line-height` | `16px` | `16px` | Counter label line height |
