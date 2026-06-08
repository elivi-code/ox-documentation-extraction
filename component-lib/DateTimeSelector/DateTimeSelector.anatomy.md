---
parent: "[[DateTimeSelector]]"
section: anatomy
---

## Variants

The component set (Figma node `80239:8235`, file `5YihJ5WuDvnvrlrRMC4sBp`) contains **68 variants** across 5 axes:

| Axis | Values | Default |
|------|--------|---------|
| Mode | `Light`, `Dark` | `Light` |
| Size | `Large`, `Medium`, `Small` | `Large` |
| State | `Rest`, `Hover`, `Focus`, `Disabled` | `Rest` |
| Error | `False`, `True` | `False` |
| Filled | `False`, `True` | `False` |

## Anatomy

Base variant: `Mode=Light, Size=Large, State=Rest, Error=False, Filled=False` (node `80239:8236`, 320×92px)

| # | Type | Name | Role | Notes |
|---|------|------|------|-------|
| 1 | instance | `_base_form_label` | optional slot | Visible when `Show Label=true` (default). 320×20px. Contains label text + required asterisk + faq icon button |
| 2 | frame | `Dropdown` | fixed sub-component | Always present. 320×48px (Large). The date picker trigger / input field |
| 3 | instance | `_base_form_hint` | optional slot | Visible when `Show Hint=true` (default). 320×16px. Shows hint or error text below the field |

**Container layout:** `flex-col`, `gap-[4px]` between zones, `w-[320px]`

### Sub-component: _base_form_label

| # | Type | Name | Role | Notes |
|---|------|------|------|-------|
| 1 | frame | `H Stack` | structural | Horizontal flex; label text + required asterisk `*` |
| 2 | text | `Label` | content | Text token `body01`; color `--text/textcolor01` |
| 3 | text | `Required` | content | `*` character; color `--error/error01`; token `bodybold01` |
| 4 | instance | `Icon Button` | content | 20×20px; faq/help icon (16×16); padding 2px; `rounded-[6px]` |

### Sub-component: Dropdown (trigger frame)

| # | Type | Name | Role | Notes |
|---|------|------|------|-------|
| 1 | frame | `Text` | structural | Horizontal flex, `gap-[8px]`, fills remaining width |
| 2 | text/div | `Text` (inner) | content | Placeholder or filled date-range value; `body02` token |
| 3 | instance | `calendar` | content | 24×24px calendar icon; hidden in Error=True state |
| 4 | frame | `Focus ring` | optional slot | Absolute, `border-2 border-[--interactive/focus01]`; visible in Focus state only |
| 5 | frame | `Error Area` | optional slot | Below dropdown in Error=True state; error message text |

## States

| State | Trigger | Visual change |
|-------|---------|---------------|
| Rest | Default | Standard surface and border |
| Hover | Pointer over Dropdown | Background change |
| Focus | Keyboard Tab | 2px ring in `--interactive/focus01`; absolute overlay extending slightly beyond dropdown |
| Disabled | `State=Disabled` | Greyed appearance; not interactive |
| Error | `Error=True` | Red 2px border on Dropdown; calendar icon hidden; Error Area appears below |
| Filled | `Filled=True` | Placeholder replaced with selected date-time value |

<!-- STUB:GAP-008 source="Run get_design_context on hover variant (80239:8243 — Light/Large/Hover/False/False) and disabled variant (80239:8376 — Light/Large/Disabled/False/True) to confirm token values for those states. Update color table in source/DateTimeSelector-figma.md." -->

<!-- STUB:GAP-009 source="Designer should add annotation nodes to the Date picker Figma component explaining design intent (e.g. why 320px fixed width, why shared trigger with DateTimeRangeSelector, why calendar icon hidden in Error state)." -->

## Component properties

### Boolean toggles

| Property | Figma key | Default | Notes |
|----------|-----------|---------|-------|
| `Show Label` | `Show Label#19887:0` | `true` | Shows/hides the `_base_form_label` zone |
| `Show Hint` | `Show Hint#19869:10` | `true` | Shows/hides the `_base_form_hint` zone |

### Text content properties

| Property | Figma key | Default |
|----------|-----------|---------|
| `Placeholder` | `Placeholder#19734:4` | `"Select date"` |
| `Text` | `Text#19735:0` | `"22/08/2022 12:00 AM - 23/08/2022 11:59 PM"` |
| `Error text` | `Error text#19714:27` | `"Error message goes here."` |

> **Naming note:** The Figma COMPONENT_SET is named `"Date picker"` (node `80239:8235`) while the OX package is `@8x8/oxygen-date-time-selector`. GAP-004 resolved (2026-05-08): this trigger component set is shared with `@8x8/oxygen-date-time-range-selector` — `DateTimeSelector` uses `value: Date` (single); `DateTimeRangeSelector` uses the same trigger with range semantics. See [[DateTimeRangeSelector]].

## Spacing & dimensions

### Container

| Property | Value | Notes |
|----------|-------|-------|
| Width | 320px | All sizes; hardcoded |
| Height | 92px / 84px / 76px | Large / Medium / Small |
| Gap (zones) | 4px | Between label / dropdown / hint; hardcoded |
| Flex direction | column | All sizes |

### Dropdown (trigger)

| Property | Value | Size |
|----------|-------|------|
| Height | 48px | Large |
| Height | 40px | Medium |
| Height | 32px | Small |
| Padding horizontal | 16px | All |
| Padding vertical | 12px | Large |
| Border radius | 6px | All; hardcoded |

### Internal spacing

| Element | Value |
|---------|-------|
| Text / calendar icon gap | 8px |
| Label zone height | 20px |
| Hint zone height | 16px |
| Icon Button size | 20×20px |
| Calendar icon size | 24×24px |
| faq icon size | 16×16px |
