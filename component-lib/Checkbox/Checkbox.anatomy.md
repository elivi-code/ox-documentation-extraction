---
parent: "[[Checkbox]]"
section: anatomy
---

## Anatomy

Three component sets are defined in Figma (file `5YihJ5WuDvnvrlrRMC4sBp`, node `51776:5078`):

| Set | Node | Role |
|-----|------|------|
| **Checkbox Input** | `51776:5081` | The bare 20 × 20 px input square — no label. Used as a sub-element inside Checkbox and CheckboxGroup. |
| **Checkbox** (full) | `51776:5160` | Checkbox Input + label text, composed horizontally. |
| **Checkbox Group** | `52682:566` | Container for multiple Checkbox items with optional `header`, `footer`, and error state. |

### Parts

1. **Group label** *(optional)* — `<legend>` (or equivalent) of a `CheckboxGroup`; the `header` slot in Figma (default `true`). Provides the accessible name for the set.
2. **Selected checkbox** — 20 × 20 px square filled with `ui/ui22` and a white check glyph.
3. **Unselected checkbox** — 20 × 20 px square with a 2 px `ui/ui21` border on transparent background.
4. **Label** — action text in `text/textColor01`, positioned to the **right** of the input. Maps to the `label` prop.
5. **Info icon button + tooltip** *(optional)* — rendered when `infoBoxText` is set; a separate keyboard focus stop named by `infoBoxButtonLabel`.
6. **Focus ring** — 2 px `interactive/focus01` outline on keyboard focus.

## Variants & states

### Variant axes (Checkbox Input & Checkbox, 24 variants each)

| Property | Type | Default | Values | Maps to |
|----------|------|---------|--------|---------|
| Mode | VARIANT | Light | Light, Dark | theme |
| State | VARIANT | Rest | Rest, Hover | transient (CSS only) |
| isChecked | VARIANT | False | False, True | `isChecked` prop |
| isIndeterminate | VARIANT | False | False, True | `isIndeterminate` prop |
| isDisabled | VARIANT | False | False, True | `isDisabled` prop |
| isFocused | VARIANT | False | False, True | transient (CSS only) |

Hover and isFocused are only defined for enabled states — disabled variants have no Hover/Focus.

### Checkbox Group variant axes (4 variants)

| Property | Type | Default | Values |
|----------|------|---------|--------|
| header | BOOLEAN | true | true, false |
| footer | BOOLEAN | true | true, false |
| Mode | VARIANT | Light | Light, Dark |
| isError | VARIANT | False | False, True |

### State matrix

| # | State | Trigger | Visual change | Token |
|---|-------|---------|---------------|-------|
| 1 | Unchecked / Rest | Default | 2 px border, transparent fill | `ui/ui21` |
| 2 | Hover | Pointer over | Border / fill brightens (transient) | (variant only) |
| 3 | Focus | Keyboard `Tab` | 2 px outline ring | `interactive/focus01` |
| 4 | Checked | `isChecked={true}` | Filled square, white check glyph | `ui/ui22` |
| 5 | Indeterminate | `isIndeterminate={true}` | Filled square, white dash glyph | `ui/ui22` |
| 6 | Disabled | `isDisabled={true}` | Muted fill, no hover/focus | `interactive/disabled02` |
| 7 | Error *(group)* | `CheckboxGroup` `isError` (Figma) | Red border + error message | `error/error01` |

## Structure & spacing

| Element | Width | Height |
|---------|-------|--------|
| Input control (each variant) | 20 px | 20 px |
| Full row (input + label) | 128 px (Figma master; label takes intrinsic width at runtime) | 20 px |
| Group item (each Figma variant) | 320 px | 168 px |

- Padding between group label and first item: `$spacing04` (verbatim from Oxygen docs).
- Padding between successive item labels (vertical list): `$spacing03` (verbatim from Oxygen docs).

<!-- STUB:GAP-004 source="Re-run get_design_context on node 51776:5081 with Figma Desktop connected to get auto-layout gap value for input-to-label spacing." -->
> **Unmeasured (GAP-004).** The exact horizontal gap between the input square and its own label is
> not captured — `get_design_context` was unavailable at extraction. Do not hand-assert a px value.

<!-- STUB:GAP-005 source="Run Figma Desktop Bridge plugin; retry figma_get_component to surface component description/design intent." -->
> **Design intent unavailable (GAP-005).** No component descriptions or design annotations were
> returned by the Figma API (known limitation without the Desktop Bridge).
