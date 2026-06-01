---
parent: "[[Accordion]]"
section: anatomy
---

## Anatomy

### Top-level structure

| # | Type | Name | Role | Notes |
|---|---|---|---|---|
| 1 | frame | `_header` | Fixed sub-component | Clickable header row. Always present |
| 2 | frame | `Scroll content` | Structural | Visible when expanded. Holds content slot + optional scrollbar |
| 3 | instance | `Content / Slot` | Content — instance swap | Placeholder; swap with custom content |
| 4 | instance | `Scrollbar_Mac OS` | Optional slot | Figma `scrollbar?` toggle (default `false`) |
| 5 | frame | `Dividers` | Structural / decorative | Bottom separator. Figma `divider?` toggle (default `true`) |

### `_header` atom (`8298:8979`)

| # | Type | Name | Role | Notes |
|---|---|---|---|---|
| 1 | instance | `Icon` | Optional slot — instance swap | Left icon. `icon?` toggle (default `true`). Maps to `iconLeft` |
| 2 | text | `Title` | Content element | Primary label. `--typography/bodyBold01` |
| 3 | frame | `AI badge` | Optional slot | `AIBadge?` toggle (default `false`). Star icon + "AI" label. No documented code prop (GAP-004) |
| 4 | frame | `Secondary info` | Optional slot | Right text. `rightText?` toggle (default `true`). Maps to `text` |
| 5 | instance | `arrow-down` | Fixed sub-component | Chevron. Rotates 180° when expanded |
| 6 | frame | `Focus ring` | Structural | 2px border overlay. Visible in `state=focus` only |

---

## Variant axes

### `Accordion` component set (`44417:100356`)

| Property | Values | Default |
|---|---|---|
| `mode` | `light`, `dark` | `light` |
| `isOpen?` | `true`, `false` | `false` |

> **Code mapping:** Figma `isOpen?` → code prop `isExpanded`.

### `_header` atom variant axes

| Property | Values | Default |
|---|---|---|
| `mode` | `light`, `dark` | `light` |
| `state` | `rest`, `hover`, `focus`, `disabled` | `rest` |
| `isOpen?` | `true`, `false` | `false` |

### `_header` atom boolean toggles

| Property | Default |
|---|---|
| `icon?` | `true` |
| `rightText?` | `true` |
| `AIBadge?` | `false` |

### `_header` atom instance swap slot

| Slot | Accepted | Default |
|---|---|---|
| `↳ icon` | `Icon` component | Video icon (`84161:245033`) |

---

## Interaction states

| State | Trigger | Visual change |
|---|---|---|
| `rest` | — | Background `--ui/ui06` |
| `hover` | Pointer over header | Background `--ui/ui05` |
| `focus` | Keyboard tab | `--ui/ui06` + `2px solid --interactive/focus01` ring |
| `disabled` | `state=disabled` | Text `--interactive/disabled04`; background unchanged |
| `isOpen=true` | Click to expand | Chevron rotates 180°; content area appears |

---

## Component sets in the Figma file (`8135:8877`)

| Component set | Node ID | Description |
|---|---|---|
| `Accordion` | `44417:100356` | Standard accordion |
| `Accordion custom` | `82572:13805` | `expandTrigger="arrow"` + `contentAfterTitle` slot |
| `Accordion nested` | `48782:6191` | Parent with nested children |
| `Accordion nested custom` | `82572:13785` | Custom nested accordion |
| `Accordion nested child` | `48782:6353` | Inner accordion for nested variants |
| `_header` | `8298:8979` | Header atom with all states |
| `_headerCustom` | `82572:13829` | Header atom for custom variant |

<!-- STUB:GAP-014 source="Run figma_get_component on node 82572:13829 (_headerCustom) to extract its properties. Confirm whether contentAfterTitle slot maps to this atom." -->

---

## Spacing

| Property | Value | Notes |
|---|---|---|
| Header height | `48px` | Fixed |
| Header padding horizontal | `16px` | |
| Header padding vertical | `14px` | |
| Content padding top | `8px` | |
| Content padding bottom / horizontal | `16px` | |
| Gap (icon → content → arrow) | `12px` | |
| Gap (title → AI badge) | `4px` | |
| Icon / arrow size | `20px` | |
| Scrollbar width | `12px` | When `scrollbar?=true` |
| Focus ring | `2px solid` | `--interactive/focus01` |

<!-- SKIP:GAP-007 type=DOC_GAP manual depends_on=GAP-003 — Spacing values are raw Figma measurements; not confirmed whether token-bound or hardcoded. Component owner confirmation needed. -->

No density variants. Single header height of `48px`.
