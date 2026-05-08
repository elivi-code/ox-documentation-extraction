---
rubric_version: "1.0"
component: SlideOut
package: "@8x8/oxygen-slide-out"
audit_date: "2026-05-05"
auditor: doc-audit skill
updated: "2026-05-05"

file_inventory:
  present:
    - props.md
    - examples.md
    - tokens.md
    - accessibility.md
  missing:
    - SlideOut-figma.md
    - SlideOut-usage.md
    - SlideOut-pui.md

dimension_scores:
  props_completeness:   { score: 0.45, coverage: "9/9 props listed; 4 props have no descriptions in MCP source; onResize observed in example but absent from props registry; all defaults missing" }
  examples_quality:     { score: 0.40, coverage: "1 example — derived from raw Storybook documentation story; MCP get-component-examples returned 0 clean snippets; controlled toggle + resize pattern shown" }
  token_coverage:       { score: 0.10, coverage: "0 tokens returned by MCP; tokens.md present but contains no actual token data; gap documented" }
  accessibility:        { score: 0.50, coverage: "ARIA roles, keyboard interactions, screen reader guidance, WCAG checklist all present; entirely inferred from component nature — MCP returned no explicit a11y data" }
  figma_fidelity:       { score: 0.0,  coverage: "SlideOut-figma.md absent — user confirmed no Figma design exists for this component" }
  pui_integration:      { score: 0.50, coverage: "SlideOut-pui.md absent; Platform UI MCP search returned 0 results; no explicit N/A marker written to confirm no PUI concern" }
  usage_guidelines:     { score: 0.0,  coverage: "SlideOut-usage.md absent — no Figma design means no Examples page to extract from" }

overall_score: 0.28

counts:
  doc_gaps: 1
  source_gaps: 8
  conflicts: 0
  warnings: 1

verdict: PARTIAL
verdict_reason: >
  GAP-001 is a blocker SOURCE_GAP: SlideOut-figma.md is absent because no Figma design
  exists for this component. This permanently blocks the figma_fidelity and
  usage_guidelines dimensions from being completed. Zero CONFLICTs exist.
  doc-rewrite can proceed on the four available dimensions (props, examples, tokens,
  accessibility), but the resulting spec will be explicitly flagged as lacking visual
  design reference. Remaining source gaps (onResize undocumented, 4 props undescribed,
  0 tokens, all a11y inferred) should be resolved from component source before rewrite
  if possible.

