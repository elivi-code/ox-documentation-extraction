---
component: DateTimeRangeSelector
package: "@8x8/oxygen-date-time-range-selector"
rubric_version: "1.0"
audit_date: "2026-05-08"
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
  examples:      0.55   # 5.5/10 — 1 semi-canonical story pattern + 8 inferred snippets
  tokens:        0.35   # 3.5/10 — MCP returned no tokens; tokens.md visual states stale vs confirmed figma.md Bridge data
  accessibility: 0.70   # 7/10 — comprehensive structure; all ARIA roles inferred; 3 WCAG items "Verify"
  figma:         0.85   # 8.5/10 — all 5 states fully confirmed via Bridge; dark mode + annotations missing
  usage:         0.10   # 1/10 — file exists but contains only a gap note; no Figma examples page
  pui:           1.00   # N/A resolved — PUI MCP search confirmed no concerns

verdict: "YES"
verdict_reason: "Zero CONFLICTs and zero blocker-severity gaps. All 6 expected files present. Remaining gaps are major/minor SOURCE_GAPs and DOC_GAPs that doc-rewrite can handle or annotate."

gaps:
  - id: GAP-001
    dimension: examples
    severity: major
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: examples.md
      location: "Header comment, lines 5–8"
      finding: "Oxygen MCP returned 1 Storybook story for @8x8/oxygen-date-time-range-selector, but it is wrapped in <Doc> and <ComponentSection> — a documentation wrapper, not a clean canonical snippet. The core usage pattern was extracted from the story. The remaining 8 snippets are inferred from prop documentation."
    fix_action: "Extract clean canonical Storybook examples from @8x8/oxygen-date-time-range-selector source once available, or confirm with the component team that these inferred usage patterns are correct."
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
      location: "Theme tokens section, lines 11–12"
      finding: "Oxygen MCP returned no theme tokens for @8x8/oxygen-date-time-range-selector. Token names in DateTimeRangeSelector-figma.md are sourced from Bridge-confirmed CSS design context for the shared trigger input; the calendar panel tokens live in @8x8/oxygen-calendar."
    fix_action: "Resolve trigger token names by running figma_get_variables on the UI-Foundations library file (iVY5nI8JAxM05Apnnvozzs) filtering for token names in DateTimeRangeSelector-figma.md color table. Update tokens.md with confirmed names."
    blocks: [tokens.md, doc-rewrite/tokens-section]
    dependency: []

  - id: GAP-003
    dimension: usage
    severity: major
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: DateTimeRangeSelector-usage.md
      location: "Status section, line 13"
      finding: "No '↳ Date picker examples' or '↳ DateTimeRangeSelector examples' page exists in the UI-components Figma file (5YihJ5WuDvnvrlrRMC4sBp). Page listing confirmed this absence. No Do/Don't editorial guidance has been created for this component."
    fix_action: "Designer must create a '↳ Date picker examples' page using the figma-draw template with ✅ Do / ❌ Don't cards. Re-run figma-extract-usage after cards are added."
    blocks: [DateTimeRangeSelector-usage.md, usage-guidelines-section]
    dependency: []

  - id: GAP-004
    dimension: props
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: props.md
      location: "DateTimeRangePicker props table, lines 73–91"
      finding: "The DateTimeRangePicker sub-component props table lists 21 props with only Prop, Type, and Description columns — no Default or Required columns. This makes it inconsistent with the DateTimeRangeSelector props table and limits rewrite quality."
    fix_action: "Add Type and Default columns to the DateTimeRangePicker props table. At minimum confirm which props have defaults vs are always required when using DateTimeRangePicker standalone."
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
      location: "Known visual states table, lines 24–32"
      finding: "tokens.md visual states table still shows 'Surface change (token unconfirmed)' for Hover and 'Disabled surface/text' without token names. DateTimeRangeSelector-figma.md (Bridge-confirmed) has all values: Hover bg = --interactive/hover06 (#ebeae1), Disabled bg = --interactive/disabled01 (#c8c8bd), Disabled text = --interactive/disabled04 (#8d8b7e), Filled text = --text/textcolor01 (#26252a)."
    fix_action: "Update the Known visual states table in tokens.md with Bridge-confirmed token values from DateTimeRangeSelector-figma.md color table. Mark as 'CSS-derived, confirmed via Bridge'."
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
      location: "ARIA roles table, line 9; Note, line 21"
      finding: "All ARIA roles are explicitly marked as 'inferred from component structure and common date range picker patterns — verify against rendered DOM'. No confirmation from Figma annotations or component source code."
    fix_action: "Verify actual ARIA roles by inspecting the rendered @8x8/oxygen-date-time-range-selector DOM or component source. Update accessibility.md with confirmed roles."
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
      location: "WCAG checklist, lines 57, 58, 61"
      finding: "WCAG 1.4.1 Use of Color, 1.4.3 Contrast (minimum), and 2.4.7 Focus Visible are marked 'Verify' — cannot be confirmed without resolved token values and DOM inspection."
    fix_action: "After GAP-002 is resolved (token values confirmed), verify color contrast ratios and focus ring visibility. Update checklist status from 'Verify' to '✓ Supported' or flag as failing."
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
      location: "Design decisions section"
      finding: "No design intent annotations found. Component description is null and annotations array is empty. No verbatim designer notes captured for any design decision."
    fix_action: "Designer should add annotation nodes to the Date picker Figma component explaining intent (e.g. why 320px fixed width, why calendar icon hides on non-rest states, why label stays active color in disabled). No automation can fix this."
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
      location: "Gaps & conflicts section — 'Dark mode' row"
      finding: "Dark mode token values not extracted. CSS design context was captured for Light mode only (5 variants: Rest, Hover, Focus, Error, Disabled). 34 Dark mode variants exist across the component set."
    fix_action: "Run get_design_context on a Dark mode variant (e.g. 80239:8257 — Dark/Large/Rest) to capture dark mode token bindings. Update figma.md color table with Dark mode column."
    blocks: []
    dependency: []

