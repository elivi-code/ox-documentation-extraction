---
component: DateTimeSelector
package: "@8x8/oxygen-date-time-selector"
rubric_version: "1.0"
audit_date: "2026-05-13"
auditor: doc-audit skill

files_found:
  - props.md
  - examples.md
  - tokens.md
  - accessibility.md
  - DateTimeSelector-figma.md
  - DateTimeSelector-usage.md

files_missing:
  - DateTimeSelector-pui.md  # absent but intentional — PUI MCP search confirmed zero results

scores:
  props:         0.75   # 7.5/10 — all props present; defaults all missing; 6 descriptions inferred not sourced
  examples:      0.50   # 5/10 — 7 inferred snippets; 0 canonical Storybook examples from MCP
  tokens:        0.30   # 3/10 — MCP returned no tokens; tokens.md does not cross-reference CSS-derived names in figma.md
  accessibility: 0.70   # 7/10 — comprehensive structure; all ARIA roles inferred; 3 WCAG items "Verify"
  figma:         0.70   # 7/10 — anatomy + API fully confirmed via Bridge; Hover/Disabled tokens missing; CONFLICT present
  usage:         0.85   # 8.5/10 — 6 grounded editorial pairs present (usage-advisor, 2026-05-13); no Figma Do/Don't page; no component instance screenshots; replace with figma-extract-usage when Figma cards exist
  pui:           1.00   # N/A resolved — PUI MCP search confirmed no concerns

verdict: "YES"
verdict_reason: "GAP-004 CONFLICT resolved (2026-05-08) — Option B confirmed: shared trigger with DateTimeRangeSelector. No remaining CONFLICTs. No blocker-severity gaps. Usage re-audited 2026-05-13 — editorial guidance now present (6 pairs). Remaining gaps are major/minor SOURCE_GAPs and DOC_GAPs that doc-rewrite can handle or annotate."

