---
parent: "[[DateTimeRangeSelector]]"
section: tokens
component: DateTimeRangeSelector
pipeline_stage: spec_ready
audit_verdict: "YES"
tags:
  - oxygen
  - component/DateTimeRangeSelector
  - role/spoke
  - section/tokens
  - stage/spec_ready
  - category/date_time
---

<!-- STUB:GAP-002 source="Resolve trigger token names by running figma_get_variables on the UI-Foundations library file (iVY5nI8JAxM05Apnnvozzs) filtering for token names in DateTimeRangeSelector-figma.md color table. Update with confirmed semantic variable names." -->
<!-- STUB:GAP-009 source="Run get_design_context on a Dark mode variant (e.g. 80239:8257 — Dark/Large/Rest) to capture dark mode token bindings. Add a Dark mode column to the color table." -->

## Token sources

No tokens returned by `mcp__oxygen-mcp__get-theme-tokens` for `@8x8/oxygen-date-time-range-selector`. The component is composed of two tokenised sub-systems:

| Sub-system | Token source |
|------------|-------------|
| Trigger input | Shared "Date picker" Figma design — CSS-derived values confirmed via Bridge (Light mode) |
| Calendar + time picker panel | `@8x8/oxygen-calendar` — see [[Calendar.tokens]] |

> Token names below come from Figma's generated CSS (Light mode), **not** from the UI-Foundations variables panel. Semantic variable name confirmation is pending (GAP-002). Dark mode bindings are unextracted (GAP-009).

---

## Color tokens — trigger input (Light mode, Bridge-confirmed)

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

---

## Visual states summary (trigger input)

| State | Token roles |
|-------|-------------|
| Rest | `--ui/ui05` (#f4f3ee) bg; `--text/textcolor02` (#6c6862) placeholder |
| Hover | `--interactive/hover06` (#ebeae1) bg; calendar icon hidden (CSS-derived, confirmed via Bridge) |
| Focus | `--interactive/focus01` (#0056e0) 2 px focus ring; calendar icon hidden |
| Error (`hasError=true`) | `--error/error01` (#cb2233) 2 px border + error area; calendar icon hidden |
| Disabled (`isDisabled=true`) | `--interactive/disabled01` (#c8c8bd) bg; `--interactive/disabled04` (#8d8b7e) filled text; calendar icon hidden (CSS-derived, confirmed via Bridge) |
| Filled | `--text/textcolor01` (#26252a) value text |

---

## Typography tokens

| Element | Token | Size | Weight | Line height | Letter spacing |
|---------|-------|------|--------|-------------|---------------|
| Label | `body01` | 14px | 400 | 20px | −0.06px |
| Required asterisk | `bodybold01` | 14px | 600 | 20px | −0.06px |
| Placeholder / range value | `body02` | 16px | 400 | 24px | +0.0121px |
| Hint text | `label01` | 12px | 400 | 16px | 0px |
| Error text | `label01` | 12px | 400 | 16px | 0px |

---

## Hardcoded values (no token)

| Property | Value | Notes |
|----------|-------|-------|
| Dropdown width | 320px | All sizes |
| Dropdown border-radius | 6px | All sizes |
| Container gap | 4px | Between zones |
| Text/icon gap | 8px | Between range text and calendar icon |
| Error border width | 2px | |
| Focus ring border width | 2px | |
| Icon Button border-radius | 6px | |
| Icon Button padding | 2px | |
