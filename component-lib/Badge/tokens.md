---
component: Badge
package: "@8x8/oxygen-badge"
category: data_display
role: tokens
role_description: "Design tokens — color, spacing, and typography token bindings"
pipeline_stage: extracted
pipeline_note: "Core files present; audit not yet run"
siblings:
  - "[[Badge/props]]"
  - "[[Badge/examples]]"
  - "[[Badge/accessibility]]"
  - "[[Badge/badge-pui]]"
  - "[[Badge/badge-usage]]"
tags:
  - oxygen
  - component/Badge
  - role/tokens
  - stage/extracted
  - category/data_display
---
# Badge — Design Tokens

> **See also:** [props.md](props.md) · [examples.md](examples.md) · [accessibility.md](accessibility.md)

---

## Colour tokens

### `notification01` — Badge background

| Mode | Token | Value | Palette reference |
|------|-------|-------|-------------------|
| Light | `notification01` | `#048284` | `colorPalette.turquoise05` |
| Dark | `notification01` | `#78CDCF` | `colorPalette.turquoise10` |

**Usage:** Background colour for all Badge types. Also used for unread message indicators and update notifications across the design system.

**CSS variable:**
```css
background-color: var(--notification/notification01);
```

---

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

---

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

---

## Token summary

| Token | Value (light) | Value (dark) | Usage |
|-------|--------------|--------------|-------|
| `notification/notification01` | `#048284` | `#78CDCF` | Badge background |
| `text/textcolor04` | `white` | `white` | Counter text |
| `typography/labelbold01/font-size` | `12px` | `12px` | Counter label size |
| `typography/labelbold01/font-weight` | `600` | `600` | Counter label weight |
| `typography/labelbold01/line-height` | `16px` | `16px` | Counter label line height |

---

_Source: Oxygen MCP (`get-theme-tokens`) · Figma node 2565:14 · Extracted 2026-04-29_