warnings:
  - id: WARN-001
    dimension: examples
    confidence: heuristic
    finding: "examples.md line 174 — the inputRenderer snippet uses ({ value, onClick }) destructuring. The actual InputRendererProps type is not confirmed from MCP; these destructured prop names are inferred from typical render-prop conventions, not from component source."
    advisory: "Validate the inputRenderer example against a running instance of @8x8/oxygen-date-time-range-selector before publishing."

  - id: WARN-002
    dimension: props
    confidence: heuristic
    finding: "props.md lists an iconLeft prop (line 44) not reflected in the Figma anatomy (DateTimeRangeSelector-figma.md). This may be an implementation-level prop not represented in the shared 'Date picker' Figma component set."
    advisory: "Verify whether iconLeft renders within the trigger input or is used in a different part of the component. Confirm it maps to a Figma element before including it in the spec."
---

# DateTimeRangeSelector — Documentation Audit

> Rubric v1.0 · Audited 2026-05-08

## File inventory

| File | Status |
|------|--------|
| `props.md` | ✅ Present |
| `examples.md` | ✅ Present |
| `tokens.md` | ✅ Present |
| `accessibility.md` | ✅ Present |
| `DateTimeRangeSelector-figma.md` | ✅ Present |
| `DateTimeRangeSelector-usage.md` | ✅ Present |
| `DateTimeRangeSelector-pui.md` | ✅ Absent — intentional (PUI MCP search confirmed no concerns) |

---

## Verdict: YES ✓

**Reason:** Zero CONFLICTs and zero blocker-severity gaps. All 6 expected files present. `doc-rewrite` can proceed on all dimensions. Remaining gaps are SOURCE_GAPs (token confirmation from UI-Foundations, usage page from designer, canonical Storybook examples) and minor DOC_GAPs that `doc-rewrite` can handle or annotate.

---

## Dimension scores

| Dimension | Score | Coverage | Status |
|-----------|-------|----------|--------|
| Props | 0.85 | 8.5/10 | Good — 32 main props fully documented; DateTimeRangePicker sub-table missing Type/Default |
| Examples | 0.55 | 5.5/10 | Major — 1 semi-canonical story pattern; 8 inferred snippets |
| Tokens | 0.35 | 3.5/10 | Major — MCP no tokens; tokens.md states table stale vs Bridge-confirmed figma.md |
| Accessibility | 0.70 | 7/10 | Solid structure — ARIA roles inferred; 3 WCAG items pending |
| Figma | 0.85 | 8.5/10 | Strong — all 5 states fully confirmed via Bridge; dark mode + annotations missing |
| Usage | 0.10 | 1/10 | Major — no Figma examples page; usage file is gap-only |
| PUI | 1.00 | N/A | Pass — confirmed no PUI concerns |

---

## Gap summary

| ID | Dimension | Severity | Type | Auto-fixable |
|----|-----------|----------|------|:------------:|
| GAP-001 | Examples | major | SOURCE_GAP | No |
| GAP-002 | Tokens | major | SOURCE_GAP | No |
| GAP-003 | Usage | major | SOURCE_GAP | No |
| GAP-004 | Props | minor | DOC_GAP | No |
| GAP-005 | Tokens | minor | DOC_GAP | Yes |
| GAP-006 | Accessibility | minor | SOURCE_GAP | No |
| GAP-007 | Accessibility | minor | DOC_GAP | No (blocked on GAP-002) |
| GAP-008 | Figma | minor | SOURCE_GAP | No |
| GAP-009 | Figma | minor | SOURCE_GAP | No |

**Totals:** 0 blockers · 3 majors · 6 minors · 0 conflicts · 2 warnings

---

## Recommended resolution order

1. **GAP-005** — auto-fixable: update tokens.md visual states table with Bridge-confirmed values from figma.md (doc-rewrite can handle)
2. **GAP-004** — add Type/Default columns to DateTimeRangePicker sub-table (doc-rewrite with component team input)
3. **GAP-002** — confirm token names from UI-Foundations library (upstream work)
4. **GAP-001** — confirm examples with component team
5. **GAP-003** — request Do/Don't cards from design team
6. Remaining minor gaps (GAP-006, GAP-007, GAP-008, GAP-009) — address post-rewrite

---

_Source: doc-audit skill v1.0 · DateTimeRangeSelector · 2026-05-08_
