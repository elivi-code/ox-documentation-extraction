---
parent: "[[TextArea]]"
section: anatomy
pipeline_stage: draft
audit_verdict: partial
tags:
  - oxygen
  - component/TextArea
  - section/anatomy
---

## Anatomy

Element structure for the baseline variant (`Mode=Light, Size=Large, State=Rest, Error=False, Filled=False`).

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
| 10 | image | `grip` | Optional slot | Resize handle image; controlled by `Resize grip` boolean toggle (default: false); absolute bottom-right 8px |
| 11 | frame | `Focus ring` | Structural/decorative | Absolute overlay, 2px border `--interactive/focus01`; visible in Focus state only |
| 12 | frame | `_base_form_hint` | Optional slot | Hint text below input; controlled by `Show Hint` boolean toggle (default: true) |
| 13 | text | Hint text | Content element | Uses `typography/label01`, color `--text/textcolor02` |
| 14 | frame | `Error Area` | Optional slot | Error icon + error message; visible when `Error=True` (replaces hint row) |
| 15 | image | Error icon | Decorative | Triangle exclamation icon (16×16px) |
| 16 | text | Error message text | Content element | Uses `typography/label01`, color `--error/error01` |
| 17 | frame/div | `Type indicator` | Structural/decorative | 1px wide, 24px tall cursor bar; `--text/textcolor01`; visible in Focus state only |

---

## Variants

### Variant axes

| Property | Values | Default |
|----------|--------|---------|
| `Mode` | Light, Dark | Light |
| `Size` | Large, Medium, Small | Large |
| `State` | Rest, Focus, Disabled | Rest |
| `Error` | False, True | False |
| `Read Only` | False, True | False |
| `Filled` | False, True | False |

**Total variant combinations:** 72 (Mode × Size × State × Error × Read Only × Filled)

### Boolean toggles

| Property | Default | Notes |
|----------|---------|-------|
| `Show Label` | true | Shows/hides the `_base_form_label` row |
| `Show Hint` | true | Shows/hides the `_base_form_hint` row below input |
| `Resize grip` | false | Shows/hides the resize handle image (bottom-right corner) |
| `hasPlaceholder` | true | Shows/hides the placeholder text inside the input |

---

## States

| State | Trigger | Visual change |
|-------|---------|---------------|
| Rest | Default | Background `--ui/ui05`, no border |
| Focus | Keyboard tab / pointer click | 2px border `--interactive/focus01` as absolute overlay; cursor bar (`Type indicator`) appears |
| Disabled | `isDisabled={true}` | Background changes to `--interactive/disabled01`, text to `--interactive/disabled04`; no border; cursor: not-allowed |
| Error | `hasError={true}` | 2px border `--error/error01`; `Error Area` replaces hint row with icon + error message |
| Read Only | `isReadOnly={true}` | Visual appearance same as Filled=True, Rest — no distinct border; uses `Read Only=True` variant |

---

## Size variants (input box dimensions)

| Size | Total component height | Input box height | Content area height |
|------|----------------------|------------------|---------------------|
| Large | ~156px | 112px | 88px |
| Medium | ~124px | ~80px | ~56px |
| Small | ~90px | ~46px | ~22px |

Heights include label row (20px lh) + 4px gap + input box + 4px gap + hint row (16px lh).

<!-- STUB:GAP-011 source="Call get_design_context on node 21562:34998 (Medium/Rest) and 21562:35010 (Small/Rest) to confirm exact padding and content area heights — Medium and Small values above are extrapolated from bounding boxes, not directly verified" -->

---

## Structure & spacing

| Property | Value | Token |
|----------|-------|-------|
| Width | 320px (Figma fixed; responsive in practice) | — |
| Border radius | 6px | Not tokenised — hardcoded |
| Padding horizontal | 16px | Not tokenised — hardcoded |
| Padding vertical | 12px | Not tokenised — hardcoded |
| Gap (label → input → hint) | 4px | Not tokenised — hardcoded |
| Resize grip offset (Rest/Focus) | 8px from edges | Not tokenised — hardcoded |
| Resize grip offset (Error) | 6px from edges | Not tokenised — hardcoded |
| Resize grip size | 5×5px | — |
| Focus ring width | 2px | Not tokenised — hardcoded |
| Focus cursor bar dimensions | 1px × 24px | Not tokenised — hardcoded |

---

## Figma reference

- **File key:** `5YihJ5WuDvnvrlrRMC4sBp`
- **Node ID:** `21562:34985`
- **URL:** https://www.figma.com/design/5YihJ5WuDvnvrlrRMC4sBp/UI-components?node-id=21562-34985

<!-- CONFLICT:GAP-007 finding="Figma Size variant axis (Large/Medium/Small) has no corresponding 'size' prop in Oxygen API — Oxygen sizes the textarea via rows/cols only; confirm whether size prop is planned or rows/cols is the intended API" HUMAN DECISION REQUIRED -->

<!-- CONFLICT:GAP-009 finding="Figma Filled variant axis (False/True) has no Oxygen prop — appears to be a derived visual state when value !== ''; confirm from Oxygen source whether Filled=True is controlled by value non-empty or by an undocumented prop" HUMAN DECISION REQUIRED -->
