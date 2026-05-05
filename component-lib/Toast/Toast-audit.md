---
rubric_version: "1.0"
component: Toast
package: "@8x8/oxygen-toast"
audit_date: "2026-05-05"
auditor: doc-audit skill

file_inventory:
  present:
    - props.md
    - examples.md
    - tokens.md
    - accessibility.md
    - Toast-figma.md
    - Toast-pui.md
    - figma-screenshot-toast.png
  missing:
    - Toast-usage.md

dimension_scores:
  props_completeness:   { score: 0.65, coverage: "11/11 Toast props present; InlineNotification props absent; ActionType shape undefined; most defaults missing" }
  examples_quality:     { score: 0.72, coverage: "6 examples (basic, types, sizes, actions, hide-close, Toaster, ToastStack); no InlineNotification example; examples derived from Storybook, not clean MCP output" }
  token_coverage:       { score: 0.85, coverage: "Container + type-indicator + typography tokens all resolved with Light/Dark primitives; spacing/radius values hardcoded (no token bindings confirmed)" }
  accessibility:        { score: 0.50, coverage: "8-row WCAG checklist present; ARIA roles and keyboard table present; all inferred — MCP returned no explicit accessibility data" }
  figma_fidelity:       { score: 0.82, coverage: "Full anatomy, spacing, variant axes, token bindings confirmed; keyboard/ARIA annotations absent in Figma; Style axis vs. code API CONFLICT" }
  pui_integration:      { score: 1.0,  coverage: "NO RELEVANT PUI CONTEXT marker present; all candidates reviewed and rejected" }
  usage_guidelines:     { score: 0.0,  coverage: "Toast-usage.md absent" }

overall_score: 0.65

counts:
  doc_gaps: 5
  source_gaps: 3
  conflicts: 1
  warnings: 2

verdict: NO
verdict_reason: >
  One unresolved CONFLICT: the Figma component set exposes a "Style" variant axis
  (Full notification / Group collapsed / Group expanded) that has no corresponding
  `style` prop in the Oxygen `Toast` API. It is unclear whether grouped/stacked
  behaviour is handled entirely by `ToastStack` + `Toaster`, or whether the Figma
  design implies a prop that is missing from the code surface. This must be resolved
  by a human (designer or engineer) before `doc-rewrite` can run. Additionally,
  `Toast-usage.md` is missing (major DOC_GAP) and accessibility data is fully
  inferred with no MCP confirmation (major SOURCE_GAP).

