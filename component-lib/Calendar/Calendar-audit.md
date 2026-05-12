---
component: Calendar
package: "@8x8/oxygen-calendar"
rubric_version: "1.0"
audit_date: "2026-05-12"
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
  props:         0.85   # 17/20 — type shape gaps for DateRange/DateOptions; enableMaxWidth default missing
  examples:      0.65   # 7/10 — no canonical Storybook examples; snippets derived from prop docs
  tokens:        0.35   # 3/9 — MCP returned no component tokens; Figma tokens from generated CSS only
  accessibility: 0.80   # 8/10 — comprehensive; two "Verify" items blocked on token resolution
  figma:         0.80   # 8/10 — anatomy/variants confirmed; token names unconfirmed; no annotations
  usage:         0.80   # 8/10 — 7 Do/Don't pairs, editorial source (published docs page); no Figma-native Do/Don't cards or screenshots
  pui:           1.00   # N/A resolved — search confirmed no PUI concerns

verdict: "YES"
verdict_reason: "Zero CONFLICTs and zero blocker-severity gaps. GAP-011 (CONFLICT) resolved 2026-05-12 — Option A chosen and documented in Calendar-usage.md Pair 3 (disabledDates + disabledDateTooltip pattern). GAP-003 resolved 2026-05-12 — Calendar-usage.md now contains 7 editorial Do/Don't pairs sourced from the published Oxygen docs page. Remaining gaps are 2 majors (GAP-001 examples, GAP-002 tokens) and 7 minors — all SOURCE_GAPs or DOC_GAPs, none blocking doc-rewrite."

gaps:
  - id: GAP-001
    dimension: examples
    severity: major
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: examples.md
      location: "Footer note, line 142"
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
    status: RESOLVED
    resolved_date: "2026-05-12"
    resolution: "Calendar-usage.md replaced with a 477-line editorial doc containing 7 Do/Don't pairs, sourced from the published Oxygen docs page (https://oxygen.8x8.com/components/calendar/usage, fetched 2026-05-12) and cross-referenced with extracted MCP/Figma artifacts. Source type is editorial (not Figma Do/Don't card frames). Re-open if the Figma '↳ Calendar examples' page (node 69971:10137) gains Do/Don't cards and figma-extract-usage is re-run."
    evidence:
      source_file: Calendar-usage.md
      location: "Frontmatter, line 9 (source_type: editorial)"
      finding: "The '↳ Calendar examples' Figma page (node 69971:10137) still contains no ✅ Do / ❌ Don't frames. The editorial usage doc substitutes published Oxygen docs page guidance — 7 pairs with full cross-references."
    fix_action: "Designer must create Do/Don't cards using the figma-draw template on the '↳ Calendar examples' page. Re-run figma-extract-usage after cards are added; replace editorial pairs."
    blocks: []
    dependency: []

  - id: GAP-004
    dimension: props
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: true
    evidence:
      source_file: props.md
      location: "Calendar props table, line 66"
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
      location: "Calendar props table, line 78"
      finding: "The `dateOptions` prop uses type `DateOptions` but the shape is only partially described. Full interface not documented."
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
      location: "Calendar props table, line 87"
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
      location: "Design decisions & annotations section, line 261"
      finding: "No Figma design intent annotations found — no verbatim designer notes captured."
    fix_action: "Designer should add annotation nodes to the Calendar Figma page explaining design decisions (e.g. why 280px column width, why 40px day cell, why 148px panel)."
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
      location: "ARIA roles table, line 33"
      finding: "ARIA role for Calendar root documented as 'role=\"application\" or role=\"group\" (implementation-defined)' — exact role not confirmed from source."
    fix_action: "Verify the actual ARIA role by inspecting rendered DOM or @8x8/oxygen-calendar source. Update accessibility.md."
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
      location: "WCAG checklist, lines 78 and 81"
      finding: "WCAG 1.4.3 Contrast (minimum) and 2.4.7 Focus Visible marked 'Verify' — cannot be confirmed without resolved token values."
    fix_action: "After GAP-002/GAP-007 resolved, verify --text/textcolor01 on --ui/ui06 background and --interactive/focus01 ring against WCAG AA ratios."
    blocks: []
    dependency: [GAP-002, GAP-007]

  - id: GAP-011
    dimension: figma
    severity: major
    type: CONFLICT
    confidence: deterministic
    auto_fixable: false
    status: RESOLVED
    resolved_date: "2026-05-12"
    resolution: "Option A chosen — 90-day limit documented as a disabledDates + disabledDateTooltip usage pattern. See Calendar-usage.md Pair 3 (lines ~145-190). If the component team adds a dedicated maxRangeDays prop in a future release, Pair 3 should be updated to prefer that."
    evidence:
      source_file: Calendar-figma.md
      location: "Boolean toggles table, line 126; Gaps & conflicts section, line 291"
      finding: "Figma boolean '90 days' (key: 90 days#85539:0) enables a 90-day range limit mode with no dedicated API prop equivalent. Decision: document as usage pattern rather than raise API gap."
    fix_action: "Resolved — Option A documented. Reopen if @8x8/oxygen-calendar gains a maxRangeDays prop."
    blocks: []
    dependency: []

