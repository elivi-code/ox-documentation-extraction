---
rubric_version: "1.0"
component: SlideOut
package: "@8x8/oxygen-slide-out"
audit_date: "2026-05-05"
auditor: doc-audit skill
updated: "2026-05-15"

file_inventory:
  present:
    - props.md
    - examples.md
    - tokens.md
    - accessibility.md
    - SlideOut-usage.md     # editorial — see WARN-002
  missing:
    - SlideOut-figma.md
    - SlideOut-pui.md

dimension_scores:
  props_completeness:   { score: 0.45, coverage: "9/9 props listed; 4 props have no descriptions in MCP source; onResize observed in example but absent from props registry; all defaults missing" }
  examples_quality:     { score: 0.40, coverage: "1 example — derived from raw Storybook documentation story; MCP get-component-examples returned 0 clean snippets; controlled toggle + resize pattern shown" }
  token_coverage:       { score: 0.10, coverage: "0 tokens returned by MCP; tokens.md present but contains no actual token data; gap documented" }
  accessibility:        { score: 0.50, coverage: "ARIA roles, keyboard interactions, screen reader guidance, WCAG checklist all present; entirely inferred from component nature — MCP returned no explicit a11y data" }
  figma_fidelity:       { score: 0.0,  coverage: "SlideOut-figma.md absent — user confirmed no Figma design exists for this component" }
  pui_integration:      { score: 0.50, coverage: "SlideOut-pui.md absent; Platform UI MCP search returned 0 results; no explicit N/A marker written to confirm no PUI concern" }
  usage_guidelines:     { score: 0.55, coverage: "SlideOut-usage.md present (editorial — see WARN-002); 7 grounded Do/Don't pairs with file:line citations, When-to-use / When-not-to-use sections, inferred Anatomy block; missing Figma-sourced verification, screenshots, and the canonical figma-extract-usage provenance" }

overall_score: 0.36

counts:
  doc_gaps: 1
  source_gaps: 7
  conflicts: 0
  warnings: 2

verdict: PARTIAL
verdict_reason: >
  GAP-001 remains a blocker SOURCE_GAP: SlideOut-figma.md is absent because no
  Figma design exists for this component. This permanently blocks the figma_fidelity
  dimension and prevents figma-extract-usage from producing the canonical usage
  doc. Zero CONFLICTs exist.

  Re-audited 2026-05-15: GAP-002 (usage absent) is now resolved editorially —
  SlideOut-usage.md was authored via usage-advisor Open mode with 7 grounded
  Do/Don't pairs (see WARN-002), mirroring the ProgressBar/PopoverMenu precedent.
  The usage_guidelines dimension score moves from 0.0 to 0.55; overall_score
  from 0.28 to 0.36.

  doc-rewrite can now proceed on five dimensions (props, examples, tokens,
  accessibility, usage) but the resulting spec will still be explicitly flagged
  as lacking visual design reference (figma_fidelity = 0.0) until upstream Figma
  work lands. Remaining source gaps (onResize undocumented, 4 props undescribed,
  0 tokens, all a11y inferred) should be resolved from component source before
  rewrite if possible.

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
    resolved_editorially: WARN-002
    resolution_date: "2026-05-15"
    evidence:
      source_file: "SlideOut-usage.md"
      location: "SlideOut-usage.md — present (editorial, drafted via usage-advisor on 2026-05-15)"
      finding: >
        Originally: no SlideOut-usage.md existed, blocked by GAP-001 (no Figma).
        Resolved editorially 2026-05-15: SlideOut-usage.md was authored via
        usage-advisor Open mode with 7 grounded Do/Don't pairs covering
        SlideOut-vs-Modal-vs-Drawer, controlled isVisible state, role choice
        (dialog vs complementary), Escape/outside-click/focus-return wiring,
        aria-hidden toggling, isResizable + min/max width, and content
        density / scroll. Every pair carries a `**Source:**` line citing
        props.md / examples.md / accessibility.md by line. The editorial
        provenance is captured as WARN-002 and must be replaced with
        figma-extract-usage output if a `↳ SlideOut examples` Figma page is
        ever authored.
    fix_action: "Resolved editorially via WARN-002. To convert to a canonical source-grounded usage doc, GAP-001 must first be cleared (Figma design created), then `↳ SlideOut examples` page authored with ✅ Do / ❌ Don't card frames, then run figma-extract-usage to overwrite SlideOut-usage.md."
    blocks: []
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

  - id: WARN-002
    dimension: usage_guidelines
    confidence: heuristic
    added: "2026-05-15"
    finding: >
      SlideOut-usage.md is editorial — drafted via usage-advisor Open mode on
      2026-05-15, not from a Figma `↳ SlideOut examples` page (which does not
      exist; see GAP-001). The 7 Do/Don't pairs are grounded in props.md,
      examples.md, and accessibility.md with explicit `**Source:** [file:line]`
      citations, but the anatomy and pair framings have not been validated
      against a Figma source-of-truth or designer review.
    advisory: "Treat the usage doc as a stand-in. If/when a Figma design and `↳ SlideOut examples` page are authored, run figma-extract-usage to overwrite SlideOut-usage.md with canonical card-frame data, and confirm whether each editorial pair survives, is restated, or is discarded."
