<!-- SOURCE: Figma MCP + figma-console MCP -->
<!-- FILE KEY: 5YihJ5WuDvnvrlrRMC4sBp -->
<!-- NODE ID: 47175:1414 (canvas) / 48432:43576 (Popover window) -->
<!-- EXTRACTED: 2026-05-08 -->
<!-- COMPONENT: PopoverMenu -->
<!-- COLOR STRATEGY: B (states as columns, elements as rows — multiple state/mode combos) -->

# PopoverMenu — Figma Design Spec

> **See also:** [props.md](./props.md) · [tokens.md](./tokens.md) ·
> [examples.md](./examples.md) · [accessibility.md](./accessibility.md)

---

## Visual reference

<!-- SCREENSHOT UNAVAILABLE — screenshot captured visually via Figma MCP but could not be saved to disk; figma-console Desktop Bridge was not connected during extraction -->

---

## Anatomy

The Figma canvas (node `47175:1414`) contains two distinct structural layers:

1. **Popover window** — the floating panel shell (node `48432:43576`)
2. **List item variants** — the menu item components that populate the panel's `Slot`

### Popover window

The container shell with configurable header, scrollable content area, and footer.

| # | Type | Name | Role | Notes |
|---|------|------|------|-------|
| 1 | frame | `_header` | optional slot | Shown when `header=true`; contains title row + search input + bottom divider |
| 1a | frame | `Title` | structural | Flex row; holds title text node + close icon button |
| 1b | frame | `Input` | content | Search text field (label: "Search placeholder") |
| 1c | frame | `Dividers` | structural/decorative | 1px divider line separating header from content |
| 2 | frame | `Content` | fixed sub-component | Always present; wraps the Slot and optional Scrollbar |
| 2a | instance | `Slot` | content element (instance swap) | Placeholder — intended to be swapped with actual list content |
| 2b | frame | `Scrollbar_Mac OS` | optional slot | Shown when `scroll=true`; 12px wide Mac-style scrollbar |
| 3 | frame | `_footer` | optional slot | Shown when `footer=true`; contains top divider + Clear/Cancel/Apply buttons |
| 3a | frame | `Dividers` | structural/decorative | 1px divider line separating content from footer |
| 3b | frame | `Buttons` | structural | Flex row; holds Clear (label button), Cancel (label button), Apply (filled button) |

### Sub-component: List item types

Eight list item variants are defined on the canvas. Each is 296 × 40px (except Collapsible in open state: 296 × 108px).

| # | Type | Name | States | Selection variants |
|---|------|------|--------|--------------------|
| 1 | frame | `List item/Single Action or Select` | rest, hover, active, focus, disabled | true, false |
| 2 | frame | `List item/Destructive` | rest, hover, active, focus, disabled | — |
| 3 | frame | `List item/Checkbox` | rest, hover, active, focus, disabled | true, false, indeterminate |
| 4 | frame | `List item/Radio` | rest, hover, active, focus, disabled | true, false |
| 5 | frame | `List item/Add Item` | rest, hover, active, focus, disabled | — |
| 6 | frame | `List item/Sub Menu` | rest, hover, active, focus, disabled | — |
| 7 | frame | `List item/Collapsible` | rest, hover, active, focus, disabled | open: yes/no |
| 8 | frame | `List item/Remove Item` | rest, hover, active, focus, disabled | — |

### Sub-component: Section header and divider

| # | Type | Name | Variants |
|---|------|------|----------|
| 1 | frame | `Section header and divider/Section header` | type: subtle, bold × mode: light, dark; 312 × 32px |
| 2 | frame | `Section header and divider/Divider` | mode: light, dark; 312 × 9px |

### Sub-component: Empty state and spinner

| # | Type | Name | Notes |
|---|------|------|-------|
| 1 | frame | `Empty state and spinner/Spinner` | 312 × 100px; loading state placeholder |
| 2 | frame | `Empty state and spinner/Empty state` | 312 × 138px; no-results placeholder |

### Atoms

| # | Type | Name | Notes |
|---|------|------|-------|
| 1 | frame | `Options` | Leading visuals (Avatar, Icon, Status) and trailing visuals (Sub Menu, Remove, Add, selection indicators) |
| 2 | frame | `_footer` | Footer atoms: default (buttons) and custom slot types |
| 3 | frame | `_header` | Header atoms: title type and custom slot types |

---

## API — Component properties

### Variant axes (Popover window — node `48432:43576`)

| Property | Values | Default |
|----------|--------|---------|
| `mode` | `light`, `dark` | `light` |
| `footer` | `true`, `false` | `false` |
| `header` | `true`, `false` | `false` |
| `scroll` | `true`, `false` | `false` |

### Boolean toggles

