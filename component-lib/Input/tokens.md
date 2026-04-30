# Input — Tokens

> **See also:** [Input-figma.md](./Input-figma.md) · [props.md](./props.md) ·
> [examples.md](./examples.md) · [accessibility.md](./accessibility.md)

---

## Theme tokens

Tokens sourced from `oxygen-mcp:get-theme-tokens` (search: "input") and from design context CSS variable references in Figma.

### Background tokens

| Token | Light | Dark | Description |
|-------|-------|------|-------------|
| `ui05` | `#F4F3EE` | `#2F2E32` | Primary background color for input fields |
| `hover06` | `#EBEAE1` | `#666666` | Hover background color for inputs |

**CSS variable references from Figma:**
```css
--ui/ui05         /* Input field background */
--hover/hover06   /* Hover state background */
```

### Text color tokens

| Token | Light | Dark | Description |
|-------|-------|------|-------------|
| `textColor01` | `#26252A` | `#FFFFFF` | Label text, filled value text |
| `textColor02` | `#6C6862` | *(dark value not captured)* | Placeholder text, helper/hint text |

**CSS variable references from Figma:**
```css
--text/textColor01    /* Label */
--text/textColor02    /* Placeholder, hint */
```

### Error tokens

| Token | Light | Dark | Description |
|-------|-------|------|-------------|
| `error01` | `#CB2233` | *(dark value not captured)* | Error border, error message text, required asterisk |

**CSS variable reference from Figma:**
```css
--error/error01    /* Required *, error state */
```

---

## Typography tokens

Sourced from design context style output.

| Token | Size | Weight | Line-height | Letter-spacing | Used for |
|-------|------|--------|-------------|----------------|---------|
| `typography/body01` | 14px | 400 | 20px | -0.06px | Label text |
| `typography/bodyBold01` | 14px | 600 | 20px | -0.06px | Required asterisk `*` |
| `typography/body02` | 16px | 400 | 24px | 0.0121px | Input text, placeholder |
| `typography/label01` | 12px | 400 | 16px | 0px | Helper/hint text |

Font family: `Inter` (Regular and Semi Bold styles)

**CSS variable references from Figma:**
```css
--typography/body01/font-family
--typography/body01/font-weight
--typography/body01/font-size        /* 14px */
--typography/body01/line-height      /* 20px */
--typography/body01/letter-spacing   /* -0.06px */

--typography/body02/font-size        /* 16px */
--typography/body02/line-height      /* 24px */
--typography/body02/letter-spacing   /* 0.0121px */

--typography/label01/font-size       /* 12px */
--typography/label01/line-height     /* 16px */

--typography/bodyBold01/font-weight  /* semi-bold, 600 */
```

---

## Spacing (hardcoded — no tokens found)

| Property | Value | Applied to | Status |
|----------|-------|------------|--------|
| padding-x | 16px | Input field | ⚠ HARDCODED |
| padding-y | 12px | Input field | ⚠ HARDCODED |
| border-radius | 6px | Input field | ⚠ HARDCODED |
| label-to-field gap | 4px | Vertical spacing | ⚠ HARDCODED |
| icon-to-input gap | 8px | Search input only | ⚠ HARDCODED |
| resize grip size | 5×5px | Text area only | ⚠ HARDCODED |

> Variables API was unavailable during extraction (REST API permission error; Desktop Bridge not connected). These hardcoded values may map to spacing tokens if the Variables API is enabled. Re-extract when access is available.

---

## Size variants

### Text input heights

| Figma size | OX size | Total height |
|-----------|---------|-------------|
| Large | `large` | 92px |
| Medium | `medium` | 84px |
| Small | `small` | 76px |

### Text area heights

| Figma size | OX size | Total height | Inner textarea height |
|-----------|---------|-------------|----------------------|
| Large | `large` | 156px | ~88px |
| Medium | `medium` | 124px | *(not explicitly captured)* |
| Small | `small` | 90px | *(not explicitly captured)* |

### Search input heights

| Figma size | Total height |
|-----------|-------------|
| Large | 92px |
| Medium | 84px |
| Small | 76px |

---

## Tokens not captured

The following are expected to exist but were not captured (Variables API unavailable):

| Expected token | Used for |
|----------------|---------|
| Focus ring / border color | Blue outline in Focus state |
| Error border color | Red border in Error state |
| Disabled background | Greyed field in Disabled state |
| Read-only background | Slightly muted field in Read Only state |
| `textColor02` dark value | Placeholder + hint text in dark mode |
| `error01` dark value | Error state in dark mode |

---

_Source: Oxygen MCP · Figma design context · Extracted 2026-04-29_
