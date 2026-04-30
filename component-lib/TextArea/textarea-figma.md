<!-- SOURCE: Figma MCP + figma-console MCP -->
<!-- FILE KEY: 5YihJ5WuDvnvrlrRMC4sBp -->
<!-- NODE ID: 21562:34985 -->
<!-- EXTRACTED: 2026-04-29 -->
<!-- COMPONENT: TextArea -->
<!-- COLOR STRATEGY: A -->

# TextArea — Figma Design Spec

> **See also:** [props.md](./props.md) · [tokens.md](./tokens.md) · [examples.md](./examples.md) · [accessibility.md](./accessibility.md) · [textarea-pui.md](./textarea-pui.md)

---

## Visual reference

![TextArea component set showing all variants across sizes (Large/Medium/Small), states (Rest/Focus/Disabled), error states, and Light/Dark modes](screenshot — captured 2026-04-29)

<!-- Screenshot was captured by MCP and shown inline during extraction. URL is ephemeral (7-day expiry). -->

Figma URL: https://www.figma.com/design/5YihJ5WuDvnvrlrRMC4sBp/UI-components?node-id=21562-34985

---

## Anatomy

Element structure extracted from the Figma layer tree for the baseline variant (`Mode=Light, Size=Large, State=Rest, Error=False, Filled=False`).

| # | Type | Name | Role | Notes |
|---|------|------|------|-------|
| 1 | frame | Root container | Structural | Flex column, gap 4px, width 320px |
| 2 | instance | `_base_form_label` | Optional slot | Controlled by `Show Label` boolean toggle (default: true) |
| 3 | frame | `H Stack` (inside label) | Structural | Holds label text + required `*` side by side |
| 4 | text | Label text | Content element | Uses `typography/body01`, color `--text/textcolor01` |
| 5 | text | `*` (required marker) | Content element | Uses `typography/bodyBold01`, color `--error/error01` |
| 6 | instance | Icon Button (info icon) | Fixed sub-component | Tooltip/FAQ icon; rounded 6px, 2px padding |
| 7 | frame | `Input Text` | Structural | Rounded 6px, px 16 py 12, bg `--ui/ui05`; the actual textarea box |
| 8 | frame | `Text` (inner) | Content element | Height 88px (Large); holds placeholder or typed text |
| 9 | text | Placeholder text | Optional slot | Controlled by `hasPlaceholder` boolean toggle (default: true) |
| 10 | image | `grip` | Optional slot | Resize handle image; controlled by `Resize grip` boolean toggle (default: false); positioned absolute bottom-right 8px |
| 11 | frame | `Focus ring` | Structural/decorative | Absolute overlay, 2px border `--interactive/focus01`; visible in Focus state only |
| 12 | frame | `_base_form_hint` | Optional slot | Hint text below input; controlled by `Show Hint` boolean toggle (default: true) |
| 13 | text | Hint text | Content element | Uses `typography/label01`, color `--text/textcolor02` |
| 14 | frame | `Error Area` | Optional slot | Error icon + error message; visible when `Error=True` (replaces hint row) |
| 15 | image | Error icon | Decorative | Triangle exclamation icon (16×16px) |
| 16 | text | Error message text | Content element | Uses `typography/label01`, color `--error/error01` |
| 17 | frame/div | `Type indicator` | Structural/decorative | 1px wide, 24px tall cursor bar; `--text/textcolor01`; visible in Focus state only |

---

## API — Component properties

### Variant axes

| Property | Values | Default |
|----------|--------|---------|
| `Mode` | Light, Dark | Light |
| `Size` | Large, Medium, Small | Large |
| `State` | Rest, Focus, Disabled | Rest |
| `Error` | False, True | False |
| `Read Only` | False, True | False |
| `Filled` | False, True | False |

**Total variant combinations:** 72 (from component set children count)

### Boolean toggles

