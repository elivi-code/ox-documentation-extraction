---
parent: "[[Button]]"
section: tokens
component: Button
package: "@8x8/oxygen-button"
tags: [oxygen, component/Button, role/tokens, section/tokens]
---

# Button — Tokens

Semantic tokens from the Oxygen theme. Values shown for `light` and `dark`; `ref` is the underlying palette token.

> ⛔ **This spoke has 3 unresolved CONFLICTs (audit verdict NO).** The token tables below are authoritative for **Primary** only until GAP-001 and GAP-002 are resolved. See markers inline.

---

## Action Tokens (Background & Text)

| Token | Description | Light | Light ref | Dark | Dark ref |
|-------|-------------|-------|-----------|------|----------|
| `action01` | Primary button background | `#0056E0` | `blue05` | `#4687ED` | `blue07` |
| `action02` | Secondary button background | `#26252A` | `offwhite02` | `#C2C2C2` | `gray08` |
| `action03` | Primary danger bg; text button danger text | `#CB2233` | `red05` | `#D83848` | `red06` |
| `action06` | Primary button inverted background | `#4687ED` | `blue07` | `#0056E0` | `blue05` |
| `action08` | Text button text; icon in text button; text link | `#0056E0` | `blue05` | `#99BBF3` | `blue08` |
| `action10` | Text button inverted text; link inverted; icon inverted | `#99BBF3` | `blue08` | `#0056E0` | `blue05` |
| `action11` | Secondary button inverted background | `#C8C8BD` | `offwhite08` | `#292929` | `gray02` |
| `action12` | Primary danger inverted bg; text danger inverted text | `#D83848` | `red06` | `#CB2233` | `red05` |
| `textColor09` | Text inside primary and secondary buttons | `#FFFFFF` | `white` | `#000000` | `black` |
| `textColor11` | Text inside primary/secondary inverted buttons | `#000000` | `black` | `#FFFFFF` | `white` |
| `ui01` | Tertiary button background (also card/divider border, selected list-item bg) | `#EBEAE1` | `offwhite09` | `#666666` | `gray05` |

---

## Hover Tokens

| Token | Description | Light | Light ref | Dark | Dark ref |
|-------|-------------|-------|-----------|------|----------|
| `hover03` | Destructive control button hover | `#D83848` | `red06` | `#F24D5F` | `red07` |
| `hover04` | Success control button hover | `#4BCE88` | `green06` | `#4BCE88` | `green06` |
| `hover09` | Tertiary reversed button hover | `#F4F3EE` | `offwhite10` | `#666666` | `gray05` |
| `hover13` | Icon button hover | `#EBEAE1` | `offwhite09` | `#525252` | `gray04` |
| `hover14` | Active icon button hover; inverted icon button hover | `#57554E` | `offwhite04` | `#C2C2C2` | `gray08` |
| `hover15` | Primary button hover; text button hover text | `#0045B3` | `blue04` | `#99BBF3` | `blue08` |
| `hover16` | Secondary button hover | `#131318` | `offwhite01` | `#E0E0E0` | `gray09` |
| `hover17` | Danger primary hover; danger text button hover text | `#A21B29` | `red04` | `#F24D5F` | `red07` |
| `hover18` | Text button hover background | `#D7E3F9` | `blue10` | `#00225A` | `blue02` |
| `hover19` | Danger text button hover background | `#FAEAEC` | `red10` | `#510E14` | `red02` |
| `hover20` | Inverted primary hover; inverted text hover text; inverted link hover | `#99BBF3` | `blue08` | `#0045B3` | `blue04` |
| `hover21` | Inverted secondary button hover | `#EBEAE1` | `offwhite09` | `#141414` | `gray01` |
| `hover22` | Inverted text button hover background | `#00225A` | `blue02` | `#D7E3F9` | `blue10` |
| `hover23` | Inverted danger text button hover background | `#510E14` | `red02` | `#FAEAEC` | `red10` |
| `hover24` | Inverted danger primary button hover | `#F24D5F` | `red07` | `#A21B29` | `red04` |
| `hover25` | Inverted danger control button hover | `#F24D5F` | `red07` | `#D83848` | `red06` |