gaps:
  - id: GAP-001
    dimension: examples
    severity: major
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: examples.md
      location: "Header comment, line 5"
      finding: "Oxygen MCP returned 0 canonical Storybook examples for @8x8/oxygen-date-time-selector. All 7 code snippets are inferred from prop descriptions, not confirmed against actual component behaviour."
    fix_action: "Extract canonical Storybook examples from @8x8/oxygen-date-time-selector source once available, or confirm with the component team that these inferred usage patterns are correct."
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
      location: "Theme tokens section, line 11"
      finding: "Oxygen MCP returned no theme tokens for @8x8/oxygen-date-time-selector. Token names in DateTimeSelector-figma.md are sourced from generated CSS (get_design_context), not confirmed from the UI-Foundations variables panel (iVY5nI8JAxM05Apnnvozzs)."
    fix_action: "Resolve token names by running figma_get_variables on the UI-Foundations library file (iVY5nI8JAxM05Apnnvozzs) filtering for token names found in DateTimeSelector-figma.md color table. Update tokens.md with confirmed names."
    blocks: [tokens.md, doc-rewrite/tokens-section]
    dependency: []

  - id: GAP-003
    dimension: usage
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: DateTimeSelector-usage.md
      location: "File header comments, lines 1–8"
      finding: "No '↳ Date picker examples' Figma page exists in the UI-components file (5YihJ5WuDvnvrlrRMC4sBp). Usage file now contains 6 editorial Do/Don't pairs (usage-advisor, 2026-05-13) grounded in props.md, examples.md, accessibility.md, and DateTimeSelector-figma.md. Editorial source — not extracted from Figma Do/Don't card frames. No component instance screenshots present."
    fix_action: "Editorial content is available. Severity downgraded to minor. Re-run figma-extract-usage and replace DateTimeSelector-usage.md once '↳ Date picker examples' cards are added to Figma file 5YihJ5WuDvnvrlrRMC4sBp."
    blocks: []
    dependency: []

  - id: GAP-004
    dimension: figma
    severity: major
    type: CONFLICT
    confidence: deterministic
    auto_fixable: false
    resolved: true
    resolution: "Option B confirmed — shared trigger. DateTimeRangeSelector extraction (2026-05-08) used the same Figma node (80239:8235) and the range-format default text confirms this component set is the shared trigger for both DateTimeSelector and DateTimeRangeSelector. DateTimeSelector reuses it with value:Date (single). See DateTimeRangeSelector-figma.md."
    evidence:
      source_file: DateTimeSelector-figma.md
      location: "Design decisions section, line 209; Gaps & conflicts section, line 237"
      finding: "The Figma COMPONENT_SET is named 'Date picker' (node 80239:8235) while the OX package is @8x8/oxygen-date-time-selector. The Figma default Text property value ('22/08/2022 12:00 AM - 23/08/2022 11:59 PM') shows a date-time range format, suggesting this trigger UI may be shared with @8x8/oxygen-date-time-range-selector. Scope of this Figma component is ambiguous: single-date selector only, or shared trigger for both packages?"
    fix_action: "RESOLVED: Option B — shared trigger confirmed. Update DateTimeSelector-figma.md to note the shared design. No API change needed."
    blocks: [doc-rewrite, examples.md, doc-rewrite/scope-section]
    dependency: []

  - id: GAP-005
    dimension: props
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: true
    evidence:
      source_file: props.md
      location: "Props table, Default column, lines 21–30"
      finding: "All 10 props show '—' for the Default value. The OX MCP did not return default values. Likely defaults for booleans: closeOnDateChange=false, isClearable=false, isLoading=false."
    fix_action: "Look up default values in @8x8/oxygen-date-time-selector TypeScript source (or Storybook controls) and populate the Default column. At minimum confirm booleans default to false."
    blocks: []
    dependency: []

  - id: GAP-006
    dimension: props
    severity: minor
    type: DOC_GAP
    confidence: heuristic
    auto_fixable: false
    evidence:
      source_file: props.md
      location: "Props table, Description column, lines 21, 22, 29, 30"
      finding: "OX MCP returned empty string descriptions for closeOnDateChange, finishButtonLabel, titleFormatPattern, value, and loadingMessage. Descriptions in props.md are inferred from prop names and types, not sourced from component documentation."
    fix_action: "Verify inferred descriptions against @8x8/oxygen-date-time-selector source JSDoc or Storybook argTypes. Update any that are incorrect or incomplete."
    blocks: []
    dependency: []

  - id: GAP-007
    dimension: tokens
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: true
    evidence:
      source_file: tokens.md
      location: "Theme tokens section, lines 11–16"
      finding: "tokens.md does not include the CSS-derived token names already documented in DateTimeSelector-figma.md (--ui/ui05, --text/textcolor01, --text/textcolor02, --error/error01, --interactive/focus01, typography tokens). The two files are not cross-referenced."
    fix_action: "Add a 'Tokens from Figma (CSS-derived)' table to tokens.md by pulling the confirmed entries from DateTimeSelector-figma.md color table. Mark as 'CSS-derived, pending UI-Foundations confirmation'."
    blocks: []
    dependency: [GAP-002]

  - id: GAP-008
    dimension: figma
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: DateTimeSelector-figma.md
      location: "Color & token bindings table, line 119; Gaps & conflicts section, line 234"
      finding: "Hover and Disabled state token values are marked '— (verify)' in the color table. Design context was only captured for Rest, Focus, and Error states. Hover background token and Disabled surface/text tokens are not confirmed."
    fix_action: "Run get_design_context on hover variant (e.g. 80239:8243 — Light/Large/Hover/False/False) and disabled variant (80239:8376 — Light/Large/Disabled/False/True) to confirm token values. Update figma.md color table."
    blocks: [tokens.md]
    dependency: []

  - id: GAP-009
    dimension: figma
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: DateTimeSelector-figma.md
      location: "Design decisions section, line 207"
      finding: "No design intent annotations found. Component description is null and annotations array is empty. No verbatim designer notes captured for any design decision."
    fix_action: "Designer should add annotation nodes to the Date picker Figma component explaining intent (e.g. why 320px fixed width, why form label uses _base_form_label shared instance, why calendar icon is hidden in error state). No automation can fix this."
    blocks: []
    dependency: []

  - id: GAP-010
    dimension: accessibility
    severity: minor
    type: SOURCE_GAP
    confidence: heuristic
    auto_fixable: false
    evidence:
      source_file: accessibility.md
      location: "ARIA roles table, line 8; Note, line 16"
      finding: "All ARIA roles are explicitly marked as 'inferred from component structure and common date picker patterns — verify against rendered DOM'. No confirmation from Figma annotations or component source code."
    fix_action: "Verify actual ARIA roles by inspecting the rendered @8x8/oxygen-date-time-selector DOM or component source. Update accessibility.md with confirmed roles."
    blocks: []
    dependency: []

  - id: GAP-011
    dimension: accessibility
    severity: minor
    type: DOC_GAP
    confidence: heuristic
    auto_fixable: false
    evidence:
      source_file: accessibility.md
      location: "WCAG checklist, lines 49, 50, 53"
      finding: "WCAG 1.4.1 Use of Color, 1.4.3 Contrast (minimum), and 2.4.7 Focus Visible are marked 'Verify' — cannot be confirmed without resolved token values and DOM inspection."
    fix_action: "After GAP-002 is resolved (token values confirmed), verify color contrast ratios and focus ring visibility. Update checklist status from 'Verify' to '✓ Supported' or flag as failing."
    blocks: []
    dependency: [GAP-002]

warnings:
  - id: WARN-001
    dimension: examples
    confidence: heuristic
    finding: "All 7 code snippets in examples.md are inferred from prop names and types. Props like closeOnDateChange, finishButtonLabel, and titleFormatPattern have empty MCP descriptions — inferred behavior may not match actual implementation semantics."
    advisory: "Validate all examples against a running instance of @8x8/oxygen-date-time-selector before publishing."

  - id: WARN-002
    dimension: figma
    confidence: heuristic
    finding: "Dark mode variants (Mode=Dark) exist across all 68 component variants. Dark mode token values were not extracted — CSS design context was only captured for Light mode variants. Dark mode coverage in figma.md is limited to noting the variants exist."
    advisory: "Run get_design_context on a Dark mode variant (e.g. 80239:8257 — Dark/Large/Rest) to capture dark mode token bindings before publishing the figma spec."