| Property | Default | Notes |
|----------|---------|-------|
| `header` | false | Shows/hides the `_header` slot (title + search + divider) |
| `footer` | false | Shows/hides the `_footer` slot (divider + Clear/Cancel/Apply buttons) |
| `scroll` | false | Shows/hides the `Scrollbar_Mac OS` inside Content |

### Instance swap slots

| Slot | Accepted types | Default |
|------|---------------|---------|
| `Slot` (inside Content) | Any content — intended for list items, empty state, spinner | Placeholder frame (`Slot` component) |

### Persistent states

| State | Property name | Notes |
|-------|--------------|-------|
| Disabled | `isDisabled` (on list items) | Applied at list item level, not on the window container |

### Token coverage

- **Coverage:** ~60% (estimated — border-radius, dimensions, and padding are hardcoded; colors and typography use tokens)
- **Hardcoded values flagged:**
  - `PopoverWindow.container`: `border-radius: 6px` — no token binding; expected a `--radius/*` or `--ui/radius*` token
  - `PopoverWindow.container`: `width: 320px` — hardcoded; no width token
  - `PopoverWindow.container`: `max-height: 400px` — hardcoded
  - `PopoverWindow.container`: `max-width: 1064px` — hardcoded
  - `PopoverWindow.container`: `padding: 1px 9px` — hardcoded
  - `PopoverWindow._header Title`: `padding: 4px 12px 8px 12px` — hardcoded
  - `PopoverWindow._header Input`: `padding: 4px 12px 12px 12px` — hardcoded
  - `PopoverWindow._footer Buttons (light)`: `padding-top: 8px; padding-x: 8px` — hardcoded
  - `PopoverWindow._footer Buttons (dark)`: `padding-top: 8px; padding-x: 12px` — ⚠️ **inconsistent** between light and dark mode
  - `PopoverWindow.Scrollbar_Mac OS`: `width: 12px`, thumb `background: #c1c1c1`, track `background: #fafafa` — all hardcoded, no token

---

## Color & token bindings

<!-- COLOR STRATEGY B: elements as rows, modes as columns -->

### Container (Popover window)

| Element | Token | Light value | Dark value |
|---------|-------|-------------|------------|
| Background | `--ui/ui06` | `white` | `#171719` |
| Border | `--ui/ui01` | `#ebeae1` | `#666` |
| Box shadow | `--ui/shadow01` | `rgba(41,41,41,0.25)` 6px 0px 2px | `#141414` 8px 2px 2px |

### Header

| Element | Token | Light value | Dark value |
|---------|-------|-------------|------------|
| Title text | `--text/textcolor01` | `#26252a` | `white` |
| Title typography | `--typography/bodybold01/*` | Inter Semi Bold, 14px, 20px lh | — |
| Search field background | `--ui/ui05` | `#f4f3ee` | `#2f2e32` |
| Search placeholder text | `--text/textcolor02` | `#6c6862` | `#c2c2c2` |
| Search placeholder typography | `--typography/body01/*` | Inter Regular, 14px, 20px lh | — |
| Divider | `--ui/ui01` | `#ebeae1` | `#666` |

### Content slot (placeholder)

| Element | Token | Light value | Dark value |
|---------|-------|-------------|------------|
| Slot background | `--ui/ui23` | `#e7e3ff` | `#3c2f8e` |
| Slot border | `--ui/ui22` | `#0056e0` | `#ccddf9` |
| Slot heading text | `--text/textcolor01` | `#26252a` | `white` |
| Slot heading typography | `--typography/heading01/*` | Inter Semi Bold, 20px, 28px lh | — |
| Slot body text | `--text/textcolor02` | `#6c6862` | `#c2c2c2` |
| Slot body typography | `--typography/body01/*` | Inter Regular, 14px, 20px lh | — |

### Footer

| Element | Token | Light value | Dark value |
|---------|-------|-------------|------------|
| Footer background | `--ui/ui06` | `white` | `#171719` |
| Divider | `--ui/ui01` | `#ebeae1` | `#666` |
| Clear button text | `--actions/action03` | `#cb2233` | `#d83848` |
| Cancel button text | `--actions/action08` | `#0056e0` | `#99bbf3` |
| Apply button background | `--actions/action09` | `#0056e0` | `#4687ed` |
| Apply button text | `--text/textcolor09` | `white` | `black` ⚠️ |
| Button typography | `--typography/labelbold01/*` | Inter Semi Bold, 12px, 16px lh | — |

> ⚠️ `--text/textcolor09` resolves to `black` in dark mode on an `--actions/action09` (`#4687ed`) background — needs contrast verification.

### Text styles

| Element | Style token | Size | Weight | Line height |
|---------|-------------|------|--------|-------------|
| Header title | `--typography/bodybold01/*` | 14px | 600 | 20px |
| Search placeholder | `--typography/body01/*` | 14px | 400 | 20px |
| Slot heading | `--typography/heading01/*` | 20px | 600 | 28px |
| Footer buttons | `--typography/labelbold01/*` | 12px | 600 | 16px |