warnings:
  - id: WARN-001
    dimension: accessibility
    confidence: heuristic
    finding: "Keyboard behavior (Page Up/Down, Home/End) documented from the ARIA Date Picker APG pattern, not confirmed against the actual @8x8/oxygen-calendar implementation."
    advisory: "Spot-check keyboard navigation in the rendered component before publishing accessibility docs."

  - id: WARN-002
    dimension: figma
    confidence: heuristic
    finding: "Dark mode not present in the Figma component set (only 'light' variant). Calendar-figma.md notes dark mode is 'likely handled via CSS tokens at runtime' — unconfirmed."
    advisory: "Confirm with the design team whether a dark mode Figma variant is planned or intentionally omitted."

  - id: WARN-003
    dimension: usage
    confidence: heuristic
    finding: "Calendar-usage.md was authored editorially from the published Oxygen docs page (source_type: editorial), not extracted from Figma Do/Don't card frames. The Figma '↳ Calendar examples' page (node 69971:10137) still has no Do/Don't cards. Usage doc note '🔖 GAP-011 (CONFLICT, open)' in Pair 3 is stale — the CONFLICT was resolved on 2026-05-12."
    advisory: "Update the '(CONFLICT, open)' note in Calendar-usage.md Pair 3 to '(CONFLICT, resolved 2026-05-12 — Option A)'. Add Do/Don't Figma cards when design capacity allows."
# --- navigation ---
role: audit
pipeline_stage: spec_ready
pipeline_note: "Audit verdict YES — doc-rewrite can run. Usage dimension is editorial (not Figma-native Do/Don't cards). Tokens dimension has major gaps — spec will note token names are from CSS, not confirmed from UI-Foundations panel."
audit_verdict: "YES"
siblings:
  - "[[Calendar/props]]"
  - "[[Calendar/examples]]"
  - "[[Calendar/tokens]]"
  - "[[Calendar/accessibility]]"
  - "[[Calendar/Calendar-figma]]"
  - "[[Calendar/Calendar-usage]]"
tags:
  - oxygen
  - component/Calendar
  - role/audit
  - stage/spec_ready
  - category/date_time

---

# Calendar — Documentation Audit

> Rubric v1.0 · Audited 2026-05-12 · Previous audit: 2026-05-08

## File inventory

| File | Status |
|------|--------|
| `props.md` | ✅ Present |
| `examples.md` | ✅ Present |
| `tokens.md` | ✅ Present |
| `accessibility.md` | ✅ Present |
| `Calendar-figma.md` | ✅ Present |
| `Calendar-usage.md` | ✅ Present — re-authored 2026-05-12 (editorial) |
| `Calendar-pui.md` | ✅ Absent — intentional (PUI search confirmed no concerns) |

---

## Verdict: YES

**Reason:** Zero CONFLICTs and zero blocker-severity gaps.

Two gaps resolved since the 2026-05-08 audit:
- **GAP-003 RESOLVED** — `Calendar-usage.md` replaced with a 477-line editorial doc containing 7 Do/Don't pairs, sourced from the published Oxygen docs page and cross-referenced with extracted MCP/Figma artifacts.
- **GAP-011 RESOLVED** — Option A chosen (2026-05-12): 90-day range limit documented as a `disabledDates` + `disabledDateTooltip` usage pattern in Calendar-usage.md Pair 3.

