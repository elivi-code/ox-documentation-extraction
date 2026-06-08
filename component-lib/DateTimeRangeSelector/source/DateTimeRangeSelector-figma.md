---
component: DateTimeRangeSelector
package: "@8x8/oxygen-date-time-range-selector"
category: date_time
role: figma
role_description: "Design system specs — anatomy, variants, spacing from Figma"
pipeline_stage: spec_ready
pipeline_note: "Audit verdict YES/PARTIAL — doc-rewrite can run"
audit_verdict: "YES"
siblings:
  - "[[DateTimeRangeSelector/props]]"
  - "[[DateTimeRangeSelector/examples]]"
  - "[[DateTimeRangeSelector/tokens]]"
  - "[[DateTimeRangeSelector/accessibility]]"
  - "[[DateTimeRangeSelector/DateTimeRangeSelector-usage]]"
  - "[[DateTimeRangeSelector/DateTimeRangeSelector-audit]]"
tags:
  - oxygen
  - component/DateTimeRangeSelector
  - role/figma
  - stage/spec_ready
  - category/date_time
---

<!-- SOURCE: Figma Desktop Bridge plugin (figma-console MCP) + Figma REST MCP -->
<!-- FILE KEY: 5YihJ5WuDvnvrlrRMC4sBp -->
<!-- NODE ID: 80239:8235 -->
<!-- EXTRACTED: 2026-05-08 -->
<!-- COMPONENT: DateTimeRangeSelector -->
<!-- COLOR STRATEGY: B (5 states × 2 modes × filled/unfilled — states as columns, elements as rows) -->
<!-- BRIDGE: All token values confirmed via get_design_context on 5 variant nodes (Rest/Hover/Focus/Error/Disabled) -->
<!-- NOTE: This Figma node (80239:8235, "Date picker") is SHARED with DateTimeSelector.
     The same trigger input component is used by both packages. The Figma default Text value
     ("22/08/2022 12:00 AM - 23/08/2022 11:59 PM") is a date-time range — confirming this
     component set primarily represents the DateTimeRangeSelector trigger.
     This resolves GAP-004 in DateTimeSelector-audit.md as Option B (shared trigger). -->

# DateTimeRangeSelector — Figma Design Spec

> **See also:** [props.md](./props.md) · [tokens.md](./tokens.md) ·
> [examples.md](./examples.md) · [accessibility.md](./accessibility.md)

---

## Visual reference

![DateTimeRangeSelector](./figma-screenshot-datetimerangeselector.png)

**Component set overview:** 68 variants at 2176×1416px. Left half = Light mode; right half = Dark mode.
The filled-state default text (`"22/08/2022 12:00 AM - 23/08/2022 11:59 PM"`) represents a date-time
range value — confirming this is the primary design for `DateTimeRangeSelector`.

> **Shared design note:** Node `80239:8235` ("Date picker") in file `5YihJ5WuDvnvrlrRMC4sBp` is the
> shared trigger input used by both `@8x8/oxygen-date-time-selector` and
> `@8x8/oxygen-date-time-range-selector`. The full anatomy and token bindings apply to both.
> For the open picker panel (calendar + predefined ranges + time selectors), see
> [Calendar — Figma Design Spec](../../Calendar/Calendar-figma.md).

---

## Anatomy

Base variant: `Mode=Light, Size=Large, State=Rest, Error=False, Filled=False` (node 80239:8236, 320×92px)

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
| 3 | instance | `calendar` | content | 24×24px calendar icon; visible in **Rest only** — hidden in Hover, Focus, Error, Disabled |
| 4 | frame | `Focus ring` | optional slot | Absolute, `border-2 border-[--interactive/focus01]`; visible in Focus state only |
| 5 | frame | `Error Area` | optional slot | Below dropdown when Error=True; error message text |

---

## API — Component properties

### Variant axes

Confirmed from `componentPropertyDefinitions` on COMPONENT_SET node `80239:8235` via Desktop Bridge:

| Property | Figma key | Type | Values | Default |
|----------|-----------|------|--------|---------|
| `Mode` | `Mode` | VARIANT | `Light`, `Dark` | `Light` |
| `Size` | `Size` | VARIANT | `Large`, `Medium`, `Small` | `Large` |
| `State` | `State` | VARIANT | `Rest`, `Hover`, `Focus`, `Disabled` | `Rest` |
| `Error` | `Error` | VARIANT | `False`, `True` | `False` |
| `Filled` | `Filled` | VARIANT | `False`, `True` | `False` |

### Boolean toggles

| Property | Figma key | Default | Notes |
|----------|-----------|---------|-------|
| `Show Label` | `Show Label#19887:0` | `true` | Shows/hides `_base_form_label` |
| `Show Hint` | `Show Hint#19869:10` | `true` | Shows/hides `_base_form_hint` |