# --- navigation (added by component-map) ---
role: audit
pipeline_stage: spec_ready
pipeline_note: "Audit verdict YES — doc-rewrite can run"
audit_verdict: "YES"
siblings:
  - "[[DateTimeSelector/props]]"
  - "[[DateTimeSelector/examples]]"
  - "[[DateTimeSelector/tokens]]"
  - "[[DateTimeSelector/accessibility]]"
  - "[[DateTimeSelector/DateTimeSelector-figma]]"
  - "[[DateTimeSelector/DateTimeSelector-usage]]"
tags:
  - oxygen
  - component/DateTimeSelector
  - role/audit
  - stage/spec_ready
  - category/date_time

---

# DateTimeSelector — Documentation Audit

> Rubric v1.0 · Audited 2026-05-13 *(re-audit — usage updated from stub to editorial draft)*

## File inventory

| File | Status |
|------|--------|
| `props.md` | ✅ Present |
| `examples.md` | ✅ Present |
| `tokens.md` | ✅ Present |
| `accessibility.md` | ✅ Present |
| `DateTimeSelector-figma.md` | ✅ Present |
| `DateTimeSelector-usage.md` | ✅ Present — 6 editorial Do/Don't pairs (usage-advisor, 2026-05-13) |
| `DateTimeSelector-pui.md` | ✅ Absent — intentional (PUI MCP search confirmed no concerns) |

---

## Verdict: YES ✓

**Reason:** No CONFLICTs, no blocker gaps. GAP-004 CONFLICT resolved 2026-05-08 (Option B — shared trigger confirmed). Usage re-audited 2026-05-13: 6 editorial pairs now present, GAP-003 downgraded to minor. `doc-rewrite` can proceed.

---

## Dimension scores

| Dimension | Score | Coverage | Status |
|-----------|-------|----------|--------|
| Props | 0.75 | 7.5/10 | Minor gaps — all defaults missing; 6 descriptions inferred |
| Examples | 0.50 | 5/10 | Major — 0 canonical Storybook examples; all 7 snippets inferred |
| Tokens | 0.30 | 3/10 | Major — MCP returned no tokens; figma.md has CSS-derived names but tokens.md doesn't include them |
| Accessibility | 0.70 | 7/10 | Solid structure — ARIA roles inferred; 3 WCAG items pending token/DOM verification |
| Figma | 0.70 | 7/10 | Anatomy + API confirmed via Bridge; Hover/Disabled tokens missing; CONFLICT resolved |
| Usage | 0.85 | 8.5/10 | 6 editorial pairs, grounded — no Figma card instances; replace with figma-extract-usage when Figma page exists |
| PUI | 1.00 | N/A | Pass — confirmed no PUI concerns |

---

## Gap summary

| ID | Dimension | Severity | Type | Auto-fixable |
|----|-----------|----------|------|:------------:|
| GAP-001 | Examples | major | SOURCE_GAP | No |
| GAP-002 | Tokens | major | SOURCE_GAP | No |
| GAP-003 | Usage | ~~major~~ minor | SOURCE_GAP | No — editorial content present; Figma page still absent |
| GAP-004 | Figma | major | ~~CONFLICT~~ RESOLVED | Option B — shared trigger confirmed |
| GAP-005 | Props | minor | DOC_GAP | Yes |
| GAP-006 | Props | minor | DOC_GAP | No |
| GAP-007 | Tokens | minor | DOC_GAP | Yes (after GAP-002) |
| GAP-008 | Figma | minor | SOURCE_GAP | No |
| GAP-009 | Figma | minor | SOURCE_GAP | No |
| GAP-010 | Accessibility | minor | SOURCE_GAP | No |
| GAP-011 | Accessibility | minor | DOC_GAP | No (blocked on GAP-002) |

**Totals:** 0 blockers · 2 majors · 9 minors · 0 conflicts · 2 warnings

---

## Recommended resolution order

1. **GAP-005** — auto-fixable defaults in props.md (doc-rewrite can handle)
2. **GAP-007** — merge CSS-derived token names from figma.md into tokens.md (doc-rewrite can handle after GAP-002)
3. **GAP-002 + GAP-008** — confirm token names from UI-Foundations library + capture Hover/Disabled states
4. **GAP-001** — confirm examples with component team
5. **GAP-003** — create Figma Do/Don't page when design team is ready; editorial pairs available in the meantime
6. Remaining minor gaps (GAP-006, GAP-009, GAP-010, GAP-011) — address post-rewrite

---

_Source: doc-audit skill v1.0 · DateTimeSelector · re-audit 2026-05-13 (original audit 2026-05-08)_
