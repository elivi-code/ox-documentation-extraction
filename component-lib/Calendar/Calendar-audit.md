---
component: Calendar
package: "@8x8/oxygen-calendar"
rubric_version: "1.0"
audit_date: "2026-05-08"
auditor: doc-audit skill

files_found:
  - props.md
  - examples.md
  - tokens.md
  - accessibility.md
  - Calendar-figma.md
  - Calendar-usage.md

files_missing:
  - Calendar-pui.md  # absent but intentional — PUI MCP search confirmed zero results

scores:
  props:         0.85   # 17/20 checks — minor type definition gaps
  examples:      0.65   # 7/10 — no canonical Storybook examples; snippets inferred from prop docs
  tokens:        0.35   # 3/9 — MCP returned no component tokens; Figma tokens from CSS only
  accessibility: 0.80   # 8/10 — comprehensive but some "verify" items pending token resolution
  figma:         0.80   # 8/10 — anatomy/variants confirmed; tokens from CSS not variables panel
  usage:         0.20   # 2/10 — examples page exists but no Do/Don't editorial cards
  pui:           1.00   # N/A resolved — search confirmed no PUI concerns

verdict: "NO"
verdict_reason: "One CONFLICT (GAP-011) requires human decision before doc-rewrite can proceed."

gaps:
  - id: GAP-001
    dimension: examples
    severity: major
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: examples.md
      location: "Footer note, line 118"
      finding: "Oxygen MCP returned 0 clean Storybook examples for the calendar package. All 8 code snippets are derived from prop descriptions, not canonical Storybook stories."
    fix_action: "Extract canonical Storybook examples from @8x8/oxygen-calendar source once available, or confirm with the component team that the documentation story is the only example."
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
      location: "Theme tokens section, line 7"
      finding: "Oxygen MCP returned no theme tokens for @8x8/oxygen-calendar. Token names in Calendar-figma.md are sourced from generated CSS (get_design_context), not confirmed from the UI-Foundations variables panel (iVY5nI8JAxM05Apnnvozzs)."
    fix_action: "Resolve token names by running figma_get_variables on the UI-Foundations library file (iVY5nI8JAxM05Apnnvozzs) and cross-referencing with CSS variable names found in Calendar-figma.md."
    blocks: [tokens.md, doc-rewrite/tokens-section]
    dependency: []

  - id: GAP-003
    dimension: usage
    severity: major
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: Calendar-usage.md
      location: "Gaps section, line 68"
      finding: "The '↳ Calendar examples' Figma page (node 69971:10137) contains no ✅ Do / ❌ Don't frames. The page has usage illustration sections only (Date picker examples, Intraday, Breakpoints, Popovers, 90 days limit) — no editorial Do/Don't guidance."
    fix_action: "Designer must create Do/Don't cards using the figma-draw template on the '↳ Calendar examples' page. Re-run figma-extract-usage after cards are added."
    blocks: [Calendar-usage.md, usage-guidelines-section]
    dependency: []

  - id: GAP-004
    dimension: props
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: true
    evidence:
      source_file: props.md
      location: "Calendar props table, line 34"
      finding: "The `range` prop uses type `DateRange` but the shape of DateRange (startDate, endDate fields) is not defined anywhere in props.md."
    fix_action: "Add a TypeScript interface block for DateRange ({ startDate?: Date; endDate?: Date }) to props.md, sourced from the package types."
    blocks: []
    dependency: []

  - id: GAP-005
    dimension: props
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: true
    evidence:
      source_file: props.md
      location: "Calendar props table, line 46"
      finding: "The `dateOptions` prop uses type `DateOptions` but the shape is only partially described (weekStartsOn, customEvenMonths). Full interface not documented."
    fix_action: "Add a TypeScript interface block for DateOptions ({ weekStartsOn?: 0|1|2|3|4|5|6; customEvenMonths?: boolean }) to props.md."
    blocks: []
    dependency: []

  - id: GAP-006
    dimension: props
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: true
    evidence:
      source_file: props.md
      location: "Calendar props table, line 55"
      finding: "`enableMaxWidth` prop has no default value documented (shown as `—`)."
    fix_action: "Look up the default for enableMaxWidth in the @8x8/oxygen-calendar source and add to the Default column."
    blocks: []
    dependency: []

  - id: GAP-007
    dimension: tokens
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: Calendar-figma.md
      location: "Token coverage section, lines 119-131"
      finding: "Token names (--ui/ui06, --actions/action01, etc.) extracted from Figma's generated CSS output, not confirmed from the UI-Foundations variables panel. Token-to-semantic-name mapping may be incomplete."
    fix_action: "Run figma_get_variables on UI-Foundations library file (iVY5nI8JAxM05Apnnvozzs) filtering for token names found in Calendar-figma.md color table to confirm names and resolve aliases."
    blocks: [tokens.md]
    dependency: [GAP-002]

  - id: GAP-008
    dimension: figma
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: Calendar-figma.md
      location: "Design decisions & annotations section, line 239"
      finding: "No Figma design intent annotations found. The '<!-- NO ANNOTATIONS FOUND IN FIGMA RESPONSE -->' marker is present — no verbatim designer notes captured."
    fix_action: "Designer should add annotation nodes to the Calendar Figma page explaining design decisions (e.g. why 280px column width, why 40px day cell, why 148px panel). No automation can fix this."
    blocks: []
    dependency: []

  - id: GAP-009
    dimension: accessibility
    severity: minor
    type: SOURCE_GAP
    confidence: heuristic
    auto_fixable: false
    evidence:
      source_file: accessibility.md
      location: "ARIA roles table, line 9"
      finding: "ARIA role for Calendar root is documented as 'role=\"application\" or role=\"group\" (implementation-defined)' — exact role not confirmed from Figma annotations or component source code."
    fix_action: "Verify the actual ARIA role used on the Calendar root element by inspecting rendered DOM or the @8x8/oxygen-calendar source. Update accessibility.md with the confirmed role."
    blocks: []
    dependency: []

  - id: GAP-010
    dimension: accessibility
    severity: minor
    type: DOC_GAP
    confidence: heuristic
    auto_fixable: false
    evidence:
      source_file: accessibility.md
      location: "WCAG checklist, lines 54 and 57"
      finding: "WCAG 1.4.3 Contrast (minimum) and 2.4.7 Focus Visible are marked 'Verify' — cannot be confirmed without resolved token values mapping to actual hex colors."
    fix_action: "After GAP-002/GAP-007 are resolved (token values confirmed), check --text/textcolor01 on --ui/ui06 background and --interactive/focus01 ring width against WCAG AA ratios. Update checklist status."
    blocks: []
    dependency: [GAP-002, GAP-007]

  - id: GAP-011
    dimension: figma
    severity: major
    type: CONFLICT
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: Calendar-figma.md
      location: "Boolean toggles table, line 102; Gaps & conflicts section, line 267"
      finding: "Figma component set has a boolean property '90 days' (key: 90 days#85539:0, default: false) that enables a 90-day range limit mode. The @8x8/oxygen-calendar API has no corresponding dedicated prop — the feature is implemented via disabledDates + disabledDateTooltip. Human decision needed: should the spec document this as a usage pattern (recommended disabledDates approach) or flag it as a missing API surface?"
    fix_action: "Human: decide whether to (A) document 90-day limit as a recommended usage pattern using disabledDates/disabledDateTooltip in examples.md, or (B) raise an issue with the component team to add a dedicated prop. Mark decision here before doc-rewrite runs."
    blocks: [doc-rewrite, examples.md]
    dependency: []