### Text content properties

| Property | Figma key | Default | Notes |
|----------|-----------|---------|-------|
| `Placeholder` | `Placeholder#19734:4` | `"Select date"` | Unfilled state |
| `Text` | `Text#19735:0` | `"22/08/2022 12:00 AM - 23/08/2022 11:59 PM"` | Filled state — range format confirms DateTimeRangeSelector primary use |
| `Error text` | `Error text#19714:27` | `"Error message goes here."` | Error=True state |

### Instance swap slots

<!-- NO INSTANCE SWAP SLOTS FOUND in returned data -->

### Persistent states

| State | Axis | API prop | Notes |
|-------|------|----------|-------|
| Error | `Error=True` | `hasError` | Red 2px border + Error Area; calendar icon hidden |
| Disabled | `State=Disabled` | `isDisabled` | `--interactive/disabled01` bg; `--interactive/disabled04` text; not interactive |
| Filled | `Filled=True` | `dateTimeRange` set | Shows selected range text in `--text/textcolor01` |

### Token coverage

- **Coverage:** Partial — colour and typography tokenised; spacing hardcoded
- **Hardcoded values flagged:**
  - `Dropdown.width`: `320px` — no token
  - `Dropdown.border-radius`: `6px` — no token
  - `Container.gap`: `4px` — no token
  - `Text.gap` (icon spacing): `8px` — no token
  - `Error border.width`: `2px` — no token
  - `Focus ring border.width`: `2px` — no token
  - `Icon Button.border-radius`: `6px` — no token
  - `Icon Button.padding`: `2px` — no token

---

## Color & token bindings

<!-- COLOR STRATEGY B: states as columns, elements as rows -->
<!-- All values confirmed via get_design_context on: 80239:8236 (Rest), 80239:8243 (Hover), -->
<!-- 80239:8478 (Focus), 80239:8610 (Error), 80239:8376 (Disabled) — Figma Desktop Bridge -->