gaps:
  - id: GAP-001
    dimension: figma_fidelity
    severity: blocker
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: "(file absent)"
      location: "SlideOut-figma.md — not present in directory"
      finding: >
        No SlideOut-figma.md exists. User confirmed that no Figma design has been
        created for this component. Visual spec, anatomy, spacing, variant axes,
        and token bindings from Figma are therefore permanently unavailable unless
        a design is created upstream.
    fix_action: "Request Figma design creation for SlideOut from the design owner. Once a Figma node exists, run figma-extract to produce SlideOut-figma.md."
    blocks: [doc-rewrite-figma-dimension, SlideOut-usage.md]
    dependency: []

  - id: GAP-002
    dimension: usage_guidelines
    severity: major
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: "(file absent)"
      location: "SlideOut-usage.md — not present in directory"
      finding: >
        No SlideOut-usage.md exists. Since no Figma design exists (GAP-001), there
        is no Figma Examples page to extract Do/Don't usage guidance from. Usage
        guidelines cannot be produced until a Figma design is created.
    fix_action: "Blocked by GAP-001. Once a Figma design with an Examples page is created, run figma-extract-usage to produce SlideOut-usage.md."
    blocks: [doc-rewrite]
    dependency: [GAP-001]

  - id: GAP-003
    dimension: pui_integration
    severity: major
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: "(file absent)"
      location: "SlideOut-pui.md — not present in directory"
      finding: >
        No SlideOut-pui.md exists. Platform UI MCP search returned 0 results for
        "SlideOut", suggesting no PUI application-layer concerns exist. However,
        no explicit N/A marker has been written to formally confirm this determination
        in the file inventory.
    fix_action: "Write a minimal SlideOut-pui.md containing only the '<!-- NO RELEVANT PUI CONTEXT -->' marker to formally confirm that no PUI integration concerns exist for this component."
    blocks: []
    dependency: []

  - id: GAP-004
    dimension: props_completeness
    severity: major
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: props.md
      location: "Props table — hasAnimation, defaultWidth, minWidth, maxWidth rows"
      finding: >
        Four props (`hasAnimation`, `defaultWidth`, `minWidth`, `maxWidth`) have
        empty descriptions in the MCP source. Their purpose can only be inferred
        from their names. Consumers cannot understand the expected units for
        `defaultWidth`, `minWidth`, `maxWidth` (pixels? percentage?) or what
        `hasAnimation` controls without source-level documentation.
    fix_action: "Obtain prop descriptions from the @8x8/oxygen-slide-out component source, JSDoc comments, or Storybook argTypes. Update props.md with accurate descriptions and specify units for the width props."
    blocks: [doc-rewrite]
    dependency: []

  - id: GAP-005
    dimension: props_completeness
    severity: major
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: props.md
      location: "Observed but undocumented props section — onResize"
      finding: >
        The `onResize` callback is passed to `<SlideOut>` in the Storybook
        documentation story (`onResize={handleResize}`) but is entirely absent
        from the MCP props registry. Its type (`(newWidth: number) => void`) is
        inferred from the story's handler implementation, not from a source
        definition. If `onResize` is a real public prop, the MCP props registry
        is incomplete.
    fix_action: "Confirm whether `onResize` is a documented public prop by checking the component source or TypeScript types. If confirmed, add it to the props table in props.md with its type signature and description."
    blocks: [doc-rewrite]
    dependency: []

  - id: GAP-006
    dimension: props_completeness
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: true
    evidence:
      source_file: props.md
      location: "Props table — Default column (all rows show '—')"
      finding: >
        Default values are missing for all 9 listed props. At minimum, the defaults
        for `isVisible`, `isResizable`, and `hasAnimation` are important for
        understanding the component's out-of-box state. The default for `defaultWidth`
        is also critical — consumers need to know what width the panel opens to if
        not specified.
    fix_action: "Populate the Default column for each prop from component source, Storybook controls panel, or argTypes configuration."
    blocks: []
    dependency: []

  - id: GAP-007
    dimension: examples_quality
    severity: major
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: examples.md
      location: "Line 5 — 'The Oxygen MCP returned 0 clean examples'"
      finding: >
        `get-component-examples` with `cleanExamples: true` returned 0 results.
        The single example in examples.md was hand-cleaned from the raw Storybook
        documentation story and uses `onResize` (a prop not in the registry — GAP-005).
        No examples cover: isResizable, hasAnimation, defaultWidth/minWidth/maxWidth
        constraints, or a non-resizable fixed-width variant.
    fix_action: "Obtain clean usage examples from Storybook stories or component documentation. Add examples covering: resizable vs. fixed-width, animation on/off, min/max width constraints, and controlled open/close with a trigger."
    blocks: []
    dependency: [GAP-005]

  - id: GAP-008
    dimension: token_coverage
    severity: major
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: tokens.md
      location: "Line 7 — 'No theme tokens were returned by the Oxygen MCP'"
      finding: >
        The MCP `get-theme-tokens` search for "slideout" returned 0 matches.
        SlideOut's visual properties (panel background, border, shadow, resize
        handle colour, width constraints) are unresolvable to design tokens from
        the available MCP data. Whether this reflects a genuine absence of tokens
        or a naming mismatch in the token registry is unknown.
    fix_action: "Search the token registry with alternative terms ('slide', 'panel', 'drawer') or inspect the @8x8/oxygen-slide-out component CSS/styled-components source to identify which tokens are consumed. Update tokens.md accordingly."
    blocks: [doc-rewrite]
    dependency: []

  - id: GAP-009
    dimension: accessibility
    severity: major
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: accessibility.md
      location: "Line 5 — 'The Oxygen MCP returned no explicit accessibility documentation'"
      finding: >
        The entire accessibility.md is inferred from the component's drawer/panel
        nature. No ARIA roles, keyboard interactions, or focus management behaviour
        are confirmed from the component source or MCP. In particular: whether the
        component itself applies `aria-hidden` when not visible, whether it traps
        focus in dialog mode, and whether the resize handle is keyboard-accessible
        are all unknown.
    fix_action: "Obtain confirmed accessibility implementation from component source, Storybook a11y addon output, or engineering. Replace inferred content with deterministic data."
    blocks: [doc-rewrite]
    dependency: []

warnings:
  - id: WARN-001
    dimension: props_completeness
    confidence: heuristic
    finding: >
      The `minWidth` and `maxWidth` props list numeric types without specifying
      units. If the component expects pixels (the most likely assumption given
      `onResize` returning `newWidth: number`), this should be stated explicitly.
      If it accepts CSS values or percentages, the type annotation `number` would
      be incorrect.
    advisory: "Clarify the unit expected by minWidth, maxWidth, and defaultWidth (pixels vs. other). Update prop descriptions and types accordingly."