warnings:
  - id: WARN-001
    dimension: accessibility
    confidence: heuristic
    finding: "Keyboard behavior (Page Up/Down, Home/End) is documented based on the ARIA Date Picker APG pattern, not confirmed against the actual @8x8/oxygen-calendar implementation. The accessibility.md note says 'Verify against the actual implementation'."
    advisory: "Spot-check keyboard navigation in the rendered component before publishing accessibility docs."

  - id: WARN-002
    dimension: figma
    confidence: heuristic
    finding: "Dark mode is not present in the Figma component set (only 'light' variant exists). Calendar-figma.md notes that dark mode is 'likely handled via CSS tokens at runtime.' This is unconfirmed."
    advisory: "Confirm with the design team whether a dark mode Figma variant is planned or intentionally omitted."
---

# Calendar — Documentation Audit

> Rubric v1.0 · Audited 2026-05-08

## File inventory

| File | Status |
|------|--------|
| `props.md` | ✅ Present |
| `examples.md` | ✅ Present |
| `tokens.md` | ✅ Present |
| `accessibility.md` | ✅ Present |
| `Calendar-figma.md` | ✅ Present |
| `Calendar-usage.md` | ✅ Present |
| `Calendar-pui.md` | ✅ Absent — intentional (PUI search confirmed no concerns) |

