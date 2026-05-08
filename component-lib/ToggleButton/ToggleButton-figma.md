---
component: ToggleButton
package: "@8x8/oxygen-toggleButton"
category: form_inputs
role: figma
role_description: "Figma design spec — anatomy, variant axes, token bindings, and spacing extracted from Figma"
pipeline_stage: blocked
pipeline_note: "Audit verdict NO — resolve CONFLICTs before rewrite"
audit_verdict: NO
siblings:
  - "[[ToggleButton/props]]"
  - "[[ToggleButton/examples]]"
  - "[[ToggleButton/tokens]]"
  - "[[ToggleButton/accessibility]]"
  - "[[ToggleButton/ToggleButton-pui]]"
  - "[[ToggleButton/ToggleButton-audit]]"
tags:
  - oxygen
  - component/ToggleButton
  - role/figma
  - stage/blocked
  - category/form_inputs
---
<!-- SOURCE: Figma MCP + figma-console MCP -->
<!-- FILE KEY: 5YihJ5WuDvnvrlrRMC4sBp -->
<!-- NODE IDs: 51776:7455 (component canvas) · 50606:95349 (examples page) -->
<!-- EXTRACTED: 2026-04-29 -->
<!-- COMPONENT: ToggleButton -->
<!-- COLOR STRATEGY: A (≤3 state variants per element — one table per element, states as rows) -->

# ToggleButton — Figma Design Spec

> **See also:** [props.md](./props.md) · [tokens.md](./tokens.md) ·
> [examples.md](./examples.md) · [accessibility.md](./accessibility.md)

---

## Visual reference

<!-- Screenshots captured from Figma node 51776:7455 (component canvas) -->

The component canvas contains three component sets:
- **Toggle Input** — switch-only (40×24px), no label
- **Toggle** — switch + label (148×24px default)
- **Toggle Group** — wrapper with header/slot/footer structure (320px wide)

---

## Anatomy

### Toggle Input (switch-only component, 40×24px)

| # | Type | Name | Role | Notes |
|---|------|------|------|-------|
| 1 | frame | Toggle Base | structural | Rounded pill, 24px border-radius; background changes by state |
| 2 | frame | Toggle Knot | structural | Circular thumb; left=off (10% from left), right=on (10% from right); 3 image variants (normal, disabled-light, disabled-dark) |
| 3 | frame | Focus ring | optional slot | Visible only when `isFocus=true` and `isDisabled=false`; 2px box-shadow ring on the switch |

### Toggle (switch + label, 148×24px default)

| # | Type | Name | Role | Notes |
|---|------|------|------|-------|
| 1 | instance | Toggle Input | fixed sub-component | 40×24px switch (see above); shrink-0 |
| 2 | frame | LabelWrapper | structural | py-2px vertical padding wrapper; items-start |
| 3 | instance | Form Controls Label | content element | 14px Inter Regular; disabled state uses `disabled02` color |
| 4 | frame | Focus ring | optional slot | Covers **entire** toggle + label area (not just switch); `isFocus=true` only |

### Toggle Group (320px wide)

| # | Type | Name | Role | Notes |
|---|------|------|------|-------|
| 1 | frame | Toggle Group Label | optional slot | `header` boolean toggle; contains label text + optional info icon button |
| 2 | instance | Slot | content element | Placeholder — swapped with actual toggle content via instance swapper |
| 3 | frame | Toggle Group Feedback Text | optional slot | `footer` boolean toggle; shows helper message or error message depending on `isError` |

---

## API — Component properties

### Variant axes

#### Toggle Input

| Property | Values | Default |
|----------|--------|---------|
| Mode | Light, Dark | Light |
| isOn? | false, true | false |
| isDisabled? | false, true | false |
| isFocus? | false, true | false |

#### Toggle (with label)

| Property | Values | Default |
|----------|--------|---------|
| Mode | Light, Dark | Light |
| isOn? | false, true | false |
| isDisabled? | false, true | false |
| isFocus | false, true | false |

#### Toggle Group

