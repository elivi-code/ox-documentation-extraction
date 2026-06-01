---
component: Button
package: "@8x8/oxygen-button"
category: interaction
role: tokens
role_description: "Design tokens — color, spacing, and typography token bindings"
pipeline_stage: blocked
pipeline_note: "Audit verdict NO — resolve CONFLICTs before rewrite"
audit_verdict: NO
siblings:
  - "[[Button/props]]"
  - "[[Button/examples]]"
  - "[[Button/accessibility]]"
  - "[[Button/Button-figma]]"
  - "[[Button/Button-usage]]"
  - "[[Button/Button-audit]]"
tags:
  - oxygen
  - component/Button
  - role/tokens
  - stage/blocked
  - category/interaction
---
# Button — Tokens

> **See also:** [Props](props.md) · [Examples](examples.md) · [Accessibility](accessibility.md) · [Usage](Button-usage.md)

All tokens listed below are semantic tokens from the Oxygen theme. Values are shown for both `light` and `dark` themes. The `reference` column shows the underlying palette token.

---

## Action Tokens (Background & Text Colors)

| Token | Description | Light value | Light ref | Dark value | Dark ref |
|-------|-------------|-------------|-----------|------------|----------|
| `action01` | Primary button background | `#0056E0` | `blue05` | `#4687ED` | `blue07` |
| `action02` | Secondary button background | `#26252A` | `offwhite02` | `#C2C2C2` | `gray08` |
| `action03` | Primary danger button background; text button danger text | `#CB2233` | `red05` | `#D83848` | `red06` |
| `action06` | Primary button inverted background | `#4687ED` | `blue07` | `#0056E0` | `blue05` |
| `action08` | Text button text color; icon inside text button; text link color | `#0056E0` | `blue05` | `#99BBF3` | `blue08` |
| `action10` | Text button inverted text; link inverted text; icon inside text button inverted | `#99BBF3` | `blue08` | `#0056E0` | `blue05` |
| `action11` | Secondary button inverted background | `#C8C8BD` | `offwhite08` | `#292929` | `gray02` |
| `action12` | Primary danger button inverted background; text button danger inverted text | `#D83848` | `red06` | `#CB2233` | `red05` |
| `textColor09` | Text inside primary and secondary buttons | `#FFFFFF` | `white` | `#000000` | `black` |
| `textColor11` | Text inside primary and secondary inverted buttons | `#000000` | `black` | `#FFFFFF` | `white` |
| `ui01` | Tertiary button background (also card/divider border, selected list-item bg) | `#EBEAE1` | `offwhite09` | `#666666` | `gray05` |

---

## Hover Tokens

| Token | Description | Light value | Light ref | Dark value | Dark ref |
|-------|-------------|-------------|-----------|------------|----------|
| `hover01` | Primary button hover *(legacy — no longer applicable)* | `#246FE5` | `blue06` | `#4687ED` | `blue07` |
| `hover02` | Secondary button hover *(legacy — no longer applicable)* | `#6C6862` | `offwhite05` | `#F1F1F1` | `gray10` |
| `hover03` | Destructive control button hover | `#D83848` | `red06` | `#F24D5F` | `red07` |
| `hover04` | Success control button hover | `#4BCE88` | `green06` | `#4BCE88` | `green06` |
| `hover09` | Tertiary reversed button hover | `#F4F3EE` | `offwhite10` | `#666666` | `gray05` |
| `hover13` | Icon button hover | `#EBEAE1` | `offwhite09` | `#525252` | `gray04` |
| `hover14` | Active icon button hover; inverted icon button hover | `#57554E` | `offwhite04` | `#C2C2C2` | `gray08` |
| `hover15` | Primary button hover; text button hover text | `#0045B3` | `blue04` | `#99BBF3` | `blue08` |
| `hover16` | Secondary button hover | `#131318` | `offwhite01` | `#E0E0E0` | `gray09` |
| `hover17` | Danger primary button hover; danger text button hover text | `#A21B29` | `red04` | `#F24D5F` | `red07` |
| `hover18` | Text button hover background | `#D7E3F9` | `blue10` | `#00225A` | `blue02` |
| `hover19` | Danger text button hover background | `#FAEAEC` | `red10` | `#510E14` | `red02` |
| `hover20` | Inverted primary button hover; inverted text button hover text; inverted link hover text | `#99BBF3` | `blue08` | `#0045B3` | `blue04` |
| `hover21` | Inverted secondary button hover | `#EBEAE1` | `offwhite09` | `#141414` | `gray01` |
| `hover22` | Inverted text button hover background | `#00225A` | `blue02` | `#D7E3F9` | `blue10` |
| `hover23` | Inverted danger text button hover background | `#510E14` | `red02` | `#FAEAEC` | `red10` |
| `hover24` | Inverted danger primary button hover | `#F24D5F` | `red07` | `#A21B29` | `red04` |
| `hover25` | Inverted danger control button hover | `#F24D5F` | `red07` | `#D83848` | `red06` |