| Property | Default | Notes |
|----------|---------|-------|
| `Show Label` | true | Shows/hides the `_base_form_label` row |
| `Show Hint` | true | Shows/hides the `_base_form_hint` row below input |
| `Resize grip` | false | Shows/hides the resize handle image (bottom-right corner) |
| `hasPlaceholder` | true | Shows/hides the placeholder text inside the input |

### Text content properties

| Property | Default value | Notes |
|----------|--------------|-------|
| `Error text` | `"Error message goes here."` | Shown in `Error Area` when `Error=True` |
| `Placeholder` | `"Placeholder"` | Shown inside input when `Filled=False` |
| `Text` | `"Text filled"` | Shown inside input when `Filled=True` |

### Persistent states

| State | Figma variant | Oxygen prop |
|-------|--------------|-------------|
| Error | `Error=True` | `hasError={true}` |
| Disabled | `State=Disabled` | `isDisabled={true}` |
| Read-only | `Read Only=True` | `isReadOnly={true}` |

### Token coverage

<!-- NO COVERAGE DATA RETURNED — figma_get_component enrich returned component data but variables API (Enterprise plan) was not accessible, preventing full token binding analysis. -->
<!-- figma_get_component_details returned error: Desktop Bridge plugin not running. -->

All design values that were resolvable from `get_design_context` code output reference CSS variables (tokens). Two confirmed hardcoded values:
- `Input Text` font-size: `16px` (hardcoded, not a token)
- `border-radius`: `6px` (hardcoded)

---

## Color & token bindings

<!-- COLOR STRATEGY A: one table per element, states as rows (≤3 state variants) -->

### Input container background

| State | Token | Light value |
|-------|-------|-------------|
| Rest | `--ui/ui05` | `#f4f3ee` |
| Focus | `--ui/ui05` | `#f4f3ee` |
| Error (Rest) | `--ui/ui05` | `#f4f3ee` |
| Disabled | `--interactive/disabled01` | `#c8c8bd` |

### Input border

| State | Token | Light value | Width |
|-------|-------|-------------|-------|
| Rest | _(none)_ | — | — |
| Focus | `--interactive/focus01` | `#0056e0` | 2px solid |
| Error | `--error/error01` | `#cb2233` | 2px solid |
| Disabled | _(none)_ | — | — |

### Label text

| State | Token | Light value |
|-------|-------|-------------|
| All states | `--text/textcolor01` | `#26252a` |

### Required `*` marker

| State | Token | Light value |
|-------|-------|-------------|
| All states | `--error/error01` | `#cb2233` |

### Placeholder / input text

| State | Token | Light value |
|-------|-------|-------------|
| Rest / Focus | `--text/textcolor02` | `#6c6862` |
| Disabled | `--interactive/disabled04` | `#8d8b7e` |

### Hint text

| State | Token | Light value |
|-------|-------|-------------|
| All states | `--text/textcolor02` | `#6c6862` |

### Error area

| Element | Token | Light value |
|---------|-------|-------------|
| Error message text | `--error/error01` | `#cb2233` |
| Error icon | `--error/error01` (via SVG fill) | `#cb2233` |

### Text styles

| Element | Token family | Size | Weight | Line height | Letter spacing |
|---------|-------------|------|--------|-------------|----------------|
| Label | `typography/body01` | 14px | 400 | 20px | −0.06px |
| Required `*` | `typography/bodyBold01` | 14px | 600 | 20px | −0.06px |
| Input / Placeholder | `typography/body02` | **16px (hardcoded)** | 400 | 24px | 0.0121px |
| Hint / Error text | `typography/label01` | 12px | 400 | 16px | 0px |

---

## Structure & spacing

### Container

| Property | Token | Value | Notes |
|----------|-------|-------|-------|
| Width | — | 320px | Fixed in Figma; responsive in practice |
| Border radius | — | 6px (hardcoded) | Applied to `Input Text` and `Focus ring` |
| Padding horizontal | — | 16px (hardcoded) | `px-[16px]` |
| Padding vertical | — | 12px (hardcoded) | `py-[12px]` |
| Gap between label/input/hint | — | 4px (hardcoded) | Flex column gap |

