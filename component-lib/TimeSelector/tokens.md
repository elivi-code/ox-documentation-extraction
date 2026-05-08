# TimeSelector — Tokens

> **See also:** [props.md](props.md) · [examples.md](examples.md) · [accessibility.md](accessibility.md)

> **Data source:** Tokens resolved from the UI-Foundations library (`iVY5nI8JAxM05Apnnvozzs`) via Desktop Bridge, collection **Semantic Colors**. Primitive aliases (e.g. `color/blue/blue05`) are the raw values these semantic tokens point to.

---

## Color tokens

### Input container background

| Token | Light value | Light alias | Dark value | Dark alias |
|-------|-------------|------------|------------|------------|
| `--ui/ui05` | `#F4F3EE` | `color/offWhite/offWhite10` | `#2F2E32` | `color/purple/purple02` |
| `--interactive/disabled01` _(disabled state)_ | `#C8C8BD` | `color/offWhite/offWhite08` | `#C2C2C2` | `color/gray/gray08` |

### Input border

| State | Token | Light value | Light alias | Dark value | Dark alias |
|-------|-------|-------------|------------|------------|------------|
| Focus ring | `--interactive/focus01` | `#0056E0` | `color/blue/blue05` | `#D7E3F9` | `color/blue/blue10` |
| Error border | `--error/error01` | `#CB2233` | `color/red/red05` | `#F24D5F` | `color/red/red07` |

### Text colors

| Element | Token | Light value | Light alias | Dark value | Dark alias |
|---------|-------|-------------|------------|------------|------------|
| Label text | `--text/textColor01` | `#26252A` | `color/offWhite/offWhite02` | `#FFFFFF` | `color/pure/white` |
| Placeholder / value / hint | `--text/textColor02` | `#6C6862` | `color/offWhite/offWhite05` | `#C2C2C2` | `color/gray/gray08` |
| Required asterisk / error text / error border | `--error/error01` | `#CB2233` | `color/red/red05` | `#F24D5F` | `color/red/red07` |
| Disabled text | `--interactive/disabled04` | `#8D8B7E` | `color/offWhite/offWhite06` | `#858585` | `color/gray/gray06` |
| Focus type cursor | `--text/textColor01` | `#26252A` | `color/offWhite/offWhite02` | `#FFFFFF` | `color/pure/white` |

---

## State × element token map

| Element | Rest (Light) | Focus (Light) | Disabled (Light) | Error (Light) |
|---------|-------------|---------------|-----------------|---------------|
| Input bg | `--ui/ui05` #F4F3EE | `--ui/ui05` #F4F3EE | `--interactive/disabled01` #C8C8BD | `--ui/ui05` #F4F3EE |
| Input border | none | `--interactive/focus01` #0056E0, 2px | none | `--error/error01` #CB2233, 2px |
| Input text | `--text/textColor02` #6C6862 | `--text/textColor02` #6C6862 | `--interactive/disabled04` #8D8B7E | `--text/textColor02` #6C6862 |
| Label | `--text/textColor01` #26252A | `--text/textColor01` #26252A | `--text/textColor01` #26252A | `--text/textColor01` #26252A |
| Asterisk / error | `--error/error01` #CB2233 | `--error/error01` #CB2233 | `--error/error01` #CB2233 | `--error/error01` #CB2233 |

| Element | Rest (Dark) | Focus (Dark) | Disabled (Dark) | Error (Dark) |
|---------|------------|--------------|-----------------|--------------|
| Input bg | `--ui/ui05` #2F2E32 | `--ui/ui05` #2F2E32 | `--interactive/disabled01` #C2C2C2 | `--ui/ui05` #2F2E32 |
| Input border | none | `--interactive/focus01` #D7E3F9, 2px | none | `--error/error01` #F24D5F, 2px |
| Input text | `--text/textColor02` #C2C2C2 | `--text/textColor02` #C2C2C2 | `--interactive/disabled04` #858585 | `--text/textColor02` #C2C2C2 |
| Label | `--text/textColor01` #FFFFFF | `--text/textColor01` #FFFFFF | `--text/textColor01` #FFFFFF | `--text/textColor01` #FFFFFF |
| Asterisk / error | `--error/error01` #F24D5F | `--error/error01` #F24D5F | `--error/error01` #F24D5F | `--error/error01` #F24D5F |

---

## Typography tokens

| Element | Token | Value |
|---------|-------|-------|
| Label | `--typography/body01/font-family` | Inter Regular |
| Label | `--typography/body01/font-size` | 14px |
| Label | `--typography/body01/font-weight` | 400 |
| Label | `--typography/body01/line-height` | 20px |
| Label | `--typography/body01/letter-spacing` | −0.06px |
| Required asterisk | `--typography/bodybold01/font-family` | Inter Semi Bold |
| Required asterisk | `--typography/bodybold01/font-weight` | 600 |
| Input value (Small) | `--typography/label01/font-size` | 12px |
| Input value (Small) | `--typography/label01/line-height` | 16px |
| Input value (Medium) | `--typography/body01/font-size` | 14px |
| Input value (Medium) | `--typography/body01/line-height` | 20px |
| Input value (Large) | `$body02` | 16px, lh 24px, ls −0.176px |
| Hint / Error text | `--typography/font-family/sans` | Inter Regular |
| Hint / Error text | `--typography/label01/font-size` | 12px |
| Hint / Error text | `--typography/label01/line-height` | 16px |
| Hint / Error text | `--typography/label01/letter-spacing` | 0px |

---

## Size variants

| Figma size | Code `size` value | Input height | Input width | Padding | Font style |
|------------|-------------------|-------------|-------------|---------|------------|
| Small | `"small"` | 32px | 80px | 8px all | `$label01` 12px / lh 16px |
| Medium | `"default"` | 40px | 97px | 12px H / 8px V | `$body01` 14px / lh 20px |
| Large | _(not in API)_ | 48px | 120px | 16px H / 12px V | `$body02` 16px / lh 24px |

> **Gap:** `size="large"` exists in the Figma component set but has no corresponding value in the `TimeSelectorSize` enum. The Figma default size is `Large`; the code default is `"default"` (Medium).

---

## Border radius

| Element | Value | Token |
|---------|-------|-------|
| Input container | 6px | Hardcoded — no token binding found |
| Icon button (label info) | 6px | Hardcoded — no token binding found |

_Source: Oxygen MCP · Figma design context · UI-Foundations library (Desktop Bridge) · Extracted 2026-05-07_
