---
parent: "[[DateTimeRangeSelector]]"
section: anatomy
component: DateTimeRangeSelector
pipeline_stage: spec_ready
audit_verdict: "YES"
tags:
  - oxygen
  - component/DateTimeRangeSelector
  - role/spoke
  - section/anatomy
  - stage/spec_ready
  - category/date_time
---

<!-- source: figma-only -->

## Anatomy

> **Shared trigger:** Figma node `80239:8235` ("Date picker") in file `5YihJ5WuDvnvrlrRMC4sBp` is used by both `DateTimeRangeSelector` and `DateTimeSelector`. The open picker panel (calendar grid, predefined ranges, time row) is documented in [[Calendar]].

Base variant: `Mode=Light, Size=Large, State=Rest, Error=False, Filled=False` (node `80239:8236`, 320×92px)

| # | Type | Name | Role | Notes |
|---|------|------|------|-------|
| 1 | instance | `_base_form_label` | optional slot | Visible when `Show Label=true` (default). 320×20px. Label + required `*` + faq icon button |
| 2 | frame | `Dropdown` | fixed sub-component | Always present. 320×48px (Large). The date-range trigger input field |
| 3 | instance | `_base_form_hint` | optional slot | Visible when `Show Hint=true` (default). 320×16px. Hint or error text below the field |

**Container layout:** `flex-col`, `gap-[4px]` between zones, `w-[320px]`

### Sub-component: _base_form_label

| # | Type | Name | Role | Notes |
|---|------|------|------|-------|
| 1 | frame | `H Stack` | structural | Label text + required asterisk `*` |
| 2 | text | `Label` | content | `body01` token; color `--text/textcolor01` |
| 3 | text | `Required` | content | `*`; color `--error/error01`; `bodybold01` token |
| 4 | instance | `Icon Button` | content | 20×20px; faq/help icon (16×16); padding 2px; `rounded-[6px]` |

### Sub-component: Dropdown (trigger frame)

| # | Type | Name | Role | Notes |
|---|------|------|------|-------|
| 1 | frame | `Text` | structural | Horizontal flex, `gap-[8px]`, fills width |
| 2 | text/div | `Text` (inner) | content | Placeholder or selected date-range value; `body02` token |
| 3 | instance | `calendar` | content | 24×24px calendar icon; **visible in Rest only** — hidden in Hover, Focus, Error, Disabled |
| 4 | frame | `Focus ring` | optional slot | Absolute, `border-2 border-[--interactive/focus01]`; visible in Focus state only |
| 5 | frame | `Error Area` | optional slot | Below dropdown when Error=True; error message text |

---

## Variant axes

All confirmed from `componentPropertyDefinitions` on COMPONENT_SET node `80239:8235` via Desktop Bridge:

| Property | Type | Values | Default |
|----------|------|--------|---------|
| `Mode` | VARIANT | `Light`, `Dark` | `Light` |
| `Size` | VARIANT | `Large`, `Medium`, `Small` | `Large` |
| `State` | VARIANT | `Rest`, `Hover`, `Focus`, `Disabled` | `Rest` |
| `Error` | VARIANT | `False`, `True` | `False` |
| `Filled` | VARIANT | `False`, `True` | `False` |

**Note:** The API exposes only `size="large" | "small"`. The Figma `Medium` variant (40px trigger) has no direct `size` prop mapping.

### Boolean toggles

| Property | Default | Notes |
|----------|---------|-------|
| `Show Label` | `true` | Shows/hides `_base_form_label` |
| `Show Hint` | `true` | Shows/hides `_base_form_hint` |

### Text content properties

| Property | Default | Notes |
|----------|---------|-------|
| `Placeholder` | `"Select date"` | Unfilled state |
| `Text` | `"22/08/2022 12:00 AM - 23/08/2022 11:59 PM"` | Filled state — range format confirms DateTimeRangeSelector primary use |
| `Error text` | `"Error message goes here."` | Error=True state |

---

## States

| State | Trigger | Visual change | Tokens confirmed |
|-------|---------|---------------|-----------------|
| Rest | Default | Placeholder or range value on `--ui/ui05` bg; calendar icon visible | ✓ Bridge |
| Hover | Pointer over Dropdown | `--interactive/hover06` bg; calendar icon hidden | ✓ Bridge |
| Focus | Keyboard Tab | 2px focus ring `--interactive/focus01`; `inset-[-12px_-48px_-12px_-16px]`; calendar icon hidden | ✓ Bridge |
| Error | `hasError=true` | Red 2px border `--error/error01`; Error Area below; calendar icon hidden | ✓ Bridge |
| Disabled | `isDisabled=true` | `--interactive/disabled01` bg; filled text `--interactive/disabled04`; calendar icon hidden | ✓ Bridge |
| Filled | `dateTimeRange` set | Placeholder replaced by formatted range string; `--text/textcolor01` text | ✓ Bridge |

> **Calendar icon behaviour:** The calendar icon is visible **only in Rest state**. It is intentionally hidden in Hover, Focus, Error, and Disabled — this is by design, not a bug.

<!-- STUB:GAP-008 source="Designer should add annotation nodes to the Date picker Figma component explaining design intent (e.g. why 320px fixed width, why calendar icon hides on non-Rest states, why label stays active color in disabled). No automation can fix this." -->

---

## Sizes

| API value | Figma variant | Trigger height | Total height (label + dropdown + hint) |
|-----------|---------------|----------------|---------------------------------------|
| `size="large"` (default) | `Size=Large` | 48px | 92px |
| — *(no API mapping)* | `Size=Medium` | 40px | 84px |
| `size="small"` | `Size=Small` | 32px | 76px |

Width is always **320px fixed** across all sizes and states (no token).

---

## Spacing

### Container

| Property | Value | Notes |
|----------|-------|-------|
| Width | 320px | all sizes — hardcoded |
| Gap between zones | 4px | label → dropdown → hint — hardcoded |
| Flex direction | column | all |

### Dropdown (trigger)

| Property | Value | Size |
|----------|-------|------|
| Height | 48px | Large |
| Height | 40px | Medium |
| Height | 32px | Small |
| Padding horizontal | 16px | all |
| Padding vertical | 12px | Large |
| Border radius | 6px | all — hardcoded |

### Internal spacing

| Property | Value | Notes |
|----------|-------|-------|
| Text/icon gap | 8px | Between range text and calendar icon (Rest state) — hardcoded |
| Label zone height | 20px | Fixed |
| Hint zone height | 16px | Fixed |
| Calendar icon | 24×24px | Rest state only |
| faq icon | 16×16px | Inside Icon Button in label |
| Focus ring inset | −12px top/bottom, −48px right, −16px left | Absolute overlay; Focus state only |

### Open picker panel

The open picker panel is documented in [[Calendar.anatomy]]:

| Panel element | Width |
|--------------|-------|
| Full range calendar | 788px |
| Predefined ranges panel | 148px (hidden when `hidePredefinedRanges`) |
| Each month column | 280px |
| Day cell | 40×40px |