### Resize grip

| Property | Value |
|----------|-------|
| Position | Absolute, bottom-right corner |
| Offset from edges | 8px (Rest/Focus state), 6px (Error state) |
| Size | 5×5px |

### Size variants (input box heights)

| Size | Total component height | Input box height | Content area height |
|------|----------------------|------------------|---------------------|
| Large | ~156px | 112px | 88px |
| Medium | ~124px | 80px | 56px |
| Small | ~90px | 46px | ~22px |

> Heights include padding (py 12px = 24px). Content area = box height − 24px.

### Auto-layout

- Direction: Vertical (column)
- Primary axis: Start (top-aligned)
- Counter axis: Stretch (full width)

---

## Interaction states

| State | Trigger | Visual change |
|-------|---------|---------------|
| Rest | Default | Background `--ui/ui05`, no border |
| Focus | Keyboard tab / pointer click | 2px border `--interactive/focus01` applied as absolute overlay (`Focus ring` node); cursor bar (`Type indicator`) appears |
| Disabled | `isDisabled=true` | Background changes to `--interactive/disabled01`, text to `--interactive/disabled04`; no border; cursor: not-allowed (expected) |
| Error | `hasError=true` | 2px border `--error/error01`; `Error Area` replaces hint row with icon + error message |
| Read Only | `isReadOnly=true` | Visual appearance same as Filled=True, Rest — no distinct border; uses `Read Only=True` variant |

---

## Design decisions & annotations

> **Text area — Node ID 21562:34985:**
> Documentation: https://oxygen.8x8.com/docs/Contribution/intro

> **Focus ring — Node ID 84709:245198:**
> "A focus ring is used to indicate the currently focused item."

> **Icon Button (info/FAQ) — Node ID 28172:41855:**
> Icon Button documentation: https://zeroheight.com/714056d2f/p/75909b-icons/b/1725fe

> **Error icon — Node ID 85729:81401:**
> Tags: exclamation, triangle, error, problem

---

## Accessibility (from Figma annotations only)

- **ARIA role:** <!-- NOT ANNOTATED IN FIGMA — inferred: native `<textarea>` = implicit `textbox` role with `aria-multiline="true"` -->
- **Focus order:** Focus ring annotation confirms component is keyboard-focusable. Tab order follows DOM order.
- **Keyboard interactions:** Focus state shows cursor bar indicator. No explicit keyboard annotation beyond focus ring description.

See [accessibility.md](./accessibility.md) for full guidance.

---

## Gaps & conflicts

| Type | Description |
|------|-------------|
| Missing token | Input text font-size is hardcoded to `16px` — not bound to a typography token variable |
| Missing token | `border-radius` (6px), padding (16px/12px), gap (4px) are all hardcoded values |
| Missing token | Resize grip offset from edges (8px / 6px) is hardcoded — slight inconsistency between error vs. rest/focus states |
| Incomplete data | `figma_get_variables` failed (Enterprise plan required) — full token alias tree unavailable |
| Incomplete data | `figma_get_component_details` failed (Desktop Bridge not running) — component key unavailable |
| Missing annotation | No accessibility annotations in Figma beyond focus ring description |
| Missing annotation | No design intent annotation explaining the `Filled` variant axis purpose |
| Missing annotation | Dark mode token values not resolved (variables API not accessible) |
| Conflict | Figma `Mode` variant axis (Light/Dark) has no direct prop counterpart in the Oxygen `Textarea` API — dark mode is controlled at theme-provider level |
| Conflict | Figma `Size` variant axis (Large/Medium/Small) has no direct Oxygen prop — component does not expose a `size` prop in the current API |
| Conflict | Figma `Filled` variant axis has no direct Oxygen prop — represents filled/empty visual state, not mapped to an API prop |

---

_Source: Figma MCP · figma-console MCP · Extracted 2026-04-29_