| Property | Values | Default |
|----------|--------|---------|
| Mode | Light, Dark | Light |
| isError | False, True | False |

### Boolean toggles (Toggle Group)

| Property | Default | Notes |
|----------|---------|-------|
| header | true | Shows/hides the Toggle Group Label (label + info icon button) |
| footer | true | Shows/hides the feedback text area (helper or error message) |

### Instance swap slots

| Slot | Accepted types | Notes |
|------|----------------|-------|
| Slot (Toggle Group) | Any component | Replaced with actual multi-toggle content via Figma instance swapper |

### Persistent states

| State | Figma property | OX prop |
|-------|----------------|---------|
| On / checked | `isOn?=true` | `isChecked` |
| Disabled | `isDisabled?=true` | `isDisabled` |
| Error (group) | `isError=True` | n/a — group-level only |

### Token coverage

<!-- NO COVERAGE DATA RETURNED BY figma_get_component enrich — Desktop Bridge not available -->
<!-- figma_get_component returned REST API data only; description fields missing -->

---

## Color & token bindings

<!-- COLOR STRATEGY A -->

### Toggle Base (pill background)

| State | Token | Light | Dark |
|-------|-------|-------|------|
| Default (off) | `--ui/ui33` | `#6c6862` | `#858585` |
| On / checked | `--actions/action01` | `#0056e0` | `#4687ed` |
| Disabled (any) | `--ui/ui33` | `#6c6862` | `#858585` |

### Focus ring (Toggle Input — switch only)

| State | Token | Light | Dark |
|-------|-------|-------|------|
| Focused | `--interactive/focus01` | `#0056e0` (box-shadow) | `#d7e3f9` (box-shadow) |

### Focus ring (Toggle — full component)

| State | Token | Light | Dark |
|-------|-------|-------|------|
| Focused border | `--ui/ui06` | `white` | `#171719` |
| Focused shadow | `--interactive/focus01` | `#0056e0` | `#d7e3f9` |

### Label text

| State | Token | Light | Dark |
|-------|-------|-------|------|
| Default | `--text/textcolor01` | `#26252a` | `white` |
| Disabled | `--interactive/disabled02` | `#c8c8bd` | `#666666` |

### Required asterisk

| State | Token | Light | Dark |
|-------|-------|-------|------|
| Default | `--actions/action03` | `#cb2233` | `#d83848` |

### Toggle Group — Feedback text

| Element | Token | Light | Dark |
|---------|-------|-------|------|
| Helper text | `--text/textcolor02` | `#6c6862` | `#c2c2c2` |
| Error text | `--error/error01` | `#cb2233` | `#f24d5f` |

### Text styles

| Element | Style | Size | Weight | Line height | Letter spacing |
|---------|-------|------|--------|-------------|----------------|
| Label | `typography/body01` | 14px | 400 | 20px | −0.06px |
| Required asterisk | `typography/bodyBold01` | 14px | 600 | 20px | −0.06px |
| Helper / error message | `typography/label01` | 12px | 400 | 16px | 0px |
| Group heading (slot) | `typography/heading01` | 20px | 600 | 28px | 0.0289px |

Font family: Inter (via `typography/body01/font-family`)

### Effect styles

<!-- NO EFFECT STYLES FOUND — focus ring uses box-shadow inline, not a shared effect style -->

---

## Structure & spacing

### Toggle Input container

| Property | Token | Value |
|----------|-------|-------|
| Width | — | 40px (fixed) |
| Height | — | 24px (fixed) |
| Border radius | — | 24px (fully rounded) |

### Toggle Knot

| Property | Token | Value |
|----------|-------|-------|
| Top/bottom offset | — | 16.67% of height (~4px) |
| Off: left offset | — | 10% (~4px) |
| On: right offset | — | 10% (~4px) |

### Toggle (with label) container

| Property | Token | Value |
|----------|-------|-------|
| Width | — | 148px (default) |
| Height | — | 24px (default) |
| Layout direction | — | horizontal |
| Gap (switch → label) | — | 12px |
| Label vertical padding | — | 2px top + 2px bottom |
| Alignment | — | items-start (top-aligned) |

