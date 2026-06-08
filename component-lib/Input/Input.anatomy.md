---
parent: "[[Input]]"
section: anatomy
tags: [oxygen, component/Input, role/anatomy]
---

## Component sets

The Input canvas (`2072:14`) ships three distinct Figma component sets:

| # | Component set | Node ID | Description |
|---|---|---|---|
| 1 | Text input | `22155:36793` | Single-line free-text field |
| 2 | Text area | `21562:34985` | Multi-line textarea |
| 3 | Search input | `25655:40530` | Search-specific with leading magnifying-glass icon |

---

## Variant axes

All three component sets share these axes:

| Property | Values | Default |
|---|---|---|
| Mode | Light, Dark | Light |
| Size | Large, Medium, Small | Large |
| State | Rest, Focus, Disabled | Rest |
| Error | False, True | False |
| Read Only | False, True | False |
| Filled | False, True | False |

> **CONFLICT-001:** `Read Only` variant axis is present on Text input and Text area but **absent from Search input**. See [[Input.props]] for the isReadOnly API conflict.

---

## Boolean toggles

### Text input and Text area

| Property | Default | Notes |
|---|---|---|
| Show Label | true | Shows/hides `_base_form_label` slot (label text + required `*` + help icon) |
| Show Hint | true | Shows/hides `_base_form_hint` slot |
| hasPlaceholder | true | Shows/hides placeholder text. **`false` recommended for all new designs.** |
| Resize grip | false | **Text area only.** Reveals resize handle at bottom-right |

### Search input

| Property | Default | Notes |
|---|---|---|
| Show Label | true | Shows/hides label slot |
| Show Hint area | true | Shows/hides hint slot |
| hasPlaceholder | true | Shows/hides placeholder text |

---

## Sub-component atoms

Shared across all three component sets:

| # | Element | Node ID (example) | Token / Role |
|---|---|---|---|
| 1 | `_base_form_label` frame | `22230:37448` | Optional label slot (controlled by Show Label) |
| 2 | Label text | `I…;21562:35645` | `typography/body01`, `text/textColor01` |
| 3 | Required `*` text | `I…;21562:35646` | `typography/bodyBold01`, `error/error01` |
| 4 | Icon Button (help/faq) | `I…;71013:28942` | Fixed `iconSizeM` in label row |
| 5 | `Input Text` / `Text Field` container | varies | `bg=ui05`, `px=16`, `py=12`, `rounded=6` |
| 6 | Placeholder text | varies | Conditional on hasPlaceholder. `typography/body02`, `text/textColor02` |
| 7 | `_base_form_hint` frame | `22230:38105` | Optional hint slot (controlled by Show Hint) |
| 8 | Hint text | `I…;21562:35642` | `typography/label01`, `text/textColor02` |

---

## Layer trees

### Text input (default variant `22155:36794`)

```
Root (flex-col, gap=4px, w=320px)
├── _base_form_label  [Show Label=true]
│   ├── H Stack
│   │   ├── "Label" text  (body01, textColor01)
│   │   └── "*" text      (bodyBold01, error01)
│   └── Icon Button       (iconSizeM, faq/help icon)
├── Input Text  (bg=ui05, px=16, py=12, rounded=6)
│   └── Text  (flex, min-w)
│       └── Placeholder  [hasPlaceholder=true]  (body02, textColor02)
└── _base_form_hint  [Show Hint=true]
    └── Hint text (label01, textColor02)
```

### Text area (additional layer vs Text input)

```
Input Text  (bg=ui05, px=16, py=12, rounded=6)
├── Text  (h=88px — taller for multi-line)
│   └── Placeholder  [hasPlaceholder=true]
└── grip  [Resize grip=true]  — 5×5px resize handle at bottom-right
```

### Search input (default variant `25649:40529`)

```
Root (flex-col, gap=4px, w=320px)
├── _base_form_label  [Show Label=true]
│   └── (same as Text input)
├── Text Field  (bg=ui05, gap=8px, px=16, rounded=6)
│   ├── Search icon  (KeywordSearch — magnifying glass)
│   └── Input  (flex-1, py=12)
│       └── Placeholder  [hasPlaceholder=true]  (body02, textColor02)
└── _base_form_hint  [Show Hint area=true]
    └── Hint text (label01, textColor02)
```

---

## Interaction states

| State | Trigger | Visual change |
|---|---|---|
| Rest | Default | Field bg `ui05`, no border |
| Hover | Pointer over field | Background shifts to `hover06` |
| Focus | Keyboard tab / click into field | Blue focus ring (`interactive/focus01`) on field |
| Filled | User has typed text | Placeholder replaced by value text |
| Disabled | `isDisabled=true` | Greyed field (`interactive/disabled01`), no interaction |
| Read Only | `isReadOnly=true` | Field shows value, no edit cursor. Bg same as Rest (`ui05`) |
| Error + Rest | `hasError=true`, not focused | Red border (`error/error01`) + error message row |
| Error + Focus | `hasError=true`, focused | Blue focus ring overrides red border; **error message stays visible** |

> **Key annotation from Figma:** "When an error occurs and a user tries to change the text, the border becomes highlighted in-focus state (blue) while the error message stays visible at the bottom." Error clears only when the value becomes valid.

---

## Design decisions & annotations

> **hasPlaceholder accessibility:** "Using placeholder text alone as a method to guide user input is not considered accessible, as it can disappear once the user starts typing, reducing clarity and usability — especially for users relying on assistive technologies."

> **hasPlaceholder guidance:** "`hasPlaceholder=true` by default to preserve behaviour in current and legacy prototypes. For all new designs and prototypes, we highly recommend setting `hasPlaceholder` to false and using a proper label and helper text combination."

> **Placement:** "Make sure the input width is proportional to the content that the user has to insert and align to grid columns. The component should also be vertically aligned to other contents of the page."

---

## Gaps

<!-- STUB:GAP-014 source="Re-run figma_get_styles with Desktop Bridge connected to retrieve effect styles (shadows etc.) for Input component" -->

<!-- STUB:GAP-015 source="Run figma_get_component with Desktop Bridge running to retrieve accurate component description URL (current REST API link is generic, not component-specific)" -->