---

## Active/Pressed Tokens

| Token | Description | Light value | Light ref | Dark value | Dark ref |
|-------|-------------|-------------|-----------|------------|----------|
| `active01` | Primary button active *(legacy — no longer applicable)* | `#0045B3` | `blue04` | `#0056E0` | `blue05` |
| `active02` | Secondary button active *(legacy — no longer applicable)* | `#3A3A3B` | `offwhite03` | `#C2C2C2` | `gray08` |
| `active03` | Danger control button active | `#A21B29` | `red04` | `#CB2233` | `red05` |
| `active09` | Tertiary reversed button active | `#C8C8BD` | `offwhite08` | `#3D3D3D` | `gray03` |
| `active12` | Icon button active (non-sticky) | `#DEDED5` | `offwhite085` | `#666666` | `gray05` |
| `active13` | Icon button active (sticky/stays active) | `#6C6862` | `offwhite05` | `#A3A3A3` | `gray07` |
| `active14` | Primary button active background; text button active text | `#003486` | `blue03` | `#CCDDF9` | `blue09` |
| `active15` | Secondary button active background | `#131318` | `offwhite01` | `#F1F1F1` | `gray10` |
| `active16` | Danger primary button active background | `#7A141F` | `red03` | `#F5D3D6` | `red09` |
| `active17` | Inverted primary button active; inverted text button active background & text; inverted link active text | `#CCDDF9` | `blue09` | `#003486` | `blue03` |
| `active18` | Inverted danger primary button active; inverted danger text button active | `#F5D3D6` | `red09` | `#7A141F` | `red03` |
| `active19` | Inverted secondary button active | `#F4F3EE` | `offwhite10` | `#141414` | `gray01` |
| `active20` | Inverted text button active background | `#003486` | `blue03` | `#CCDDF9` | `blue09` |
| `active21` | Danger text button active text | `#A21B29` | `red04` | `#EAA7AD` | `red08` |
| `active22` | Inverted danger text button active text | `#EAA7AD` | `red08` | `#A21B29` | `red04` |
| `active23` | Inverted danger control button active | `#CB2233` | `red05` | `#A21B29` | `red04` |

---

## Token-to-Variant Quick Reference

| Variant | Rest bg token | Hover bg token | Active bg token | Text token |
|---------|--------------|----------------|-----------------|------------|
| Primary | `action01` | `hover15` | `active14` | `textColor09` |
| Secondary | `action02` | `hover16` | `active15` | `textColor09` |
| Primary (danger) | `action03` | `hover17` | `active16` | `textColor09` |
| Primary (inverted) | `action06` | `hover20` | `active17` | `textColor11` |
| Secondary (inverted) | `action11` | `hover21` | `active19` | `textColor11` |
| Text | — | `hover18` | — | `action08` |
| Text (danger) | — | `hover19` | — | `action03` |
| Text (inverted) | — | `hover22` | `active20` | `action10` |
| Text danger (inverted) | — | `hover23` | `active18` | `action12` |
| Tertiary | `ui01` | — | — | — |
| Destructive control | — | `hover03` | `active03` | — |
| Success control | — | `hover04` | — | — |
| Tertiary reversed | — | `hover09` | `active09` | — |
| Icon button | — | `hover13` | `active12` | — |
| Icon button (active/sticky) | — | `hover14` | `active13` | — |

> **Tertiary (non-reversed):** Only the rest background token `ui01` is confirmed in the Oxygen theme ("tertiary button background"). Dedicated hover/active tokens for non-reversed tertiary are not documented separately — `hover09`/`active09` belong to the **tertiary reversed** variant. Confirm with the token owner if distinct tertiary hover/active states are required.

---

_Source: Oxygen MCP · Extracted 2026-04-28_