**Caveats for doc-rewrite:**
- Usage dimension is editorial (not Figma-native Do/Don't cards) — spec should carry `source_type: editorial` on the usage section.
- Tokens dimension has major gaps (GAP-002/007) — token names sourced from Figma CSS only. Spec should note this caveat rather than assert token names as canonical.
- One stale note in `Calendar-usage.md` Pair 3 reads "(CONFLICT, open)" — this should be updated to "(CONFLICT, resolved 2026-05-12 — Option A)" — see WARN-003.

---

## Dimension scores

| Dimension | Score | Coverage | Change | Status |
|-----------|-------|----------|--------|--------|
| Props | 0.85 | 17/20 | — | Minor gaps — type shapes for `DateRange`, `DateOptions`; `enableMaxWidth` default missing |
| Examples | 0.65 | 7/10 | — | Major — no canonical Storybook examples |
| Tokens | 0.35 | 3/9 | — | Major — MCP returned no tokens; Figma tokens from generated CSS only |
| Accessibility | 0.80 | 8/10 | — | Solid — two "Verify" items blocked on token resolution |
| Figma | 0.80 | 8/10 | — | Good anatomy + variants; token names unconfirmed; no annotations |
| Usage | **0.80** | **8/10** | **↑ from 0.20** | 7 Do/Don't pairs (editorial); no Figma-native cards or screenshots |
| PUI | 1.00 | N/A | — | Pass — confirmed no PUI concerns |

---

## Gap summary

| ID | Dimension | Severity | Type | Status | Auto-fixable |
|----|-----------|----------|------|--------|:------------:|
| GAP-001 | Examples | major | SOURCE_GAP | Open | No |
| GAP-002 | Tokens | major | SOURCE_GAP | Open | No |
| GAP-003 | Usage | major | SOURCE_GAP | **RESOLVED 2026-05-12** | — |
| GAP-004 | Props | minor | DOC_GAP | Open | Yes |
| GAP-005 | Props | minor | DOC_GAP | Open | Yes |
| GAP-006 | Props | minor | DOC_GAP | Open | Yes |
| GAP-007 | Tokens | minor | SOURCE_GAP | Open | No |
| GAP-008 | Figma | minor | SOURCE_GAP | Open | No |
| GAP-009 | Accessibility | minor | SOURCE_GAP | Open | No |
| GAP-010 | Accessibility | minor | DOC_GAP | Open | No (blocked on GAP-002) |
| GAP-011 | Figma | major | CONFLICT | **RESOLVED 2026-05-12** | — |

**Totals (open):** 0 blockers · 2 majors · 7 minors · 0 conflicts · 3 warnings

---

## GAP-011 — RESOLVED

> **90 days Figma boolean vs. API design — Option A chosen**

The Figma boolean `90 days` (default: `false`) enables a 90-day range limit mode. The `@8x8/oxygen-calendar` API has no dedicated prop for this.

**Decision made 2026-05-12: Option A** — Document as usage pattern.

`Calendar-usage.md` Pair 3 documents the recommended implementation:

```tsx
<Calendar
  displayMode="dateRange"
  disabledDates={buildDisabledDates(windowStart)}
  disabledDateTooltip={(day) =>
    isBefore(day, windowStart)
      ? t('calendar.outsideReportWindow', '90-day report limit — earlier data is not retained')
      : undefined
  }
/>
```

If `@8x8/oxygen-calendar` gains a `maxRangeDays` prop in a future release, update Pair 3 to prefer that API.

---

## Recommended resolution order

1. **WARN-003** — Fix stale "(CONFLICT, open)" note in `Calendar-usage.md` Pair 3 (~1 min)
2. **GAP-004, GAP-005, GAP-006** — auto-fixable DOC_GAPs in props.md (doc-rewrite can handle)
3. **GAP-002 + GAP-007** — resolve token names from UI-Foundations library (`iVY5nI8JAxM05Apnnvozzs`)
4. **GAP-001** — confirm Storybook examples with component team
5. **GAP-008** — request Figma annotation nodes from design team
6. **GAP-009, GAP-010** — verify ARIA root role + WCAG contrast/focus checks post-token-resolution
7. **Figma Do/Don't cards** — request designer adds `✅ Do —` / `❌ Don't —` frames to `↳ Calendar examples` page; then re-run `figma-extract-usage` to replace editorial pairs

---

_Source: doc-audit skill v1.0 · Calendar · Re-audited 2026-05-12 (prior audit: 2026-05-08)_