---

## Verdict: NO

**Reason:** One CONFLICT (GAP-011) requires a human decision before `doc-rewrite` can proceed. The `90 days` Figma design property has no direct API equivalent — the resolution strategy must be confirmed.

**After resolving GAP-011**, the remaining gaps are all SOURCE_GAPs or minor DOC_GAPs. The rewrite can proceed to a `PARTIAL` spec covering props, examples, accessibility, and figma dimensions fully, with tokens and usage noted as incomplete.

---

## Dimension scores

| Dimension | Score | Coverage | Status |
|-----------|-------|----------|--------|
| Props | 0.85 | 17/20 | Minor gaps — type shapes for `DateRange`, `DateOptions`; `enableMaxWidth` default missing |
| Examples | 0.65 | 7/10 | Major — no canonical Storybook examples; snippets inferred from prop docs |
| Tokens | 0.35 | 3/9 | Major — MCP returned no tokens; Figma tokens from generated CSS only |
| Accessibility | 0.80 | 8/10 | Solid — some "Verify" items blocked on token resolution |
| Figma | 0.80 | 8/10 | Good anatomy + variants; token names unconfirmed; no annotations |
| Usage | 0.20 | 2/10 | Major — examples page has no Do/Don't cards |
| PUI | 1.00 | N/A | Pass — confirmed no PUI concerns |

---

## Gap summary

| ID | Dimension | Severity | Type | Auto-fixable |
|----|-----------|----------|------|:------------:|
| GAP-001 | Examples | major | SOURCE_GAP | No |
| GAP-002 | Tokens | major | SOURCE_GAP | No |
| GAP-003 | Usage | major | SOURCE_GAP | No |
| GAP-004 | Props | minor | DOC_GAP | Yes |
| GAP-005 | Props | minor | DOC_GAP | Yes |
| GAP-006 | Props | minor | DOC_GAP | Yes |
| GAP-007 | Tokens | minor | SOURCE_GAP | No |
| GAP-008 | Figma | minor | SOURCE_GAP | No |
| GAP-009 | Accessibility | minor | SOURCE_GAP | No |
| GAP-010 | Accessibility | minor | DOC_GAP | No (blocked on GAP-002) |
| GAP-011 | Figma | major | **CONFLICT** | **No — human decision required** |

**Totals:** 0 blockers · 4 majors · 6 minors · 1 conflict · 2 warnings

---

## GAP-011 — CONFLICT requiring human decision

> **90 days Figma boolean vs. API design**

The Figma component set includes a boolean property `90 days` (default: `false`) that enables a 90-day range limit mode — dates outside the 90-day window are disabled and show a tooltip on hover/focus.

The `@8x8/oxygen-calendar` API has **no dedicated prop** for this. The feature is achieved via:
- `disabledDates: Date[]` — pass dates outside the allowed 90-day window
- `disabledDateTooltip: (day: Date) => string | undefined` — return tooltip text for out-of-range dates

**Decision required (choose one):**

| Option | Action |
|--------|--------|
| A — Document as usage pattern | Add a "90-day limit" example to `examples.md` using `disabledDates` + `disabledDateTooltip`. No API change needed. |
| B — Raise API gap | File an issue with the component team to add a `maxRangeDays` or similar prop. Hold doc-rewrite until resolved. |

---

## Recommended resolution order

1. **GAP-011** — resolve the CONFLICT (human decision, ~5 min)
2. **GAP-004, GAP-005, GAP-006** — auto-fixable DOC_GAPs in props.md (doc-rewrite can handle)
3. **GAP-002 + GAP-007** — resolve token names from UI-Foundations library (run figma_get_variables on `iVY5nI8JAxM05Apnnvozzs`)
4. **GAP-001** — confirm Storybook examples with component team
5. **GAP-003** — request Do/Don't cards from design team
6. Remaining minor gaps (GAP-008, GAP-009, GAP-010) — address post-rewrite if desired

---

_Source: doc-audit skill v1.0 · Calendar · 2026-05-08_