# --- navigation (added by component-map) ---
role: audit
pipeline_stage: spec_ready
pipeline_note: "Audit verdict PARTIAL — doc-rewrite can run on 5 of 7 dimensions; usage is editorial (WARN-002); figma_fidelity still blocked by GAP-001."
siblings:
  - "[[SlideOut/props]]"
  - "[[SlideOut/examples]]"
  - "[[SlideOut/tokens]]"
  - "[[SlideOut/accessibility]]"
  - "[[SlideOut/SlideOut-usage]]"
tags:
  - oxygen
  - component/SlideOut
  - role/audit
  - stage/spec_ready
---

# SlideOut — Audit Report

> **Verdict: PARTIAL** — GAP-001 is a permanent blocker SOURCE_GAP: no Figma design exists for SlideOut. `figma_fidelity` cannot be completed without upstream design work.
>
> **Re-audited 2026-05-15:** GAP-002 (usage absent) closed editorially — `SlideOut-usage.md` was authored via `usage-advisor` Open mode with 7 grounded Do/Don't pairs (WARN-002). `doc-rewrite` can now proceed on 5 of 7 dimensions (props, examples, tokens, accessibility, usage). Resolve GAP-004 / GAP-005 (missing prop descriptions + `onResize`) and GAP-008 (tokens) from source before rewriting for best coverage.
>
> Rubric version: 1.0 · Re-audited: 2026-05-15 (prior audit: 2026-05-05)

## Summary

| Dimension | Score | Δ | Status |
|-----------|-------|---|--------|
| Props completeness | 0.45 | — | 9 props listed; 4 undescribed; `onResize` unregistered; all defaults missing |
| Examples quality | 0.40 | — | 1 Storybook-derived example; 0 clean MCP examples; limited coverage |
| Token coverage | 0.10 | — | 0 tokens from MCP; file present but empty of data |
| Accessibility | 0.50 | — | Full structure present but entirely inferred — no MCP source data |
| Figma fidelity | 0.00 | — | `SlideOut-figma.md` absent — no Figma design exists (GAP-001) |
| PUI integration | 0.50 | — | No PUI results found; no explicit N/A marker written |
| Usage guidelines | 0.55 | **+0.55** | ✅ Available — editorial; 7 grounded Do/Don't pairs, When-to-use / When-not-to-use, inferred Anatomy block; missing Figma verification (WARN-002) |
| **Overall** | **0.36** | **+0.08** | |

## Gap register

| ID | Dimension | Severity | Type | Summary |
|----|-----------|----------|------|---------|
| GAP-001 | figma_fidelity | blocker | SOURCE_GAP | No Figma design exists — SlideOut-figma.md cannot be produced |
| GAP-002 | usage_guidelines | major | SOURCE_GAP | ✅ Resolved editorially 2026-05-15 (see WARN-002) — `SlideOut-usage.md` authored via `usage-advisor` with 7 grounded Do/Don't pairs |
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
| WARN-002 | usage_guidelines | `SlideOut-usage.md` is editorial (drafted via `usage-advisor` 2026-05-15). Replace with `figma-extract-usage` output if a `↳ SlideOut examples` Figma page is ever authored |

## Resolution path

To unblock `doc-rewrite` on available dimensions (props, examples, tokens, accessibility, usage):

1. **GAP-004 + GAP-005 (props):** Check `@8x8/oxygen-slide-out` component source or Storybook argTypes for `hasAnimation`, `defaultWidth`, `minWidth`, `maxWidth` descriptions and confirm whether `onResize` is a public prop. Update props.md.
2. **GAP-008 (tokens):** Search token registry with alternate terms ('slide', 'panel', 'drawer') or inspect component CSS source. Update tokens.md.
3. **GAP-009 (accessibility):** Obtain confirmed ARIA/keyboard implementation from component source or Storybook a11y addon.
4. **GAP-003 (pui):** Write a minimal `SlideOut-pui.md` with the `<!-- NO RELEVANT PUI CONTEXT -->` marker to formally close this dimension.

**GAP-001 (Figma)** is permanently blocked until a Figma design is created. Flag to the design owner. **GAP-002 (Usage)** is closed editorially as of 2026-05-15 (WARN-002) — re-open and overwrite with `figma-extract-usage` output once a Figma examples page exists.

Minor gap (GAP-006) and warnings (WARN-001, WARN-002) are auto-fixable or advisory and do not block rewrite.

## Re-audit log

**2026-05-15** — Re-run after `SlideOut-usage.md` was added editorially.
- `file_inventory`: `SlideOut-usage.md` moved from `missing` → `present` (editorial).
- `usage_guidelines` dimension score: 0.00 → 0.55.
- `source_gaps` count: 8 → 7 (GAP-002 closed editorially).
- `warnings` count: 1 → 2 (added WARN-002 for editorial provenance).
- `overall_score`: 0.28 → 0.36.
- Verdict: PARTIAL → PARTIAL (unchanged; GAP-001 still a blocker SOURCE_GAP).
