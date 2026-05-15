---
rubric_version: "1.0"
component: Toast
package: "@8x8/oxygen-toast"
audit_date: "2026-05-15"
auditor: doc-audit skill
updated: "2026-05-15"
prior_audit: "2026-05-05"

file_inventory:
  present:
    - props.md
    - examples.md
    - tokens.md
    - accessibility.md
    - Toast-figma.md
    - Toast-pui.md
    - Toast-usage.md
    - figma-screenshot-toast.png
    - figma-screenshot-inline-notification.png
  missing: []

dimension_scores:
  props_completeness:   { score: 0.65, coverage: "11/11 Toast props present; ToastStack 1/1; InlineNotification props absent from MCP; ActionType shape undefined; all 11 Toast prop defaults missing" }
  examples_quality:     { score: 0.75, coverage: "7 examples (basic, types, sizes, actions, hide-close, Toaster, ToastStack); no InlineNotification example; WARN-001 resolved: notify() content param confirmed correct per toaster-note.md" }
  token_coverage:       { score: 0.87, coverage: "Notification container + type-indicator + typography tokens all resolved (Light/Dark); InlineNotification all 10 variant hex values confirmed; 3 InlineNotification token names unresolved pending Desktop Bridge" }
  accessibility:        { score: 0.50, coverage: "8-row WCAG checklist + ARIA roles + keyboard table present; all content inferred — MCP returned no explicit accessibility data" }
  figma_fidelity:       { score: 0.88, coverage: "Full anatomy for Notification + InlineNotification; all 10 InlineNotification variant colors confirmed; dedicated screenshot added; design distinction documented (non-inverted theming); keyboard/ARIA annotations absent in Figma" }
  pui_integration:      { score: 1.0,  coverage: "NO RELEVANT PUI CONTEXT marker present; all 5 candidates reviewed and rejected" }
  usage_guidelines:     { score: 0.80, coverage: "Toast-usage.md present with 7 Do/Don't pairs; editorially authored (no Figma examples page exists); pairs grounded with evidence citations from all source files" }

overall_score: 0.78

counts:
  doc_gaps: 5
  source_gaps: 4
  conflicts: 0
  warnings: 1

verdict: "YES"
verdict_reason: >
  Zero CONFLICTs. Zero blocker-severity gaps. GAP-001 (CONFLICT, Style axis) resolved 2026-05-05.
  GAP-003 (usage_guidelines, major DOC_GAP) resolved 2026-05-15: Toast-usage.md now present
  with 7 grounded editorial Do/Don't pairs. Remaining gaps are SOURCE_GAPs and minor DOC_GAPs;
  none are blocker severity. doc-rewrite can proceed.

