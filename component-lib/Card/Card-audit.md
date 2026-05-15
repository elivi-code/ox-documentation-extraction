---
rubric_version: "1.0"
component: Card
package: "@8x8/oxygen-card"
audit_date: "2026-05-05"
auditor: doc-audit skill
updated: "2026-05-05"
deprecated: true

file_inventory:
  present:
    - props.md
    - examples.md
    - tokens.md
    - accessibility.md
    - Card-figma.md
    - figma-screenshot-Card.png
    - figma-screenshot-Card-examples.png
  missing:
    - Card-usage.md
    - Card-pui.md

dimension_scores:
  props_completeness:   { score: 0.70, coverage: "11 props across 4 sub-components (Card, Header, Separator, Statistics); all documented with types, required flags, defaults; deprecation banner present; StatisticsItemData type body absent; CardTheme/StatisticsTheme shapes unknown" }
  examples_quality:     { score: 0.45, coverage: "3 code examples (basic, separator, statistics) — all derived from Storybook doc story; MCP get-component-examples returned 0 clean snippets; Statistics example uses placeholder type; usage guidance from MCP present" }
  token_coverage:       { score: 0.50, coverage: "3 global tokens (ui01/02/03) documented for light+dark with palette references; rest/focus background fill token (variable 20136:267 = #FFFFFF light / #171719 dark) unmatched to named token; CardTheme/StatisticsTheme interface shapes unknown" }
  accessibility:        { score: 0.50, coverage: "Full structure present — ARIA roles per sub-component, keyboard interaction table, screen reader guidance, WCAG 2.1 AA checklist; entirely inferred from component nature; no confirmed data from MCP or Figma annotations" }
  figma_fidelity:       { score: 0.65, coverage: "Card-figma.md present; component set, 6 variants (Mode×State), all properties, color bindings documented; token variable IDs opaque; padding/auto-layout data missing; dark hover fill not captured; typography tokens absent; component description unavailable (REST API bug)" }
  pui_integration:      { score: 0.40, coverage: "Card-pui.md absent; Platform UI MCP search returned 0 results for 'card'; no N/A marker written to formally confirm no PUI concern" }
  usage_guidelines:     { score: 0.00, coverage: "Card-usage.md absent; Figma examples page (49372:112) contains only one freeform 'Contact card' wireframe — no ✅ Do / ❌ Don't template frames present" }

overall_score: 0.46

counts:
  doc_gaps: 1
  source_gaps: 11
  conflicts: 0
  warnings: 2

verdict: "YES"
verdict_reason: >
  All four blocker-severity files are present (props.md, examples.md,
  accessibility.md, Card-figma.md). Zero CONFLICTs exist. No blocker-severity
  gaps were identified — all gaps are major or minor SOURCE_GAPs. doc-rewrite
  can proceed across all 7 dimensions; gaps will propagate to the spec as
  explicit SOURCE_GAP notes. The deprecation status of the component
  (confirmed by MCP: deprecated:true) must be the primary feature of the
  resulting spec — the rewrite should open with a prominent deprecation
  banner and include migration guidance if a replacement is identified.
  Recommend resolving GAP-006 (token semantic names via Desktop Bridge) and
  GAP-007 (spacing via get_design_context) before rewrite if possible, as
  these are the highest-value resolvable source gaps.