---

## Structure & spacing

### Container

| Property | Token | Value | Notes |
|----------|-------|-------|-------|
| Width | — | `320px` | Hardcoded |
| Max width | — | `1064px` | Hardcoded |
| Max height | — | `400px` | Hardcoded |
| Border radius | — | `6px` | Hardcoded |
| Padding horizontal | — | `1px` | Hardcoded |
| Padding vertical | — | `9px` | Hardcoded |
| Overflow | — | `clip` | Hardcoded |

### Internal spacing

| Element | Property | Token | Value | Notes |
|---------|----------|-------|-------|-------|
| Header title row | padding | — | `4px 12px 8px 12px` | Hardcoded |
| Header search input | padding | — | `4px 12px 12px 12px` | Hardcoded |
| Footer buttons (light) | padding | — | `8px 8px 0 8px` | Hardcoded |
| Footer buttons (dark) | padding | — | `8px 12px 0 12px` | ⚠️ Inconsistent with light |
| Gap (footer buttons group) | gap | — | `16px` | Hardcoded |
| Gap (footer button internal) | gap | — | `8px` | Hardcoded |
| Footer button padding | — | — | `8px 12px` | Hardcoded |
| Scrollbar width | — | — | `12px` | Hardcoded |

### Auto-layout

- **Container**: `flex-col`, vertical stack
- **Header**: `flex-col`, vertical stack (title → search → divider)
- **Footer buttons row**: `flex-row`, `justify-end`, `items-center`, `gap-16px`
- **List items**: `296px` wide, `40px` tall (standard); `108px` tall (Collapsible open)

### Density / size variants

No size variants exist for the Popover window container — it has a single fixed width (320px). List item height is fixed at 40px (single-line) or 108px (Collapsible expanded).

---

## Interaction states

States from list item variant names on the canvas:

| State | Trigger | Notes |
|-------|---------|-------|
| `rest` | Default | Normal resting state |
| `hover` | Pointer over list item | Background tint change |
| `active` | Pointer down / pressed | Pressed visual feedback |
| `focus` | Keyboard navigation (Tab/Arrow) | Focus ring applied |
| `disabled` | `isDisabled=true` on item | Non-interactive; reduced opacity |

---

## Design decisions & annotations

> **Popover window (Stable):** Status is Stable. Refer to [How to use slots in Figma](https://oxygen.8x8.com/blog/how-to-use-slots-in-figma) for guidance on swapping the `Slot` placeholder with actual content.

> **Slot:** "This is a placeholder component. Swap me with your custom content by using the component instance swapper."

---

## Accessibility (from Figma annotations only)

- **ARIA role:** <!-- NOT ANNOTATED IN FIGMA -->
- **Focus order:** <!-- NOT ANNOTATED IN FIGMA -->
- **Keyboard interactions:** <!-- NOT ANNOTATED IN FIGMA -->

See [accessibility.md](./accessibility.md) for full inferred accessibility documentation.

---

## Gaps & conflicts

| Type | Description |
|------|-------------|
| Missing token | `PopoverWindow.container` — `border-radius: 6px` hardcoded; no radius token binding found |
| Missing token | `PopoverWindow.container` — `width: 320px` hardcoded |
| Missing token | `PopoverWindow.container` — `max-height: 400px` and `max-width: 1064px` hardcoded |
| Missing token | All padding values inside header, footer, and container are hardcoded |
| Missing token | `Scrollbar_Mac OS` — thumb and track colors (`#c1c1c1`, `#fafafa`) hardcoded |
| Conflict | Footer button padding differs between light (`px-8px`) and dark (`px-12px`) — inconsistency in Figma source |
| Conflict | `--text/textcolor09` in dark mode resolves to `black` on `#4687ed` Apply button background — contrast ratio needs verification against WCAG 4.5:1 |
| SOURCE_GAP | `figma_get_component_details` — Popover canvas is not published as a named library component; no variant key map available |
| SOURCE_GAP | `figma_get_variables` (UI-components file) — zero popover-namespaced variables; tokens (`--ui/ui06`, `--ui/shadow01`, etc.) reside in the UI-Foundations library (file key `iVY5nI8JAxM05Apnnvozzs`), not in this file |
| SOURCE_GAP | `figma_get_styles` — zero named styles registered in the UI-components file |
| Incomplete data | Screenshot captured visually but not saved to disk (`figma-screenshot-PopoverMenu.png` absent) |
| Missing annotation | No ARIA role, focus order, or keyboard interaction annotations in Figma |
| DOC_GAP | `Divider` and `SectionHeader` sub-component props not registered in Oxygen MCP |
| DOC_GAP | `activeProp`, `disabledProp`, `placement`, `portalTargetRef`, `maxHeight` props have no descriptions in MCP source |

---

_Source: Figma MCP · figma-console MCP · Extracted 2026-05-08_