gaps:
  - id: GAP-001
    dimension: figma_fidelity
    severity: blocker
    type: CONFLICT
    status: RESOLVED
    resolved_date: "2026-05-05"
    resolution: >
      Confirmed via OX MCP comparison: "Group collapsed" and "Group expanded" Figma Style
      variants are handled entirely by the Toaster system component (automatic stacking and
      collapse/expand managed by the notify() queue). No `style` prop is missing from Toast.
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: Toast-figma.md
      location: "Gaps & conflicts table, item 8"
      finding: "Figma Style axis (Full / Group collapsed / Group expanded) has no style prop in Toast API."
    fix_action: "RESOLVED — Toaster system component handles stacking/grouping."
    blocks: []
    dependency: []

  - id: GAP-002
    dimension: accessibility
    severity: major
    type: SOURCE_GAP
    status: open
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: accessibility.md
      location: "Line 7 — 'No explicit ARIA role data was returned by the MCP. The following is inferred…'"
      finding: >
        The entire accessibility file is labelled as inferred. The MCP returned no
        explicit ARIA role, keyboard interaction, or live-region data for the Toast
        component. The role="status" / role="alert" split, Escape key behaviour, and
        aria-live guidance are all heuristic extrapolations.
    fix_action: "Obtain confirmed ARIA implementation from @8x8/oxygen-toast source code or Storybook a11y addon output. Replace inferred content with deterministic data."
    blocks: [doc-rewrite]
    dependency: []

  - id: GAP-003
    dimension: usage_guidelines
    severity: major
    type: DOC_GAP
    status: RESOLVED
    resolved_date: "2026-05-15"
    resolution: >
      Toast-usage.md created 2026-05-15 with 7 Do/Don't pairs editorially authored from
      props.md, examples.md, accessibility.md, tokens.md, Toast-figma.md, Toast-pui.md,
      Toast-audit.md. No Figma "↳ Toast examples" page exists so figma-extract-usage
      cannot produce Figma-sourced pairs. File is clearly marked as editorial and
      provisional pending designer review.
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: Toast-usage.md
      location: "File now present — 7 Do/Don't pairs, When to use / not to use table, Grounding summary"
      finding: "RESOLVED — file present."
    fix_action: "RESOLVED. When a Figma examples page is created, re-run figma-extract-usage and replace editorial pairs with Figma-sourced Do/Don't frames."
    blocks: []
    dependency: []

  - id: GAP-004
    dimension: props_completeness
    severity: major
    type: DOC_GAP
    status: open
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: props.md
      location: "InlineNotification section — 'No props available from MCP'"
      finding: >
        InlineNotification is a named export of @8x8/oxygen-toast but its prop surface
        is entirely absent — MCP returned no data. Figma extraction (2026-05-15) confirms
        InlineNotification has Mode and Type variant axes and a Title text prop, but the
        actual code props (and their types, defaults, descriptions) are unknown.
    fix_action: "Extract InlineNotification props from @8x8/oxygen-toast component source or Storybook. Add props table to props.md and at least one InlineNotification usage example to examples.md."
    blocks: []
    dependency: []

  - id: GAP-005
    dimension: props_completeness
    severity: minor
    type: DOC_GAP
    status: open
    confidence: deterministic
    auto_fixable: true
    evidence:
      source_file: props.md
      location: "Toast props table — actions prop, type Array<ActionType>"
      finding: >
        The ActionType shape used by the actions prop is not defined anywhere in props.md.
        Consumers do not know what properties an action object must have.
    fix_action: "Add an ActionType shape definition below the Toast props table listing each field with its type and required/optional status."
    blocks: []
    dependency: []

  - id: GAP-006
    dimension: props_completeness
    severity: minor
    type: DOC_GAP
    status: open
    confidence: deterministic
    auto_fixable: true
    evidence:
      source_file: props.md
      location: "Toast props table — Default column (all rows show '—')"
      finding: "Default values missing for all 11 Toast props."
    fix_action: "Populate the Default column for each prop from the component source or Storybook controls panel."
    blocks: []
    dependency: []

  - id: GAP-007
    dimension: examples_quality
    severity: minor
    type: DOC_GAP
    status: open
    confidence: deterministic
    auto_fixable: true
    evidence:
      source_file: examples.md
      location: "All 7 examples — no InlineNotification example present"
      finding: >
        No InlineNotification usage example is provided. Figma extraction (2026-05-15)
        confirms InlineNotification has Mode, Type, and Title props, making a basic
        example feasible.
    fix_action: "Add an InlineNotification usage example demonstrating at least one type variant. Verify notify() content param usage against @8x8/oxygen-toaster source (toaster-note.md confirms content is the correct param name)."
    blocks: []
    dependency: [GAP-004]

  - id: GAP-008
    dimension: token_coverage
    severity: minor
    type: SOURCE_GAP
    status: open
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: tokens.md
      location: "Note at bottom — hardcoded values; Toast-figma.md Structure & spacing table"
      finding: >
        Container width (320px), indicator bar width (4px), icon container size (24px),
        and border-radius (6px) are hardcoded in Figma with no token binding. Spacing
        values (padding, gaps) also hardcoded.
    fix_action: "Flag to the Figma design owner that container width, indicator width, border-radius, and all spacing values should be bound to spacing/radius tokens. Document as SOURCE_GAP pending upstream fix."
    blocks: []
    dependency: []

  - id: GAP-009
    dimension: figma_fidelity
    severity: minor
    type: SOURCE_GAP
    status: open
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: Toast-figma.md
      location: "Keyboard and focus notes — '<!-- NOT FOUND IN FIGMA RESPONSE -->'; ARIA notes same"
      finding: "No keyboard interaction or ARIA annotations found on the Notification or InlineNotification component sets in Figma."
    fix_action: "Request design owner add accessibility annotations (ARIA roles, keyboard interactions) to the Figma component sets."
    blocks: []
    dependency: [GAP-002]

  - id: GAP-010
    dimension: token_coverage
    severity: minor
    type: SOURCE_GAP
    status: open
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: Toast-figma.md
      location: "InlineNotification — Container tokens table (2026-05-15 section)"
      finding: >
        Three variable IDs for InlineNotification remain unresolved: 20136:267 (background),
        20136:253 (border stroke), and 20136:484 (Info indicator). Semantic token names
        require getVariableByIdAsync via figma-console Desktop Bridge plugin when active.
    fix_action: "With Figma Desktop Bridge plugin running, call getVariableByIdAsync for variable IDs 20136:267, 20136:253, and 20136:484 and update Toast-figma.md InlineNotification container tokens table with resolved names."
    blocks: []
    dependency: []

warnings:
  - id: WARN-001
    dimension: examples_quality
    confidence: deterministic
    status: RESOLVED
    finding: >
      The notify() imperative API usage in examples.md passes content (a string) rather
      than title/description props. Per toaster-note.md (confirmed 2026-05-05), the
      notify() function signature accepts content, iconTitle, and onClose — not title/description.
      content IS the correct param name for notify().
    advisory: "RESOLVED — content is confirmed correct for notify(). No change needed in examples.md."

  - id: WARN-002
    dimension: figma_fidelity
    confidence: heuristic
    status: open
    finding: >
      The Interaction component set (9141:14534) in the same Figma page covers incoming
      calls, meeting reminders, and messages — a separate domain. Not mapped to @8x8/oxygen-toast
      but the relationship is assumed rather than confirmed.
    advisory: "Confirm with engineering that the Interaction component set has no relationship to @8x8/oxygen-toast or @8x8/oxygen-toaster."