| Element | Rest | Hover | Focus | Disabled | Error |
|---------|------|-------|-------|----------|-------|
| Dropdown background | `--ui/ui05` (#f4f3ee) | `--interactive/hover06` (#ebeae1) | `--ui/ui05` (#f4f3ee) | `--interactive/disabled01` (#c8c8bd) | `--ui/ui05` (#f4f3ee) |
| Dropdown border | none | none | none | none | `--error/error01` (#cb2233) 2px solid |
| Focus ring | — | — | `--interactive/focus01` (#0056e0) 2px | — | — |
| Placeholder text | `--text/textcolor02` (#6c6862) | `--text/textcolor02` (#6c6862) | `--text/textcolor02` (#6c6862) | — | `--text/textcolor02` (#6c6862) |
| Filled range text | `--text/textcolor01` (#26252a) | — | — | `--interactive/disabled04` (#8d8b7e) | — |
| Calendar icon | visible (24×24) | hidden | hidden | hidden | hidden |
| Label text | `--text/textcolor01` (#26252a) | `--text/textcolor01` (#26252a) | `--text/textcolor01` (#26252a) | `--text/textcolor01` (#26252a) | `--text/textcolor01` (#26252a) |
| Required `*` | `--error/error01` (#cb2233) | `--error/error01` (#cb2233) | `--error/error01` (#cb2233) | `--error/error01` (#cb2233) | `--error/error01` (#cb2233) |
| Hint text | `--text/textcolor02` (#6c6862) | `--text/textcolor02` (#6c6862) | `--text/textcolor02` (#6c6862) | `--text/textcolor02` (#6c6862) | — |
| Error message text | — | — | — | — | `--error/error01` (#cb2233) |

> Dark mode token values were not extracted — CSS design context was captured for Light mode only.
> Dark mode variants (Mode=Dark) exist across all 68 variants; run `get_design_context` on a
> Dark variant (e.g. 80239:8257 — Dark/Large/Rest) for dark mode token coverage.

### Text styles

| Element | Token | Size | Weight | Line height | Letter spacing |
|---------|-------|------|--------|-------------|---------------|
| Label | `body01` | 14px | 400 | 20px | −0.06px |
| Required asterisk | `bodybold01` | 14px | 600 | 20px | −0.06px |
| Placeholder / range value | `body02` | 16px | 400 | 24px | +0.0121px |
| Hint text | `label01` | 12px | 400 | 16px | 0px |
| Error text | `label01` | 12px | 400 | 16px | 0px |

### Effect styles

<!-- NO EFFECT STYLES FOUND IN FIGMA RESPONSE -->

---

## Structure & spacing

### Container (trigger input)

| Property | Token | Value | Variant |
|----------|-------|-------|---------|
| Width | — | 320px | all sizes |
| Height | — | 92px | Large (label + dropdown + hint + gaps) |
| Height | — | 84px | Medium |
| Height | — | 76px | Small |
| Gap (zones) | — | 4px | all |
| Flex direction | — | column | all |

### Dropdown (trigger) dimensions

| Property | Token | Value | Size |
|----------|-------|-------|------|
| Height | — | 48px | Large |
| Height | — | 40px | Medium |
| Height | — | 32px | Small |
| Padding horizontal | — | 16px | all |
| Padding vertical | — | 12px | Large |
| Border radius | — | 6px | all |

### Internal spacing

| Property | Token | Value | Notes |
|----------|-------|-------|-------|
| Text/icon gap | — | 8px | Between range text and calendar icon (Rest state) |
| Label zone height | — | 20px | Fixed |
| Hint zone height | — | 16px | Fixed |
| Calendar icon size | — | 24×24px | Right side of dropdown; Rest state only |
| faq icon size | — | 16×16px | Inside Icon Button in label |
| Focus ring inset | — | −12px top/bottom, −48px right, −16px left | Absolute overlay; Focus state only |

### Open picker panel dimensions

The open picker panel (Calendar + predefined ranges + time selectors) is documented in
[Calendar — Figma Design Spec](../../Calendar/Calendar-figma.md):

| Panel element | Width | Notes |
|--------------|-------|-------|
| Full range calendar | 788px | Dual-month grid |
| Predefined ranges panel | 148px | Left side; hidden when `hidePredefinedRanges` |
| Each month column | 280px | |
| Day cell | 40×40px | |

---

## Interaction states

| State | Trigger | Visual change | Token(s) confirmed |
|-------|---------|---------------|--------------------|
| hover | pointer over Dropdown | `--interactive/hover06` (#ebeae1) bg; calendar icon hidden | ✓ Bridge |
| focus | keyboard Tab | `border-2` focus ring `--interactive/focus01` (#0056e0); `inset-[-12px_-48px_-12px_-16px]`; calendar icon hidden | ✓ Bridge |
| error | `hasError=true` | Red 2px border `--error/error01`; calendar icon hidden; Error Area below | ✓ Bridge |
| disabled | `isDisabled=true` | `--interactive/disabled01` (#c8c8bd) bg; filled text `--interactive/disabled04` (#8d8b7e); calendar icon hidden | ✓ Bridge |
| filled | `dateTimeRange` set | Placeholder replaced by formatted range string; `--text/textcolor01` (#26252a) text | ✓ Bridge |

---

## Design decisions & annotations

<!-- NO ANNOTATIONS FOUND IN FIGMA RESPONSE — component description is null -->

> **Shared trigger confirmation:** The Figma `Text` property default (`"22/08/2022 12:00 AM - 23/08/2022 11:59 PM"`) is a date-time range, confirming that node `80239:8235` is the primary design representation of the `DateTimeRangeSelector` trigger. `DateTimeSelector` reuses the same input component with `value: Date` (single date). This resolves the CONFLICT previously noted in `DateTimeSelector-audit.md` GAP-004 as **Option B — shared trigger**.

---

## Accessibility (from Figma annotations only)

- **ARIA role:** <!-- NOT ANNOTATED IN FIGMA -->
- **Focus order:** <!-- NOT ANNOTATED IN FIGMA -->
- **Keyboard interactions:** Focus ring defined — `border-2 border-[--interactive/focus01] rounded-[6px]` absolute overlay positioned `inset-[-12px_-48px_-12px_-16px]`.

See [accessibility.md](./accessibility.md) for full accessibility documentation.

---

## Gaps & conflicts

| Type | Description |
|------|-------------|
| Shared design | Node 80239:8235 is used by both `DateTimeSelector` and `DateTimeRangeSelector` — no separate Figma component for the range trigger |
| Missing tokens | `Dropdown.width` (320px), `border-radius` (6px), `Container.gap` (4px), `Text.gap` (8px), `Error.border-width` (2px), `Focus.border-width` (2px), `Icon Button.border-radius` (6px), `Icon Button.padding` (2px) — all hardcoded |
| Missing annotation | No design intent annotations in Figma — component description is null |
| Token source | Variables empty in UI-components file — tokens are in UI-Foundations library (`iVY5nI8JAxM05Apnnvozzs`) |
| Dark mode | Dark mode token values not captured — only Light mode states extracted via Bridge |
| Missing usage page | No `↳ Date picker examples` or `↳ DateTimeRangeSelector examples` page in Figma file |
| Open picker panel | Full calendar/predefined-ranges/time panel design is in Calendar node (80239:7420), not in this component set |

---

_Source: Figma Desktop Bridge plugin (figma-console MCP) · Figma REST MCP · Extracted 2026-05-08_