> `hover01` (primary) and `hover02` (secondary) are legacy — no longer applicable.

---

## Active/Pressed Tokens

| Token | Description | Light | Light ref | Dark | Dark ref |
|-------|-------------|-------|-----------|------|----------|
| `active03` | Danger control button active | `#A21B29` | `red04` | `#CB2233` | `red05` |
| `active09` | Tertiary reversed button active | `#C8C8BD` | `offwhite08` | `#3D3D3D` | `gray03` |
| `active12` | Icon button active (non-sticky) | `#DEDED5` | `offwhite085` | `#666666` | `gray05` |
| `active13` | Icon button active (sticky) | `#6C6862` | `offwhite05` | `#A3A3A3` | `gray07` |
| `active14` | Primary button active bg; text button active text | `#003486` | `blue03` | `#CCDDF9` | `blue09` |
| `active15` | Secondary button active background | `#131318` | `offwhite01` | `#F1F1F1` | `gray10` |
| `active16` | Danger primary button active background | `#7A141F` | `red03` | `#F5D3D6` | `red09` |
| `active17` | Inverted primary active; inverted text active bg & text; inverted link active | `#CCDDF9` | `blue09` | `#003486` | `blue03` |
| `active18` | Inverted danger primary active; inverted danger text active | `#F5D3D6` | `red09` | `#7A141F` | `red03` |
| `active19` | Inverted secondary button active | `#F4F3EE` | `offwhite10` | `#141414` | `gray01` |
| `active20` | Inverted text button active background | `#003486` | `blue03` | `#CCDDF9` | `blue09` |
| `active21` | Danger text button active text | `#A21B29` | `red04` | `#EAA7AD` | `red08` |
| `active22` | Inverted danger text button active text | `#EAA7AD` | `red08` | `#A21B29` | `red04` |
| `active23` | Inverted danger control button active | `#CB2233` | `red05` | `#A21B29` | `red04` |

> `active01` (primary) and `active02` (secondary) are legacy — no longer applicable.

---

## Token-to-Variant Quick Reference

| Variant | Rest bg | Hover bg | Active bg | Text |
|---------|---------|----------|-----------|------|
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

> **Tertiary (non-reversed):** only the rest background `ui01` is confirmed. Dedicated hover/active tokens are not documented separately — `hover09`/`active09` belong to **tertiary reversed**.

---

## Figma-annotated bindings (Color Tokens Reference page)

The Figma examples page annotates these background tokens per variant/state. Conflicts with the Oxygen theme tokens above are flagged below.

| Variant | Rest | Hover | Active | Disabled |
|---------|------|-------|--------|----------|
| Primary | `action01` | `hover15` | `active14` | `disabled01` |
| Secondary | `action01` ⚠️ | `hover16` | `active15` | `disabled01` |
| Danger (Primary+Danger) | `action03` | `hover17` | `active16` | `disabled01` |
| Text Primary | — | `hover18` | `active17` ⚠️ | — |
| Text Danger | — | `hover19` | `active17` ⚠️ | — |

<!-- CONFLICT:GAP-001 finding="Secondary rest bg: Figma reference annotates $action01 (#0056E0, blue); tokens.md specifies action02 (#26252A, near-black). Visually distinct — one source must be wrong." HUMAN DECISION REQUIRED -->
<!-- CONFLICT:GAP-002 finding="Text Primary & Text Danger active bg annotated $active17 in Figma; tokens.md defines active17 as inverted-only and documents no active bg for non-inverted text buttons." HUMAN DECISION REQUIRED -->
<!-- CONFLICT:GAP-003 finding="Figma CSS export emits var(--actions/action09) for Primary bg; tokens.md names the same hex action01. CSS path naming vs semantic token naming diverge with no documented mapping." HUMAN DECISION REQUIRED -->

---

## Disabled-state tokens

Identified by name in Figma annotations (apply across all variant disabled states):

| Token | Description |
|-------|-------------|
| `disabled01` | Disabled button background (all solid variants) |
| `disabled04` | Disabled button text / icon color (all variants) |

<!-- SKIP:GAP-014 manual="disabled01/disabled04 hex values absent from tokens.md (names only). Add hex from the Oxygen theme. Depends on GAP-001 resolution." -->