gaps:
  - id: GAP-001
    dimension: usage_guidelines
    severity: major
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: "(file absent)"
      location: "Card-usage.md — not present in directory"
      finding: >
        Card-usage.md does not exist. The Figma examples page (node 49372:112,
        "↳ Card examples") was fully traversed via the Desktop Bridge and found
        to contain only one frame named "Contact card" — a freeform wireframe
        mockup with no ✅ Do / ❌ Don't structural frames. The usage guidelines
        template has never been filled in for this component.
    fix_action: "Designer must populate the ↳ Card examples Figma page with ✅ Do / ❌ Don't template frames. Once complete, re-run figma-extract-usage to produce Card-usage.md."
    blocks: [doc-rewrite-usage-dimension]
    dependency: []

  - id: GAP-002
    dimension: pui_integration
    severity: major
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: true
    evidence:
      source_file: "(file absent)"
      location: "Card-pui.md — not present in directory"
      finding: >
        Card-pui.md does not exist. Platform UI MCP search returned 0 results
        for "card" (only a false positive from a logging package mentioning
        "discard"). No PUI application-layer concerns exist for this component,
        but this conclusion has not been formally recorded in a file.
    fix_action: "Write a minimal Card-pui.md containing only the '<!-- NO RELEVANT PUI CONTEXT -->' marker to formally confirm that no PUI integration concerns exist for Card."
    blocks: []
    dependency: []

  - id: GAP-003
    dimension: props_completeness
    severity: major
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: props.md
      location: "Card.Statistics section — data prop type; line 80 DOC_GAP note"
      finding: >
        The `data` prop of `Card.Statistics` has type `StatisticsItemData[]`,
        but the MCP description for this type ends with "where `StatisticsItemData`
        is:" and includes no type body. The shape of each array item (required
        fields, optional fields, field types) is entirely unknown. Consumers
        cannot use `Card.Statistics` without this information.
    fix_action: "Locate the StatisticsItemData type definition in the @8x8/oxygen-card package source (TypeScript types or JSDoc). Add the interface definition to props.md under Card.Statistics."
    blocks: [doc-rewrite, examples.md Statistics example]
    dependency: []

  - id: GAP-004
    dimension: props_completeness
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: props.md
      location: "theme prop row — all four sub-components"
      finding: >
        `Card`, `Card.Header`, and `Card.Separator` accept `theme: Partial<CardTheme>`;
        `Card.Statistics` accepts `theme: Partial<StatisticsTheme>`. Neither
        `CardTheme` nor `StatisticsTheme` interface shapes were returned by the
        MCP. Consumers cannot know which CSS properties are themeable.
    fix_action: "Locate CardTheme and StatisticsTheme interface definitions in the @8x8/oxygen-card source. Document the available theme keys in props.md and tokens.md."
    blocks: []
    dependency: []

  - id: GAP-005
    dimension: token_coverage
    severity: major
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: tokens.md
      location: "Theme Tokens section; corroborated by Card-figma.md Color & token bindings tables"
      finding: >
        The Rest and Focus background fill (Figma variable ID `20136:267`) resolves
        to #FFFFFF in Light mode and #171719 in Dark mode. These values do not
        match any of the three ui0x tokens returned by the MCP (ui01=#EBEAE1,
        ui02=#F4F3EE, ui03=#ABA999). The semantic token name for the card's
        default background surface is unknown. tokens.md does not document this
        token.
    fix_action: "Resolve variable ID 20136:267 to its semantic name using the Figma Desktop Bridge (figma_execute + figma.variables.getVariableByIdAsync) or the Variables REST API. Add the token to tokens.md."
    blocks: [doc-rewrite]
    dependency: []

  - id: GAP-006
    dimension: figma_fidelity
    severity: major
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: Card-figma.md
      location: "Color & token bindings section — SOURCE_GAP note; variable IDs 20136:253, 20136:263, 20136:267"
      finding: >
        All three token variable IDs extracted from Figma are opaque (20136:253,
        20136:263, 20136:267). The Variables REST API returned 403 (Enterprise
        plan required). Semantic token names were inferred by matching resolved
        hex values against MCP ui0x token descriptions, but these mappings are
        unconfirmed. Two of the three IDs (ui01 border, ui02 hover fill) match
        by value; one (rest fill) does not match any known token.
    fix_action: "Run figma_execute with figma.variables.getVariableByIdAsync for IDs 20136:253, 20136:263, 20136:267 in the Figma Desktop Bridge to obtain confirmed semantic token names. Update Card-figma.md and tokens.md."
    blocks: [doc-rewrite]
    dependency: []

  - id: GAP-007
    dimension: figma_fidelity
    severity: major
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: Card-figma.md
      location: "Structure & spacing — Internal spacing section; '<!-- NO STRUCTURE DATA FOUND -->'"
      finding: >
        Padding (horizontal and vertical), gap between child elements, and
        auto-layout direction for the Card container were not returned by the
        REST API calls. The `get_design_context` call failed because no node
        was selected in Figma Desktop at extraction time. Card dimensions (352×226)
        and Header dimensions (320×22) were captured, but internal spacing values
        are unknown.
    fix_action: "With Figma Desktop open on the Card component set, call get_design_context (fileKey: 5YihJ5WuDvnvrlrRMC4sBp, nodeId: 18080:28136 for Light/Rest variant) to retrieve padding, gap, and auto-layout data. Update Card-figma.md Structure & spacing section."
    blocks: [doc-rewrite]
    dependency: []

  - id: GAP-008
    dimension: figma_fidelity
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: Card-figma.md
      location: "Color & token bindings — Card container Dark mode table"
      finding: >
        Dark mode Hover and Focus variants (nodes 18080:30021, 18080:30158) were
        not fetched. The Dark/Hover fill token and Dark/Focus fill token are absent
        from the color bindings tables. Only Dark/Rest was captured (#171719 fill,
        #666666 border).
    fix_action: "Call figma_get_component for nodes 18080:30021 (Dark/Hover) and 18080:30158 (Dark/Focus) to capture their fill token IDs. Update Card-figma.md Dark mode table."
    blocks: []
    dependency: []

  - id: GAP-009
    dimension: figma_fidelity
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: Card-figma.md
      location: "Color & token bindings — Text styles section; '<!-- NO TOKEN BINDINGS FOUND IN FIGMA RESPONSE -->'"
      finding: >
        The `Widget Name` text node (18080:28139) inside the Header frame returned
        no `boundVariables` for typography. Text style name, font size, weight,
        and line height are unavailable. This affects the Typography section of
        the eventual spec.
    fix_action: "Inspect text node 18080:28139 via figma_execute to retrieve its textStyleId or boundVariables for font properties. Update Card-figma.md Text styles section."
    blocks: []
    dependency: []

  - id: GAP-010
    dimension: figma_fidelity
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: Card-figma.md
      location: "Design decisions & annotations section; '<!-- NO ANNOTATIONS FOUND IN FIGMA RESPONSE -->'"
      finding: >
        The component description could not be retrieved because of a known Figma
        REST API bug where description fields are missing from responses. The
        Desktop Bridge plugin provides reliable description data; it was not running
        during extraction.
    fix_action: "With Desktop Bridge running, call figma_get_component (nodeId: 18077:30676) — the enriched REST API warning will resolve and the description field will be populated. Update Card-figma.md Design decisions section."
    blocks: []
    dependency: []

  - id: GAP-011
    dimension: accessibility
    severity: major
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: accessibility.md
      location: "ARIA Roles & Semantics table — all rows; Figma has no annotations"
      finding: >
        The entire accessibility.md is inferred from the component's semantic
        nature as a layout container. No ARIA role, keyboard interaction, or
        focus management behaviour is confirmed from the MCP source, component
        TypeScript, or Figma annotations. Specific unknowns: whether Card renders
        as a native semantic element or a div; whether focus ring is implemented
        in CSS or via the Focus ring sub-instance; exact aria-level default
        confirmed in source.
    fix_action: "Verify ARIA role and keyboard behaviour from @8x8/oxygen-card component source or Storybook a11y addon output. Confirm: (1) root element type, (2) aria-level default for Header, (3) whether Focus ring is the Card's own implementation or the consumer's. Replace inferred content with confirmed data."
    blocks: [doc-rewrite]
    dependency: []

  - id: GAP-012
    dimension: examples_quality
    severity: major
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: examples.md
      location: "Card with Statistics example — data prop uses placeholder comment"
      finding: >
        `get-component-examples` with cleanExamples:true returned 0 results for
        the card package. The three examples in examples.md were derived from
        the Storybook documentation story. The Statistics example uses
        `data={[/* StatisticsItemData[] */]}` because the type shape is unknown
        (GAP-003). No examples cover: themed card, clickable card pattern,
        custom icon selection, or Show actions/Show icon toggle usage.
    fix_action: "Blocked by GAP-003 for Statistics. For remaining patterns, obtain confirmed usage examples from Storybook stories. Add examples for: (1) clickable card wrapping in <a>, (2) Show actions=false variant, (3) custom icon via Select Light icon prop."
    blocks: []
    dependency: [GAP-003]

warnings:
  - id: WARN-001
    dimension: props_completeness
    confidence: heuristic
    finding: >
      The `theme` prop is documented on all four sub-components but its interface
      shape is unknown (GAP-004). doc-rewrite cannot describe theming capability
      beyond acknowledging the prop exists. If CardTheme/StatisticsTheme shapes
      are not resolved before rewrite, the spec's theming section will be a
      stub. Consider whether documenting an undocumented theme API is useful
      for a deprecated component.
    advisory: "Decide whether to resolve GAP-004 or explicitly note in the spec that the theme prop interface is not publicly documented."

  - id: WARN-002
    dimension: component_lifecycle
    confidence: heuristic
    finding: >
      `@8x8/oxygen-card` is confirmed deprecated (MCP: deprecated:true). No
      replacement component or migration path is specified anywhere in the
      extracted documentation or Figma files. doc-rewrite will produce a spec
      with a deprecation banner but no migration guidance. Consumers encountering
      the deprecation warning have no direction on what to use instead.
    advisory: "Before running doc-rewrite, determine if there is a recommended replacement (e.g. a newer card pattern, or guidance to build layout compositions directly). Add the replacement to the spec's deprecation section."
# --- navigation (added by component-map) ---
role: audit
pipeline_stage: spec_ready
pipeline_note: "Audit verdict YES/PARTIAL — doc-rewrite can run"
siblings:
  - "[[Card/props]]"
  - "[[Card/examples]]"
  - "[[Card/tokens]]"
  - "[[Card/accessibility]]"
  - "[[Card/Card-figma]]"
tags:
  - oxygen
  - component/Card
  - role/audit
  - stage/spec_ready
---

# Card — Audit Report

> **Verdict: YES** — All required files present; zero CONFLICTs; zero blocker-severity gaps. `doc-rewrite` can proceed across all 7 dimensions. Gaps will surface as SOURCE_GAP notes in the spec. Strongly recommend resolving GAP-006 (token semantic names) and GAP-007 (spacing) via Desktop Bridge before rewrite, as these are the highest-value resolvable gaps. Component is confirmed **deprecated** — spec must open with a prominent deprecation banner.

## Summary

| Dimension | Score | Status |
|-----------|-------|--------|
| Props completeness | 0.70 | 11 props across 4 sub-components; StatisticsItemData type body missing; theme shapes unknown |
| Examples quality | 0.45 | 3 Storybook-derived examples; 0 clean MCP examples; Statistics placeholder; no advanced patterns |
| Token coverage | 0.50 | ui01/02/03 documented; rest fill token unmatched; theme interface shapes unknown |
| Accessibility | 0.50 | Full structure present; entirely inferred — no confirmed source data |
| Figma fidelity | 0.65 | File present; variants/properties/bindings documented; token IDs opaque; spacing missing |
| PUI integration | 0.40 | No PUI concerns found; no N/A marker written (auto-fixable) |
| Usage guidelines | 0.00 | File absent; Figma examples page has no Do/Don't template frames |
| **Overall** | **0.46** | |

## Gap register

| ID | Dimension | Severity | Type | Auto-fixable | Summary |
|----|-----------|----------|------|:------------:|---------|
| GAP-001 | usage_guidelines | major | SOURCE_GAP | No | Card-usage.md absent — Figma examples page has no Do/Don't frames |
| GAP-002 | pui_integration | major | DOC_GAP | **Yes** | Card-pui.md absent — write N/A marker file to close dimension |
| GAP-003 | props_completeness | major | SOURCE_GAP | No | StatisticsItemData type body unavailable from MCP |
| GAP-004 | props_completeness | minor | SOURCE_GAP | No | CardTheme / StatisticsTheme interface shapes unknown |
| GAP-005 | token_coverage | major | SOURCE_GAP | No | Rest/Focus background fill token (var 20136:267) unmatched to named token |
| GAP-006 | figma_fidelity | major | SOURCE_GAP | No | Token variable IDs opaque — semantic names need Desktop Bridge/Variables API |
| GAP-007 | figma_fidelity | major | SOURCE_GAP | No | Padding, gap, auto-layout direction unavailable — get_design_context failed |
| GAP-008 | figma_fidelity | minor | SOURCE_GAP | No | Dark mode Hover/Focus fill tokens not captured |
| GAP-009 | figma_fidelity | minor | SOURCE_GAP | No | Typography token bindings unavailable for Header text node |
| GAP-010 | figma_fidelity | minor | SOURCE_GAP | No | Component description unavailable (Figma REST API bug) |
| GAP-011 | accessibility | major | SOURCE_GAP | No | All a11y content inferred — no confirmed ARIA or keyboard data |
| GAP-012 | examples_quality | major | SOURCE_GAP | No | 0 clean MCP examples; Statistics example has placeholder type |

## Warnings

| ID | Dimension | Advisory |
|----|-----------|---------|
| WARN-001 | props_completeness | Decide whether to resolve theme interface shapes (GAP-004) or note them as undocumented in the spec |
| WARN-002 | component_lifecycle | Component is deprecated with no stated replacement — spec must include migration guidance or explicitly flag the absence of one |

## Resolution path

### Before doc-rewrite (recommended)

1. **GAP-002 (auto-fixable):** Write `Card-pui.md` with the `<!-- NO RELEVANT PUI CONTEXT -->` marker. Closes the pui_integration dimension entirely.
2. **GAP-006 + GAP-005 (token names):** With Desktop Bridge running, call `figma_execute` with `figma.variables.getVariableByIdAsync("VariableID:.../20136:267")` etc. to resolve all three variable IDs to semantic names. Update `Card-figma.md` and `tokens.md`.
3. **GAP-007 (spacing):** With Figma Desktop open, call `get_design_context` for node `18080:28136` (Light/Rest variant) to retrieve padding, gap, and auto-layout direction.

### Can resolve from source code

4. **GAP-003 + GAP-012:** Locate `StatisticsItemData` type in `@8x8/oxygen-card` package source. Fixes props.md and unblocks the Statistics example.
5. **GAP-011 (accessibility):** Check component source or Storybook a11y addon to confirm root element type, Header aria-level default, and Focus ring implementation.

### Designer action required

6. **GAP-001 (usage guidelines):** Notify design owner — the `↳ Card examples` Figma page needs ✅ Do / ❌ Don't template frames added. Then re-run `figma-extract-usage`.

### Acceptable as-is for deprecated component

7. **GAP-004, GAP-008, GAP-009, GAP-010** (minor) — resolution effort may not be warranted for a deprecated component. Flag in spec as known limitations.