gaps:
  - id: GAP-001
    dimension: figma_fidelity
    severity: blocker
    type: CONFLICT
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: Toast-figma.md
      location: "Gaps & conflicts table, item 8; API — Component properties section"
      finding: >
        The Figma Notification component set has a `Style` variant axis with three
        values: "Full notification", "Group collapsed", and "Group expanded". The
        Oxygen `Toast` component API (props.md) exposes no `style` prop. The Figma
        `Style` variants appear to be handled by `ToastStack` + `Toaster` at the
        application layer, but this is not confirmed. If Figma `Style` implies a
        missing prop, the documentation and potentially the component API is
        incomplete.
    fix_action: "Confirm with design/engineering whether Figma Style variants (Group collapsed / Group expanded) map to ToastStack/Toaster behaviour only, or require a `style` prop on Toast. Update props.md and figma spec accordingly."
    blocks: [doc-rewrite]
    dependency: []

  - id: GAP-002
    dimension: accessibility
    severity: major
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: accessibility.md
      location: "Line 7 — 'No explicit ARIA role data was returned by the MCP. The following is inferred…'"
      finding: >
        The entire accessibility file is labelled as inferred. The MCP returned no
        explicit ARIA role, keyboard interaction, or live-region data for the Toast
        component. The documented `role="status"` / `role="alert"` split, `Escape`
        key behaviour, and `aria-live` guidance are all heuristic extrapolations
        from component intent, not confirmed from source.
    fix_action: "Obtain confirmed ARIA implementation from the oxygen-toast source code (or Storybook a11y addon output) and replace inferred content with deterministic data."
    blocks: [doc-rewrite]
    dependency: []

  - id: GAP-003
    dimension: usage_guidelines
    severity: major
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: "(file absent)"
      location: "Toast-usage.md — not present in directory"
      finding: >
        No Toast-usage.md file exists. Do/Don't editorial guidance from the Figma
        "Toast — Examples" page (if it exists) has not been extracted. Without
        usage guidelines the spec cannot communicate design intent to consumers.
    fix_action: "Run figma-extract-usage skill for the Toast component to check for an Examples page. If found, extract and write Toast-usage.md. If the page does not exist in Figma, mark as SOURCE_GAP and note accordingly."
    blocks: [doc-rewrite]
    dependency: []

  - id: GAP-004
    dimension: props_completeness
    severity: major
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: true
    evidence:
      source_file: props.md
      location: "InlineNotification section — 'No props available from MCP'"
      finding: >
        `InlineNotification` is a named export of `@8x8/oxygen-toast` but its prop
        surface is entirely absent — the MCP returned no data. The component is
        also noted as "Documentation not available" on the Oxygen docs site (per
        Figma annotation in Toast-figma.md). Consumers cannot use the component
        from documentation alone.
    fix_action: "Extract InlineNotification props directly from the component source or Storybook. Add a props table to props.md and at least one InlineNotification example to examples.md."
    blocks: []
    dependency: []

  - id: GAP-005
    dimension: props_completeness
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: true
    evidence:
      source_file: props.md
      location: "Toast props table — Default column"
      finding: >
        The `ActionType` shape (used by the `actions` prop) is not defined anywhere
        in props.md. Consumers do not know what properties an action object must
        have (e.g. `label`, `onClick`, additional optional fields). This makes the
        `actions` prop unusable from documentation alone.
    fix_action: "Add an `ActionType` shape definition below the Toast props table, listing each field with its type and required/optional status."
    blocks: []
    dependency: []

  - id: GAP-006
    dimension: props_completeness
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: true
    evidence:
      source_file: props.md
      location: "Toast props table — Default column (all rows show '—')"
      finding: >
        Default values are missing for all 11 Toast props. Several props have
        semantically important defaults that affect rendering (e.g. whether
        `hideCloseControl` defaults to `false`, whether `isToast` defaults to
        `true`). Without defaults, consumers cannot reason about the component's
        out-of-box behaviour.
    fix_action: "Populate the Default column for each prop from the component source or Storybook controls panel."
    blocks: []
    dependency: []

  - id: GAP-007
    dimension: examples_quality
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: true
    evidence:
      source_file: examples.md
      location: "Lines 106-107 — note about derivation from Storybook"
      finding: >
        The footer note states examples were "derived from the Storybook story code
        and Toaster usage patterns" rather than sourced cleanly from the MCP. No
        `InlineNotification` usage example is provided. If the Storybook stories
        have evolved since extraction, the examples may be out of date or inaccurate.
    fix_action: "Add an InlineNotification usage example. Verify existing examples against current Storybook stories and correct any discrepancies."
    blocks: []
    dependency: []

  - id: GAP-008
    dimension: token_coverage
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: Toast-figma.md
      location: "Hardcoded values table; Structure and spacing table"
      finding: >
        Container width (`320px`), indicator bar width (`4px`), icon container size
        (`24px`), and border-radius (`6px`) are hardcoded in Figma with no token
        binding. Spacing values (padding, gaps) are also all hardcoded. These values
        cannot be resolved to design tokens without upstream Figma work to bind them.
    fix_action: "Flag to the Figma design owner that container width, indicator width, border-radius, and all spacing values should be bound to spacing/radius tokens. Document as SOURCE_GAP pending upstream fix."
    blocks: []
    dependency: []

  - id: GAP-009
    dimension: figma_fidelity
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: Toast-figma.md
      location: "Keyboard and focus notes section; ARIA notes section"
      finding: >
        Both the keyboard interaction and ARIA sections in Toast-figma.md contain
        `<!-- NOT FOUND IN FIGMA RESPONSE -->` markers. No accessibility annotations
        are present on the Notification component set in Figma. This is a gap in the
        Figma source, not in extraction.
    fix_action: "Request design owner add accessibility annotations (ARIA roles, keyboard interactions) to the Figma component set. Until then, accessibility.md must rely on inferred data (GAP-002)."
    blocks: []
    dependency: [GAP-002]