# --- navigation (added by component-map) ---
role: audit
pipeline_stage: spec_ready
pipeline_note: "Audit verdict YES/PARTIAL — doc-rewrite can run"
siblings:
  - "[[SlideOut/props]]"
  - "[[SlideOut/examples]]"
  - "[[SlideOut/tokens]]"
  - "[[SlideOut/accessibility]]"
tags:
  - oxygen
  - component/SlideOut
  - role/audit
  - stage/spec_ready
---

# SlideOut — Audit Report

> **Verdict: PARTIAL** — GAP-001 is a permanent blocker SOURCE_GAP: no Figma design exists for SlideOut. `figma_fidelity` and `usage_guidelines` dimensions cannot be completed without upstream design work. `doc-rewrite` can proceed on props, examples, tokens, and accessibility dimensions. Resolve GAP-004/GAP-005 (missing prop descriptions + onResize) and GAP-008 (tokens) from source before rewriting for best coverage.

## Summary

| Dimension | Score | Status |
|-----------|-------|--------|
| Props completeness | 0.45 | 9 props listed; 4 undescribed; onResize unregistered; all defaults missing |
| Examples quality | 0.40 | 1 Storybook-derived example; 0 clean MCP examples; limited coverage |
| Token coverage | 0.10 | 0 tokens from MCP; file present but empty of data |
| Accessibility | 0.50 | Full structure present but entirely inferred — no MCP source data |
| Figma fidelity | 0.00 | SlideOut-figma.md absent — no Figma design exists |
| PUI integration | 0.50 | No PUI results found; no explicit N/A marker written |
| Usage guidelines | 0.00 | SlideOut-usage.md absent — blocked by missing Figma design |
| **Overall** | **0.28** | |

## Gap register

| ID | Dimension | Severity | Type | Summary |
|----|-----------|----------|------|---------|
| GAP-001 | figma_fidelity | blocker | SOURCE_GAP | No Figma design exists — SlideOut-figma.md cannot be produced |
| GAP-002 | usage_guidelines | major | SOURCE_GAP | SlideOut-usage.md absent — blocked by GAP-001 (no Figma) |
| GAP-003 | pui_integration | major | SOURCE_GAP | SlideOut-pui.md absent; PUI search returned 0 results but no N/A marker written |
| GAP-004 | props_completeness | major | SOURCE_GAP | 4 props (hasAnimation, defaultWidth, minWidth, maxWidth) have no descriptions in MCP |
| GAP-005 | props_completeness | major | SOURCE_GAP | `onResize` observed in Storybook story but absent from props registry |
| GAP-006 | props_completeness | minor | DOC_GAP | Default values missing for all 9 props |
| GAP-007 | examples_quality | major | SOURCE_GAP | 0 clean MCP examples; 1 Storybook-derived example only; limited coverage |
| GAP-008 | token_coverage | major | SOURCE_GAP | 0 tokens from MCP; visual token bindings unknown |
| GAP-009 | accessibility | major | SOURCE_GAP | All accessibility content inferred — no confirmed ARIA or keyboard data |

## Warnings

| ID | Dimension | Advisory |
|----|-----------|---------|
| WARN-001 | props_completeness | Clarify units for `minWidth`, `maxWidth`, `defaultWidth` — number type without unit spec is ambiguous |

## Resolution path

To unblock `doc-rewrite` on available dimensions (props, examples, tokens, accessibility):

1. **GAP-004 + GAP-005 (props):** Check `@8x8/oxygen-slide-out` component source or Storybook argTypes for `hasAnimation`, `defaultWidth`, `minWidth`, `maxWidth` descriptions and confirm whether `onResize` is a public prop. Update props.md.
2. **GAP-008 (tokens):** Search token registry with alternate terms ('slide', 'panel', 'drawer') or inspect component CSS source. Update tokens.md.
3. **GAP-009 (accessibility):** Obtain confirmed ARIA/keyboard implementation from component source or Storybook a11y addon.
4. **GAP-003 (pui):** Write a minimal `SlideOut-pui.md` with the `<!-- NO RELEVANT PUI CONTEXT -->` marker to formally close this dimension.

GAP-001 and GAP-002 (Figma + Usage) are permanently blocked until a Figma design is created. Flag to the design owner.

Minor gap (GAP-006) and warning (WARN-001) are auto-fixable or advisory and do not block rewrite.
