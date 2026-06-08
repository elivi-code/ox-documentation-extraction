---
parent: "[[Checkbox]]"
section: tokens
---

## Tokens

### Color & state tokens (confirmed from Figma)

Resolved via `figma_execute` + `getVariableByIdAsync` alias-chain traversal on node `51776:5081`
(UI-components → UI-Foundations library), confirmed 2026-05-05.

| Element | Semantic token | Primitive (Light) | Hex (Light) | Primitive (Dark) | Hex (Dark) |
|---------|---------------|-------------------|-------------|------------------|------------|
| Unchecked border | `ui/ui21` | `color/offWhite/offWhite05` | `#6c6862` | `color/gray/gray08` | `#c2c2c2` |
| Checked / indeterminate fill | `ui/ui22` | `color/blue/blue05` | `#0056e0` | `color/blue/blue09` | `#ccddf9` |
| Disabled background | `interactive/disabled02` | `color/offWhite/offWhite08` | `#c8c8bd` | `color/gray/gray05` | `#666666` |
| Focus ring | `interactive/focus01` | `color/blue/blue05` | `#0056e0` | `color/blue/blue10` | `#d7e3f9` |
| Label text | `text/textColor01` | `color/offWhite/offWhite02` | `#26252a` | `color/pure/white` | `#ffffff` |
| Error border / message | `error/error01` | `color/red/red05` | `#cb2233` | `color/red/red07` | `#f24d5f` |

### Spacing tokens

| Usage | Token |
|-------|-------|
| Between group label and first checkbox | `$spacing04` |
| Between checkbox labels (vertical list) | `$spacing03` |

### State → token summary

| State | Input appearance |
|-------|-----------------|
| Unchecked rest | 2 px border `ui/ui21` on transparent bg |
| Checked / indeterminate rest | Filled with `ui/ui22` (blue), white glyph |
| Disabled (any) | Bg `interactive/disabled02`, muted appearance |
| Focus ring | 2 px outline `interactive/focus01`, inset gap `ui/ui06` |
| Error | Border + message text `error/error01` |

<!-- STUB:GAP-003 source="Verify in Oxygen theme SCSS whether Checkbox label inherits typography from a theme variable or is hardcoded. Document the mechanism in tokens.md." -->
> **Typography tokens (GAP-003).** No typography variable bindings were found on the Checkbox
> component set (only the 5 color/focus variables above). Label text typography is likely inherited
> from the theme rather than bound at component level — unconfirmed without checking the Oxygen
> theme layer. `text/textColor01` and `error/error01` were resolved from the shared token pattern
> (confirmed on Label / ToggleButton / Input extractions), not directly bound on this set.
