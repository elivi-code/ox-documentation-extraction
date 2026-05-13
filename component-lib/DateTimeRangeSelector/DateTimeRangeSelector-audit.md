---
component: DateTimeRangeSelector
package: "@8x8/oxygen-date-time-range-selector"
rubric_version: "1.0"
audit_date: "2026-05-12"
auditor: doc-audit skill

files_found:
  - props.md
  - examples.md
  - tokens.md
  - accessibility.md
  - DateTimeRangeSelector-figma.md
  - DateTimeRangeSelector-usage.md

files_missing:
  - DateTimeRangeSelector-pui.md  # absent but intentional — PUI MCP search confirmed zero results

scores:
  props:         0.85   # 8.5/10 — 32 main props fully documented; DateTimeRangePicker sub-table missing Type/Default
  examples:      0.55   # 5.5/10 — 1 semi-canonical story pattern + 9 inferred snippets
  tokens:        0.35   # 3.5/10 — MCP returned no tokens; tokens.md visual states stale vs Bridge-confirmed figma.md data
  accessibility: 0.70   # 7/10 — comprehensive structure; all ARIA roles inferred; 3 WCAG items "Verify"
  figma:         0.85   # 8.5/10 — all 5 Light-mode states confirmed via Bridge; dark mode + annotations missing
  usage:         0.75   # 7.5/10 — 8 editorial Do/Don't pairs (re-authored 2026-05-12 via usage-advisor skill); all grounded in extracted artifacts; no Figma-native Do/Don't cards
  pui:           1.00   # N/A resolved — PUI MCP search confirmed no concerns

verdict: "YES"
verdict_reason: "Zero CONFLICTs and zero blocker-severity gaps. All 6 expected files present. GAP-003 resolved editorially 2026-05-12 — DateTimeRangeSelector-usage.md now contains 8 Do/Don't pairs grounded in the extracted artifacts, modelled on Calendar-usage.md. Remaining gaps are 2 majors (GAP-001 examples, GAP-002 tokens) and 7 minors — all SOURCE_GAPs or DOC_GAPs. doc-rewrite can proceed on all dimensions."

