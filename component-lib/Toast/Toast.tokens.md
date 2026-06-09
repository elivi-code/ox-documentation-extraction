---
component: Toast
parent: "[[Toast]]"
section: tokens
role: spoke
pipeline_stage: spec_ready
audit_verdict: partial
siblings:
  - "[[Toast.props]]"
  - "[[Toast.anatomy]]"
  - "[[Toast.usage]]"
  - "[[Toast.accessibility]]"
  - "[[Toast.platform]]"
  - "[[Toast.composition]]"
tags:
  - oxygen
  - component/Toast
  - role/spoke
  - stage/spec_ready
---

<!-- source: figma-only -->

Token values resolved via Figma plugin API (`getVariableByIdAsync`) traversing the alias chain from the UI-components file (`5YihJ5WuDvnvrlrRMC4sBp`) into the linked UI-Foundations library (`iVY5nI8JAxM05Apnnvozzs`). All confirmed values are from Figma — not inferred. OX MCP returned no token matches for the keyword `toast`.

---

## Notification — Container tokens

| Element | Semantic token | Primitive (Light) | Hex (Light) | Primitive (Dark) | Hex (Dark) |
|---------|---------------|-------------------|-------------|------------------|------------|
| Background fill | `ui/ui07` | `color/offWhite/offWhite02` | `#26252a` | `color/gray/gray10` | `#f1f1f1` |
| Drop shadow | `ui/shadow01` | *(direct value)* | `rgba(41,41,41,0.25)` | *(direct value)* | `rgba(20,20,20,1.0)` |
| Title + description text | `text/textColor09` | `color/pure/white` | `#ffffff` | `color/pure/black` | `#000000` |
| Status icon fill | `icon/icon05` | `color/pure/white` | `#ffffff` | `color/gray/gray02` | `#292929` |
| Action links | `actions/action10` | `color/blue/blue08` | `#99bbf3` | `color/blue/blue05` | `#0056e0` |

> **Inverted background by design** — Light mode background is dark (`#26252a`), Dark mode background is light (`#f1f1f1`), so the toast always contrasts with the main app canvas.

---

## Notification — Left indicator bar (type-specific)

| `type` prop | Semantic token | Primitive (Light) | Hex (Light) | Primitive (Dark) | Hex (Dark) |
|-------------|---------------|-------------------|-------------|------------------|------------|
| `"success"` | `success/success02` | `color/green/green04` | `#189b55` | `color/green/green03` | `#12743f` |
| `"error"` | `error/error02` | `color/red/red07` | `#f24d5f` | `color/red/red05` | `#cb2233` |
| `"warning"` | `warning/warning01` | `color/yellow/yellow06` | `#f8ae1a` | `color/yellow/yellow03` | `#9f701c` |
| `"info"` | `info/info01` | `color/offWhite/offWhite09` | `#ebeae1` | `color/gray/gray05` | `#666666` |
| `"loading"` | `actions/action06` | `color/blue/blue07` | `#4687ed` | `color/blue/blue05` | `#0056e0` |

> Warning icon vector fill uses `warning/warning03` — in Light mode this resolves to the same `color/yellow/yellow06` primitive as `warning/warning01`.

---

## Notification — Typography tokens

| Style | Token prefix | Size | Weight | Line-height | Letter-spacing |
|-------|-------------|------|--------|-------------|----------------|
| Title | `typography/bodyBold01/` | 14px | 600 (semi-bold) | 20px | -0.06px |
| Description | `typography/body01/` | 14px | 400 (regular) | 20px | -0.06px |
| CTA links | `typography/bodyBold01/` | 14px | 600 (semi-bold) | 20px | -0.06px |
| Loading text | `typography/body01/` | 14px | 400 (regular) | 20px | -0.06px |

---

## Hardcoded structural values (no token bindings)

<!-- STUB:GAP-008 source="Flag to Figma design owner: container width (320px), indicator width (4px), icon container size (24px), and border-radius (6px) should be bound to spacing/radius tokens. Spacing values (padding, gaps) also hardcoded." -->

| Element | Property | Hardcoded value | Flag |
|---------|----------|-----------------|------|
| Container | width | 320px | Should be a size token or responsive constraint |
| Indicator bar | width | 4px | Should be a spacing token |
| Icon container | size | 24px | May map to an icon-size token |
| Container | border-radius | 6px | Should reference a radius token |
| Padding | left / right / top-bottom | 16px / 12px / 8px | Should be spacing tokens |
| Gaps | outer row / inner content / icon→text / text items / CTA | 12px / 16px / 8px / 8px / 8px,16px | Should be spacing tokens |

---

## InlineNotification — Indicator bar by type

Values confirmed from `figma_get_component_for_development` layer data. Semantic token names inferred by cross-referencing hex values against Notification tokens; marked *(inferred)*. InlineNotification uses a **non-inverted** theme, so Light/Dark hex values are swapped relative to the Notification table.

| `Type` | Variable ID (local) | Light hex | Dark hex | Inferred token |
|--------|---------------------|-----------|----------|----------------|
| Success | `20136:304` | `#127440` | `#189B55` | `success/success02` *(inferred — Light/Dark swapped vs Notification)* |
| Error | `20136:303` | `#CB2233` | `#F24D5F` | `error/error02` *(inferred — swapped)* |
| Warning | `20136:305` | `#F8AE1A` | `#F8AE1A` | `warning/warning01` *(inferred — same hex in both modes)* |
| Info | `20136:484` | `#6C6862` | `#D8D8D8` | Unresolved — variable ID out of range of other type tokens |
| Loading | `20136:294` | `#0056E0` | `#4687ED` | `actions/action06` *(inferred — swapped)* |

## InlineNotification — Container tokens

| Element | Variable ID (local) | Light hex | Dark hex | Inferred token |
|---------|---------------------|-----------|----------|----------------|
| Background fill | `20136:267` | `#FFFFFF` | `#171619` | Unresolved |
| Border stroke | `20136:253` | `#EBEAE1` | `#666666` | Unresolved |

<!-- STUB:GAP-010 source="With Figma Desktop Bridge plugin running, call getVariableByIdAsync for variable IDs 20136:267 (background), 20136:253 (border), and 20136:484 (Info indicator) to resolve semantic token names. Update this table once resolved." -->