### Toggle Group container

| Property | Token | Value |
|----------|-------|-------|
| Width | — | 320px (fixed in Figma) |
| Layout direction | — | vertical |
| Gap | — | 12px |
| Alignment | — | items-start |

### Internal spacing (from Figma usage guidelines)

| Usage | Value | Token |
|-------|-------|-------|
| Gap between stacked Toggle items | 8px | `$spacing03` |
| Gap between Toggle and adjacent Icon Button | 4px | `$spacing02` |

### Auto-layout

- **Toggle Input:** relative positioning (not auto-layout)
- **Toggle:** horizontal auto-layout, gap 12px, items-start
- **Toggle Group:** vertical auto-layout (flex-col), gap 12px, items-start

---

## Interaction states

| State | Trigger | Visual change |
|-------|---------|---------------|
| hover | pointer over | Not a separate Figma variant — implied in implementation |
| isFocused | keyboard Tab | 2px focus ring; on Toggle Input: ring around switch only; on Toggle: ring covers switch + full label area |
| isOn | activation (click/Space) | Toggle Base turns blue (`action01`); knot moves to right side |
| isDisabled | `isDisabled?=true` | Toggle Base stays gray (`ui33`); knot uses disabled-variant image; label text turns `disabled02` |
| isError (group) | `isError=True` | Footer shows `InlineValidationMessage` with error icon instead of `HelperMessage` |

---

## Design decisions & annotations

> **Toggle Switch with no label:** "Use the Toggle Input component if you don't want to include a label. It can be used in scenarios where the function of the Toggle is clear from the context or design of the interface. An example could be a cell within a table or an item in a list."

> **Multiple Toggles:** "The gap between Toggle items is 8px (represented by `$spacing03`)."

> **Toggle + Icon Button:** "Place the icon button to the right of the Toggle component. The gap between the two separate components is 4px, represented by `$spacing02`."

> **Slot component:** "This is a placeholder component. Swap me with your custom content by using the component instance swapper."

> **Toggle Group structure:** "Use the 'Slot' component to replace the content with your multi-toggle content." Documented slots: Header · Slot Content · Footer · Error.

> **Font scaling (browser):** "The font scaling option enlarges the font size, but it doesn't affect the size of the Toggle Switch. The Toggle Switch alignment remains at the top."

> **Browser zoom:** "The browser's zoom option proportionally increases the font size, Toggle Switch, and the gap between them."

> **Multiline label:** "When the text for the Toggle label extends to a second line or more, the Toggle Switch alignment stays at the top."

---

## Accessibility (from Figma annotations only)

- **Focus area:** "The focus includes the entire Toggle item, from the Toggle Switch to the label. The whole area of the item is interactive, clickable, and responsive to hover actions."
- **Keyboard (Toggle + Icon Button pair):** "As separate elements, the Toggle and the Icon Button each have a different focus state. This means that when navigating with a keyboard, the focus will shift from one to the other."
- **ARIA role:** <!-- NOT ANNOTATED IN FIGMA — inferred as `checkbox` from OX implementation -->

---

## Gaps & conflicts

| Type | Description |
|------|-------------|
| Missing data | `figma_get_component_details` failed — Desktop Bridge not running; component keys not retrieved |
| Missing data | `figma_get_variables` failed — Enterprise plan or Desktop Bridge required; token aliases not resolved from Figma source |
| Missing data | `figma_get_styles` returned 0 styles — file may not expose styles via REST API |
| Missing annotation | No explicit ARIA role annotated in Figma — inferred from OX implementation |
| Missing annotation | Hover state is not a separate Figma variant; visual change not documented in Figma |
| Conflict | Figma `isOn?` property vs OX `isChecked` prop — same concept, different naming convention |
| Conflict | Figma `ToggleButtonGroup` shows `isError` variant but OX `ToggleButtonGroup` has no `isError` prop — group-level error may require custom wrapping |
| Incomplete data | Token coverage % not available (requires Desktop Bridge) |

---

_Source: Figma MCP · figma-console MCP · Extracted 2026-04-29_