gaps:
  - id: GAP-001
    dimension: examples
    severity: major
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: examples.md
      location: "Header comment, lines 29–33"
      finding: "Oxygen MCP returned 1 Storybook story for @8x8/oxygen-date-time-range-selector wrapped in <Doc> and <ComponentSection> documentation wrappers — not a clean canonical snippet. The core usage pattern is extracted from it. The remaining 9 snippets (hidePredefinedRanges, hideTime, small size, custom labels, locale, 90-day limit, error state, disabled, custom inputRenderer) are inferred from prop documentation, not from Storybook source."
    fix_action: "Extract clean canonical Storybook examples from @8x8/oxygen-date-time-range-selector source once available, or confirm with the component team that inferred usage patterns are correct."
    blocks: [storybook-generate]
    dependency: []

  - id: GAP-002
    dimension: tokens
    severity: major
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: tokens.md
      location: "Theme tokens section, lines 34–36"
      finding: "Oxygen MCP returned no theme tokens for @8x8/oxygen-date-time-range-selector. Token names in DateTimeRangeSelector-figma.md are sourced from Bridge-confirmed CSS design context for the shared trigger input; the calendar panel tokens live in @8x8/oxygen-calendar. The UI-Foundations library (iVY5nI8JAxM05Apnnvozzs) has not been queried to confirm semantic variable names."
    fix_action: "Resolve trigger token names by running figma_get_variables on the UI-Foundations library file (iVY5nI8JAxM05Apnnvozzs) filtering for token names in DateTimeRangeSelector-figma.md color table. Update tokens.md with confirmed names."
    blocks: [tokens.md, doc-rewrite/tokens-section]
    dependency: []

  - id: GAP-003
    dimension: usage
    severity: minor
    type: SOURCE_GAP
    status: resolved-editorial
    resolved_date: "2026-05-12"
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: DateTimeRangeSelector-usage.md
      location: "Frontmatter + Do/Don't section, lines 1–end"
      finding: "RESOLVED EDITORIALLY (2026-05-12). DateTimeRangeSelector-usage.md re-authored via the usage-advisor skill (open mode) using Calendar-usage.md as the structural template. Contains 8 grounded Do/Don't pairs covering: range-vs-single picker, predefined-ranges visibility, time-row visibility, Finish/Apply commit boundary, placeholder vs. pre-fill, validation (hasError + endTimeErrorMessage), isDisabled semantics, full localisation. All claims trace to specific props.md / examples.md / accessibility.md / DateTimeRangeSelector-figma.md line numbers. Original Figma gap note preserved as appendix. Still missing: a `↳ Date picker examples` page in Figma file 5YihJ5WuDvnvrlrRMC4sBp with ✅ Do / ❌ Don't card frames — until those exist, figma-extract-usage cannot produce canonical output and this editorial file remains the source of truth."
    fix_action: "Optional follow-up: use figma-draw to push the 8 editorial pairs into a new '↳ Date picker examples' page in Figma file 5YihJ5WuDvnvrlrRMC4sBp; then re-run figma-extract-usage and replace DateTimeRangeSelector-usage.md with its canonical output."
    blocks: []
    dependency: []

  - id: GAP-004
    dimension: props
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: props.md
      location: "DateTimeRangePicker props table, lines 99–124"
      finding: "The DateTimeRangePicker sub-component props table lists 21 props with only Prop and Description columns — no Type, Default, or Required columns. This is inconsistent with the DateTimeRangeSelector props table and limits rewrite quality for the named export."
    fix_action: "Add Type and Default columns to the DateTimeRangePicker props table, or confirm with the component team which props have defaults and which are always required when using DateTimeRangePicker standalone."
    blocks: []
    dependency: []

  - id: GAP-005
    dimension: tokens
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: true
    evidence:
      source_file: tokens.md
      location: "Known visual states table, lines 49–56"
      finding: "tokens.md still shows 'Surface change (token unconfirmed)' for Hover state and 'Disabled surface/text' without token names. DateTimeRangeSelector-figma.md (Bridge-confirmed) has all values: Hover bg = --interactive/hover06 (#ebeae1), Disabled bg = --interactive/disabled01 (#c8c8bd), Disabled text = --interactive/disabled04 (#8d8b7e), Filled text = --text/textcolor01 (#26252a)."
    fix_action: "Update the Known visual states table in tokens.md with Bridge-confirmed token values from DateTimeRangeSelector-figma.md color table (lines 156–167). Mark as 'CSS-derived, confirmed via Bridge'."
    blocks: []
    dependency: []

  - id: GAP-006
    dimension: accessibility
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: accessibility.md
      location: "ARIA roles table, lines 32–43; Note, lines 45–47"
      finding: "All ARIA roles are explicitly marked as 'inferred from component structure and common date range picker patterns — verify against rendered DOM'. No confirmation from Figma annotations or component source code."
    fix_action: "Verify actual ARIA roles by inspecting the rendered @8x8/oxygen-date-time-range-selector DOM or component source. Update accessibility.md with confirmed roles and remove the 'inferred' caveat."
    blocks: []
    dependency: []

  - id: GAP-007
    dimension: accessibility
    severity: minor
    type: DOC_GAP
    confidence: heuristic
    auto_fixable: false
    evidence:
      source_file: accessibility.md
      location: "WCAG checklist, lines 80–86"
      finding: "WCAG 1.4.1 Use of Color, 1.4.3 Contrast (minimum), and 2.4.7 Focus Visible are marked 'Verify' — cannot be confirmed without resolved token values and DOM inspection."
    fix_action: "After GAP-002 is resolved (token values confirmed from UI-Foundations), verify color contrast ratios and focus ring visibility. Update checklist status from 'Verify' to '✓ Supported' or flag as failing."
    blocks: []
    dependency: [GAP-002]

  - id: GAP-008
    dimension: figma
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: DateTimeRangeSelector-figma.md
      location: "Design decisions section, lines 249–253"
      finding: "No design intent annotations found. Component description is null and annotations array is empty. No verbatim designer notes captured for any design decision (e.g. why 320px fixed width, why calendar icon hides on non-Rest states, why label stays active color in disabled)."
    fix_action: "Designer should add annotation nodes to the Date picker Figma component explaining intent. No automation can fix this."
    blocks: []
    dependency: []

  - id: GAP-009
    dimension: figma
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: DateTimeRangeSelector-figma.md
      location: "Color & token bindings section — Dark mode note, line 169"
      finding: "Dark mode token values not extracted. CSS design context was captured for Light mode only (5 variants: Rest, Hover, Focus, Error, Disabled). 34 Dark mode variants exist across the component set."
    fix_action: "Run get_design_context on a Dark mode variant (e.g. 80239:8257 — Dark/Large/Rest) to capture dark mode token bindings. Update figma.md color table with Dark mode column."
    blocks: []
    dependency: []

warnings:
  - id: WARN-001
    dimension: examples
    confidence: heuristic
    finding: "examples.md lines 195–209 — the inputRenderer snippet uses ({ value, onClick }) destructuring. The actual InputRendererProps type is not confirmed from MCP; these destructured prop names are inferred from typical render-prop conventions, not from component source."
    advisory: "Validate the inputRenderer example against a running instance of @8x8/oxygen-date-time-range-selector before publishing."

  - id: WARN-002
    dimension: props
    confidence: heuristic
    finding: "props.md lists an iconLeft prop (line 76) not reflected in the Figma anatomy (DateTimeRangeSelector-figma.md). This may be an implementation-level prop not represented in the shared 'Date picker' Figma component set."
    advisory: "Verify whether iconLeft renders within the trigger input or is used in a different part of the component. Confirm it maps to a Figma element before including it in the spec."