warnings:
  - id: WARN-001
    dimension: examples_quality
    confidence: heuristic
    finding: >
      The `notify()` imperative API usage in the Toaster example passes `content`
      (a string) rather than using `title`/`description` props. It is unclear whether
      `content` is the correct prop name for the `Toaster`/`notify()` API or if this
      is a simplified illustration. The `notify()` signature is not documented in
      props.md.
    advisory: "Verify the notify() function signature from @8x8/oxygen-toaster source/Storybook and add a `notify()` API table to props.md."

  - id: WARN-002
    dimension: figma_fidelity
    confidence: heuristic
    finding: >
      The Interaction component set (`9141:14534`) in the same Figma page covers
      incoming calls, meeting reminders, and messages — a separate domain with
      telephony/meeting UI concerns. It is noted as not mapped to the `Toast`/`Toaster`
      Oxygen package, but the relationship is assumed rather than confirmed. If any
      Interaction variants are implemented via `@8x8/oxygen-toast` internally, the
      component surface is wider than currently documented.
    advisory: "Confirm with engineering that the Interaction component set has no relationship to @8x8/oxygen-toast or @8x8/oxygen-toaster."
---

# Toast — Audit Report

> **Verdict: NO** — One unresolved CONFLICT (GAP-001: Figma `Style` axis vs. missing `style` prop in code) blocks `doc-rewrite`. Two major gaps also require resolution before the spec can be considered authoritative: accessibility data is fully inferred with no MCP confirmation (GAP-002 / SOURCE_GAP), and `Toast-usage.md` is absent (GAP-003 / DOC_GAP).

## Summary

| Dimension | Score | Status |
|-----------|-------|--------|
| Props completeness | 0.65 | InlineNotification props absent; ActionType undefined; defaults missing |
| Examples quality | 0.72 | 6 examples present; derived from Storybook; no InlineNotification example |
| Token coverage | 0.85 | Color + typography tokens fully resolved; spacing/radius hardcoded |
| Accessibility | 0.50 | Content present but entirely inferred — MCP returned no explicit data |
| Figma fidelity | 0.82 | Detailed spec; CONFLICT on Style axis; no Figma a11y annotations |
| PUI integration | 1.00 | No relevant PUI context (confirmed) |
| Usage guidelines | 0.00 | Toast-usage.md missing |
| **Overall** | **0.65** | |

## Gap register

| ID | Dimension | Severity | Type | Summary |
|----|-----------|----------|------|---------|
| GAP-001 | figma_fidelity | blocker | CONFLICT | Figma Style axis (Group collapsed / expanded) has no `style` prop in code |
| GAP-002 | accessibility | major | SOURCE_GAP | All accessibility content is inferred — no MCP or Figma source data |
| GAP-003 | usage_guidelines | major | DOC_GAP | Toast-usage.md absent |
| GAP-004 | props_completeness | major | DOC_GAP | InlineNotification props not available from MCP |
| GAP-005 | props_completeness | minor | DOC_GAP | ActionType shape not defined |
| GAP-006 | props_completeness | minor | DOC_GAP | Default values missing for all Toast props |
| GAP-007 | examples_quality | minor | DOC_GAP | No InlineNotification example; examples derived from Storybook |
| GAP-008 | token_coverage | minor | SOURCE_GAP | Spacing/radius values hardcoded in Figma; no token bindings |
| GAP-009 | figma_fidelity | minor | SOURCE_GAP | No keyboard/ARIA annotations found in Figma |

## Warnings

| ID | Dimension | Advisory |
|----|-----------|---------|
| WARN-001 | examples_quality | Verify `notify()` signature from @8x8/oxygen-toaster — `content` prop usage unconfirmed |
| WARN-002 | figma_fidelity | Confirm Interaction component set has no relationship to @8x8/oxygen-toast |

## Resolution path

To unblock `doc-rewrite`:

1. **Resolve GAP-001 (CONFLICT):** Get engineer/designer confirmation on whether Figma `Style` variants (Group collapsed / Group expanded) are handled solely by `ToastStack` + `Toaster`, or require a `style` prop on `Toast`. Update props.md and Toast-figma.md accordingly.
2. **Address GAP-002 (accessibility SOURCE_GAP):** Obtain confirmed ARIA implementation from component source or Storybook a11y output. Replace inferred content in accessibility.md.
3. **Extract GAP-003 (usage guidelines):** Run `figma-extract-usage` for Toast. If an Examples Figma page exists, extract it to `Toast-usage.md`.
4. **Fix GAP-004 (InlineNotification props):** Source `InlineNotification` props from component code or Storybook and add to props.md + examples.md.

Minor gaps (GAP-005 through GAP-009) are auto-fixable or advisory and do not block rewrite once the above are resolved.