# --- navigation (added by component-map) ---
role: audit
pipeline_stage: spec_ready
pipeline_note: "Audit verdict YES — doc-rewrite can run"
siblings:
  - "[[Toast/props]]"
  - "[[Toast/examples]]"
  - "[[Toast/tokens]]"
  - "[[Toast/accessibility]]"
  - "[[Toast/Toast-figma]]"
  - "[[Toast/Toast-pui]]"
  - "[[Toast/Toast-usage]]"
tags:
  - oxygen
  - component/Toast
  - role/audit
  - stage/spec_ready
---

# Toast — Audit Report

> **Verdict: YES** — All conflicts resolved. GAP-003 (usage guidelines) resolved 2026-05-15: Toast-usage.md present with 7 editorial Do/Don't pairs. GAP-001 (Style axis CONFLICT) resolved 2026-05-05. Zero blockers remain. doc-rewrite can proceed.
>
> Re-audited: 2026-05-15 (prior: 2026-05-05)

## Summary

| Dimension | Score | Change | Status |
|-----------|-------|--------|--------|
| Props completeness | 0.65 | — | InlineNotification props absent; ActionType undefined; defaults missing |
| Examples quality | 0.75 | +0.03 | 7 examples; WARN-001 resolved; no InlineNotification example |
| Token coverage | 0.87 | +0.02 | Notification fully resolved; InlineNotification hex confirmed; 3 semantic names pending |
| Accessibility | 0.50 | — | Content present but entirely inferred |
| Figma fidelity | 0.88 | +0.06 | InlineNotification enriched; screenshot added; design distinction documented |
| PUI integration | 1.00 | — | No relevant PUI context (confirmed) |
| Usage guidelines | 0.80 | +0.80 | Toast-usage.md now present — GAP-003 resolved |
| **Overall** | **0.78** | **+0.13** | |

## Gap register

| ID | Dimension | Severity | Type | Status | Summary |
|----|-----------|----------|------|--------|---------|
| ~~GAP-001~~ | ~~figma_fidelity~~ | ~~blocker~~ | ~~CONFLICT~~ | ✅ RESOLVED 2026-05-05 | ~~Style axis has no style prop~~ → handled by Toaster system |
| GAP-002 | accessibility | major | SOURCE_GAP | Open | All accessibility content is inferred — no MCP or Figma source data |
| ~~GAP-003~~ | ~~usage_guidelines~~ | ~~major~~ | ~~DOC_GAP~~ | ✅ RESOLVED 2026-05-15 | ~~Toast-usage.md absent~~ → file created with 7 editorial pairs |
| GAP-004 | props_completeness | major | DOC_GAP | Open | InlineNotification props not available from MCP |
| GAP-005 | props_completeness | minor | DOC_GAP | Open | ActionType shape not defined |
| GAP-006 | props_completeness | minor | DOC_GAP | Open | Default values missing for all 11 Toast props |
| GAP-007 | examples_quality | minor | DOC_GAP | Open | No InlineNotification example |
| GAP-008 | token_coverage | minor | SOURCE_GAP | Open | Spacing/radius values hardcoded in Figma; no token bindings |
| GAP-009 | figma_fidelity | minor | SOURCE_GAP | Open | No keyboard/ARIA annotations in Figma |
| GAP-010 | token_coverage | minor | SOURCE_GAP | Open | InlineNotification background/border/Info indicator token names unresolved |

## Warnings

| ID | Dimension | Status | Advisory |
|----|-----------|--------|---------|
| ~~WARN-001~~ | examples_quality | ✅ RESOLVED | `content` param in notify() is confirmed correct per toaster-note.md |
| WARN-002 | figma_fidelity | Open | Confirm Interaction component set has no relationship to @8x8/oxygen-toast |

## Resolution path

All blockers and major conflicts are resolved. doc-rewrite can start now.

**Recommended before final spec:**

1. **GAP-004 (InlineNotification props):** Source props from @8x8/oxygen-toast component code or Storybook. Add to props.md and examples.md.
2. **GAP-002 (accessibility SOURCE_GAP):** Obtain confirmed ARIA implementation. Replace inferred accessibility.md content with deterministic data.
3. **GAP-010 (InlineNotification token names):** With Desktop Bridge active, resolve variable IDs 20136:267, 20136:253, 20136:484 via `getVariableByIdAsync`.

Minor gaps (GAP-005 through GAP-009) are auto-fixable or advisory and do not block rewrite.