# --- navigation ---
role: audit
pipeline_stage: spec_ready
pipeline_note: "Audit verdict YES — doc-rewrite can run; usage dimension re-audited 2026-05-12"
audit_verdict: "YES"
siblings:
  - "[[DateTimeRangeSelector/props]]"
  - "[[DateTimeRangeSelector/examples]]"
  - "[[DateTimeRangeSelector/tokens]]"
  - "[[DateTimeRangeSelector/accessibility]]"
  - "[[DateTimeRangeSelector/DateTimeRangeSelector-figma]]"
  - "[[DateTimeRangeSelector/DateTimeRangeSelector-usage]]"
tags:
  - oxygen
  - component/DateTimeRangeSelector
  - role/audit
  - stage/spec_ready
  - category/date_time

---

# DateTimeRangeSelector — Documentation Audit

> Rubric v1.0 · Audited 2026-05-12 (full re-audit; previous audit 2026-05-08)

## File inventory

| File | Status |
|------|--------|
| `props.md` | ✅ Present |
| `examples.md` | ✅ Present |
| `tokens.md` | ✅ Present |
| `accessibility.md` | ✅ Present |
| `DateTimeRangeSelector-figma.md` | ✅ Present |
| `DateTimeRangeSelector-usage.md` | ✅ Present (re-authored editorially 2026-05-12) |
| `DateTimeRangeSelector-pui.md` | ✅ Absent — intentional (PUI MCP search confirmed no concerns) |

---

## Verdict: YES ✓

**Reason:** Zero CONFLICTs and zero blocker-severity gaps. All 6 expected files present. GAP-003 resolved editorially 2026-05-12 — `DateTimeRangeSelector-usage.md` now contains 8 Do/Don't pairs grounded in the extracted artifacts, modelled on `Calendar-usage.md`. Remaining gaps are SOURCE_GAPs (token confirmation from UI-Foundations, canonical Storybook examples, Figma examples page) and minor DOC_GAPs. `doc-rewrite` can proceed on all dimensions.

---

## Dimension scores

| Dimension | Score | Coverage | Status |
|-----------|-------|----------|--------|
| Props | 0.85 | 8.5/10 | Good — 32 main props fully documented; DateTimeRangePicker sub-table missing Type/Default |
| Examples | 0.55 | 5.5/10 | Major — 1 semi-canonical story; 9 inferred snippets |
| Tokens | 0.35 | 3.5/10 | Major — MCP returned no tokens; tokens.md states table stale vs Bridge-confirmed figma.md |
| Accessibility | 0.70 | 7/10 | Solid structure — ARIA roles inferred; 3 WCAG items pending token resolution |
| Figma | 0.85 | 8.5/10 | Strong — all 5 Light-mode states confirmed via Bridge; dark mode + annotations missing |
| Usage | 0.75 | 7.5/10 | Good (editorial) — 8 Do/Don't pairs re-authored 2026-05-12; no Figma-native cards or screenshots |
| PUI | 1.00 | N/A | Pass — confirmed no PUI concerns |

---

## Gap summary

| ID | Dimension | Severity | Type | Auto-fixable | Status |
|----|-----------|----------|------|:------------:|--------|
| GAP-001 | Examples | major | SOURCE_GAP | No | Open |
| GAP-002 | Tokens | major | SOURCE_GAP | No | Open |
| GAP-003 | Usage | minor | SOURCE_GAP | No | Resolved-editorial 2026-05-12 |
| GAP-004 | Props | minor | DOC_GAP | No | Open |
| GAP-005 | Tokens | minor | DOC_GAP | Yes | Open |
| GAP-006 | Accessibility | minor | SOURCE_GAP | No | Open |
| GAP-007 | Accessibility | minor | DOC_GAP | No (blocked on GAP-002) | Open |
| GAP-008 | Figma | minor | SOURCE_GAP | No | Open |
| GAP-009 | Figma | minor | SOURCE_GAP | No | Open |

**Totals:** 0 blockers · 2 majors · 7 minors (1 resolved-editorial) · 0 conflicts · 2 warnings

---

## Recommended resolution order

1. **GAP-005** — auto-fixable: update tokens.md visual states table with Bridge-confirmed values from figma.md (doc-rewrite can handle)
2. **GAP-004** — add Type/Default columns to DateTimeRangePicker sub-table (doc-rewrite with component team input)
3. **GAP-002** — confirm token names from UI-Foundations library (upstream work)
4. **GAP-001** — confirm examples with component team
5. **GAP-003 (resolved-editorial 2026-05-12)** — optional: use figma-draw to push the 8 editorial pairs into a `↳ Date picker examples` page in Figma file 5YihJ5WuDvnvrlrRMC4sBp; then re-run figma-extract-usage to produce canonical output
6. Remaining minor gaps (GAP-006, GAP-007, GAP-008, GAP-009) — address post-rewrite

---

_Source: doc-audit skill v1.0 · DateTimeRangeSelector · 2026-05-12_
