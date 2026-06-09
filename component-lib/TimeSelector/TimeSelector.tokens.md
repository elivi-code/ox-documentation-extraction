---
parent: "[[TimeSelector]]"
section: tokens
component: TimeSelector
pipeline_stage: draft
tags:
  - oxygen
  - component/TimeSelector
  - role/spoke
  - section/tokens
  - category/date_time
---

<!-- source: figma-only -->

> **Data source:** Tokens resolved from the UI-Foundations library (`iVY5nI8JAxM05Apnnvozzs`) via Desktop Bridge, collection **Semantic Colors**. Primitive aliases (e.g. `color/blue/blue05`) are the raw values these semantic tokens point to.

<!-- STUB:GAP-007 source="Cross-reference token names against the @8x8/oxygen-tokens package or the design-token catalog to confirm exact CSS custom property names used at runtime. Current names use Figma variable casing (e.g. --text/textColor01) which may differ from OX design-token package identifiers." -->
<!-- STUB:GAP-010 source="Token coverage % must be derived manually by comparing the hardcoded values list against the total number of design properties in the component. The UI-components Figma file has 0 local variables; all tokens are from the external UI-Foundations library, which is not queryable via Desktop Bridge when UI-components is the active file." -->

---

## Color tokens

### Input container background

| Token | Light value | Light alias | Dark value | Dark alias |
|-------|-------------|------------|------------|------------|
| `--ui/ui05` | `#F4F3EE` | `color/offWhite/offWhite10` | `#2F2E32` | `color/purple/purple02` |
| `--interactive/disabled01` *(disabled state)* | `#C8C8BD` | `color/offWhite/offWhite08` | `#C2C2C2` | `color/gray/gray08` |

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

### Light mode

| Element | Rest | Focus | Disabled | Error |
|---------|------|-------|----------|-------|
| Input bg | `--ui/ui05` `#F4F3EE` | `--ui/ui05` `#F4F3EE` | `--interactive/disabled01` `#C8C8BD` | `--ui/ui05` `#F4F3EE` |
| Input border | none | `--interactive/focus01` `#0056E0`, 2 px | none | `--error/error01` `#CB2233`, 2 px |
| Input text | `--text/textColor02` `#6C6862` | `--text/textColor02` `#6C6862` | `--interactive/disabled04` `#8D8B7E` | `--text/textColor02` `#6C6862` |
| Label | `--text/textColor01` `#26252A` | `--text/textColor01` `#26252A` | `--text/textColor01` `#26252A` | `--text/textColor01` `#26252A` |
| Asterisk / error | `--error/error01` `#CB2233` | `--error/error01` `#CB2233` | `--error/error01` `#CB2233` | `--error/error01` `#CB2233` |

### Dark mode

| Element | Rest | Focus | Disabled | Error |
|---------|------|-------|----------|-------|
| Input bg | `--ui/ui05` `#2F2E32` | `--ui/ui05` `#2F2E32` | `--interactive/disabled01` `#C2C2C2` | `--ui/ui05` `#2F2E32` |
| Input border | none | `--interactive/focus01` `#D7E3F9`, 2 px | none | `--error/error01` `#F24D5F`, 2 px |
| Input text | `--text/textColor02` `#C2C2C2` | `--text/textColor02` `#C2C2C2` | `--interactive/disabled04` `#858585` | `--text/textColor02` `#C2C2C2` |
| Label | `--text/textColor01` `#FFFFFF` | `--text/textColor01` `#FFFFFF` | `--text/textColor01` `#FFFFFF` | `--text/textColor01` `#FFFFFF` |
| Asterisk / error | `--error/error01` `#F24D5F` | `--error/error01` `#F24D5F` | `--error/error01` `#F24D5F` | `--error/error01` `#F24D5F` |

---

## Typography tokens

| Element | Token | Value |
|---------|-------|-------|
| Label | `--typography/body01/font-family` | Inter Regular |
| Label | `--typography/body01/font-size` | 14 px |
| Label | `--typography/body01/font-weight` | 400 |
| Label | `--typography/body01/line-height` | 20 px |
| Label | `--typography/body01/letter-spacing` | −0.06 px |
| Required asterisk | `--typography/bodybold01/font-family` | Inter Semi Bold |
| Required asterisk | `--typography/bodybold01/font-weight` | 600 |
| Input value (Small) | `--typography/label01/font-size` | 12 px |
| Input value (Small) | `--typography/label01/line-height` | 16 px |
| Input value (Medium) | `--typography/body01/font-size` | 14 px |
| Input value (Medium) | `--typography/body01/line-height` | 20 px |
| Input value (Large) | `$body02` | 16 px, lh 24 px, ls −0.176 px |
| Hint / Error text | `--typography/font-family/sans` | Inter Regular |
| Hint / Error text | `--typography/label01/font-size` | 12 px |
| Hint / Error text | `--typography/label01/line-height` | 16 px |
| Hint / Error text | `--typography/label01/letter-spacing` | 0 px |

---

## Size variant token summary

| Figma size | Code `size` | Input height | Input width | Padding | Font style |
|------------|-------------|-------------|-------------|---------|------------|
| Small | `"small"` | 32 px | 80 px | 8 px all | `$label01` 12 px / lh 16 px |
| Medium | `"default"` | 40 px | 97 px | 12 px H / 8 px V | `$body01` 14 px / lh 20 px |
| Large | *(not in API)* | 48 px | 120 px | 16 px H / 12 px V | `$body02` 16 px / lh 24 px |

---

## Hardcoded values (no token binding)

| Element | Value | Note |
|---------|-------|------|
| Input container border-radius | 6 px | Should map to a border-radius token |
| Icon button border-radius | 6 px | Should map to a border-radius token |
| Focus ring border-width | 2 px | Likely intentional |
| All padding / spacing values | See [[TimeSelector.anatomy]] | Hardcoded in Figma |
