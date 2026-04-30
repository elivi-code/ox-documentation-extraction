---
rubric_version: "1.0"
component: Checkbox
package: "@8x8/oxygen-checkbox"
audit_date: "2026-04-29"
auditor: doc-audit skill

file_inventory:
  present:
    - props.md
    - examples.md
    - tokens.md
    - accessibility.md
    - checkbox-figma.md
    - checkbox-pui.md
  missing:
    - checkbox-usage.md   # figma-extract-usage skill not run

dimension_scores:
  props_completeness:   { score: 0.90, coverage: "9/10" }
  examples_quality:     { score: 0.67, coverage: "6/9"  }
  token_coverage:       { score: 0.25, coverage: "2/8"  }
  accessibility:        { score: 0.80, coverage: "8/10" }
  figma_fidelity:       { score: 0.67, coverage: "6/9"  }
  pui_integration:      { score: 1.00, coverage: "4/4"  }   # resolved by NO RELEVANT PUI CONTEXT marker
  usage_guidelines:     { score: 0.00, coverage: "0/5"  }   # file missing entirely

overall_score: 0.64

counts:
  doc_gaps: 5
  source_gaps: 9
  conflicts: 0
  warnings: 3

verdict: PARTIAL
verdict_reason: >
  All core files present (props, examples, accessibility, figma, pui). Zero conflicts.
  No blocker-severity source gaps in present files. However checkbox-usage.md is entirely
  absent (major SOURCE_GAP) and token bindings are unavailable for any state/color (major
  SOURCE_GAP). doc-rewrite can proceed on Props, Examples, Accessibility, and PUI
  dimensions but Token and Usage Guidelines dimensions will produce stubs.

gaps:
  - id: GAP-001
    dimension: usage_guidelines
    severity: major
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: "(absent)"
      location: "component-lib/Checkbox/checkbox-usage.md"
      finding: "File does not exist. figma-extract-usage skill was not run."
    fix_action: "Run figma-extract-usage skill for Checkbox to extract Do/Don't guidelines from Figma."
    blocks: [docusaurus-usage-section, storybook-do-dont-panel]
    dependency: []

  - id: GAP-002
    dimension: token_coverage
    severity: major
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: tokens.md
      location: "## Color palette section, data gap notice"
      finding: >
        Zero checkbox-specific semantic color tokens returned by Oxygen MCP
        (search term 'checkbox' → 0 matches). Figma Variables API returned
        permission error. No border, background, checkmark, or hover color
        values are documented.
    fix_action: "Enable Figma Desktop Bridge; run figma_get_variables(namePattern='checkbox', resolveAliases=true). Or search Oxygen token source SCSS/JSON for 'checkbox' in the semantic layer."
    blocks: [theming-doc, dark-mode-section, token-table-in-spec]
    dependency: []

  - id: GAP-003
    dimension: token_coverage
    severity: major
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: tokens.md
      location: "## Color palette section"
      finding: >
        No typography tokens (font-size, line-height, font-weight) for the
        checkbox label text are documented. Oxygen MCP returned 0 token
        matches; Figma styles returned 0 results.
    fix_action: "Retrieve typography tokens via Figma Desktop Bridge or search Oxygen theme SCSS for label text style applied to Checkbox."
    blocks: [token-table-in-spec]
    dependency: []

  - id: GAP-004
    dimension: figma_fidelity
    severity: major
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: checkbox-figma.md
      location: "## 3. Color and token bindings — <!-- NOT FOUND IN FIGMA RESPONSE -->"
      finding: "Figma Variables API inaccessible (permissions error). No token-to-property bindings for any state or mode."
    fix_action: "Run Figma Desktop Bridge plugin; re-run figma_get_variables with resolveAliases=true and call get_design_context on node 51776:5160."
    blocks: [figma-spec-token-section, dark-mode-token-table]
    dependency: [GAP-002]

  - id: GAP-005
    dimension: figma_fidelity
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: checkbox-figma.md
      location: "## 4. Structure and spacing — 'Gap between input and label' note"
      finding: >
        Exact horizontal gap between checkbox input (20px) and label text
        is not measured. get_design_context failed (Figma Desktop required).
        The value is noted as unknown in checkbox-figma.md.
    fix_action: "Re-run get_design_context on node 51776:5160 with Figma Desktop connected to get auto-layout gap value."
    blocks: [spacing-spec-in-spec]
    dependency: []

  - id: GAP-006
    dimension: figma_fidelity
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: checkbox-figma.md
      location: "## 5. Figma annotations — <!-- NOT FOUND IN FIGMA RESPONSE -->"
      finding: "Component descriptions absent from Figma REST API response (known Figma API bug). No design intent annotations captured."
    fix_action: "Run Figma Desktop Bridge plugin to surface component descriptions; re-run figma_get_component with Desktop Bridge active."
    blocks: [design-intent-section]
    dependency: []

  - id: GAP-007
    dimension: examples_quality
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: examples.md
      location: "Data gap notice, line 5–8"
      finding: >
        Oxygen MCP returned 0 clean code examples (cleanExamples: true).
        All examples in examples.md are derived from prop definitions, not
        from verified Storybook source. The ControlledCheckbox wrapper
        pattern from Storybook is mentioned but not shown.
    fix_action: "Obtain clean examples from Storybook source (Checkbox.documentation.stories.tsx) or from Oxygen documentation site directly."
    blocks: [storybook-examples-section]
    dependency: []

  - id: GAP-008
    dimension: examples_quality
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: true
    evidence:
      source_file: examples.md
      location: "No CheckboxGroup error state example present"
      finding: >
        Figma confirms CheckboxGroup has an isError variant (with 'Error
        message goes here.' text slot visible in screenshot). No example
        showing CheckboxGroup with isError=True is present in examples.md.
    fix_action: "Add CheckboxGroup error state example to examples.md using isError prop (prop name inferred from Figma — verify against CheckboxGroup API)."
    blocks: [error-state-example-in-spec]
    dependency: []

  - id: GAP-009
    dimension: props_completeness
    severity: minor
    type: SOURCE_GAP
    confidence: heuristic
    auto_fixable: false
    evidence:
      source_file: props.md
      location: "## CheckboxGroup Props — only 1 prop listed"
      finding: >
        CheckboxGroup is documented with only isHorizontal (1 prop). The
        Figma component has header (BOOLEAN) and footer (BOOLEAN) slots, and
        isError (VARIANT). These are Figma-layer properties but may correspond
        to undocumented CheckboxGroup props not returned by the MCP. The MCP's
        get-component-props call returned only isHorizontal — completeness
        unverifiable without Storybook source or more detailed MCP data.
    fix_action: "Verify CheckboxGroup full prop list against Storybook argsConfig or package source. Add error prop, label prop, hint prop if they exist."
    blocks: [checkboxgroup-props-table-in-spec]
    dependency: []

  - id: GAP-010
    dimension: props_completeness
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: true
    evidence:
      source_file: props.md
      location: "Checkbox screenshot shows Beta badge on info card"
      finding: >
        The Figma screenshot shows a 'Beta' badge on the component info card.
        Beta status is not noted in props.md, examples.md, or any other file.
        Consumers should be aware the component API may change.
    fix_action: "Add Beta status notice to props.md near the component heading and installation section."
    blocks: [spec-stability-notice]
    dependency: []

  - id: GAP-011
    dimension: accessibility
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: true
    evidence:
      source_file: accessibility.md
      location: "## Nesting and group accessibility"
      finding: >
        The error state for CheckboxGroup (isError=True visible in Figma)
        is not addressed in accessibility.md. The error message text slot
        needs an aria-live region or aria-describedby pattern to be
        announced to screen readers.
    fix_action: "Add error state accessibility pattern to accessibility.md: aria-describedby linking CheckboxGroup to its error message; or aria-live='polite' on error container."
    blocks: [a11y-error-pattern-in-spec]
    dependency: []

  - id: GAP-012
    dimension: accessibility
    severity: minor
    type: DOC_GAP
    confidence: heuristic
    auto_fixable: true
    evidence:
      source_file: accessibility.md
      location: "## Nesting and group accessibility"
      finding: >
        accessibility.md recommends wrapping CheckboxGroup in a fieldset/
        legend but notes this 'should be handled' by the component — it is
        unverified. No Storybook rendered output was checked. This could
        be an assumption gap if CheckboxGroup does not emit a fieldset.
    fix_action: "Verify rendered CheckboxGroup DOM output for fieldset/legend presence. Update accessibility.md to reflect actual behavior (confirmed or absent)."
    blocks: [a11y-group-role-in-spec]
    dependency: []

  - id: GAP-013
    dimension: figma_fidelity
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: true
    evidence:
      source_file: checkbox-figma.md
      location: "## Screenshot section — info card description"
      finding: >
        The screenshot image tag in checkbox-figma.md has no src attribute
        (broken Markdown image: '![Checkbox...]' with no URL). The screenshot
        was captured but not saved as an asset file.
    fix_action: "Save the screenshot PNG to component-lib/Checkbox/img/checkbox-screenshot.png and update the image tag src."
    blocks: [visual-record-in-spec]
    dependency: []

warnings:
  - id: WARN-001
    dimension: examples_quality
    confidence: heuristic
    finding: >
      examples.md uses 'isChecked={...}' and 'onChange={...}' as placeholder
      props in the CheckboxGroup example. These are not runnable as-is.
      Downstream Storybook generation may need to substitute real state
      management patterns.
    advisory: "Replace placeholder props with concrete state hooks before publishing to Storybook."

  - id: WARN-002
    dimension: token_coverage
    confidence: heuristic
    finding: >
      tokens.md includes the full Oxygen color palette ramp as 'available'
      and speculatively assigns blue05/blue06 as the primary interactive
      color. This is unconfirmed and could mislead doc-rewrite.
    advisory: "Remove the speculative color assignment from tokens.md or clearly mark it as unverified inference."

  - id: WARN-003
    dimension: accessibility
    confidence: heuristic
    finding: >
      accessibility.md guidance is fully inferred from prop definitions and
      WAI-ARIA patterns — no Figma annotations or MCP accessibility data
      confirmed it. The content is likely correct but carries heuristic
      confidence only.
    advisory: "Validate accessibility.md content against the actual rendered component before publishing."
---

# Checkbox — Audit Report

> **Verdict: PARTIAL** — doc-rewrite can start on Props, Examples, Accessibility, and PUI dimensions.
> Token and Usage Guidelines dimensions will produce stubs until source gaps are resolved.
>
> Rubric version: 1.0 · Audited: 2026-04-29

---

## File inventory

| File | Status | Produced by |
|------|--------|-------------|
| `props.md` | ✅ Present | oxygen-mcp-extract |
| `examples.md` | ✅ Present | oxygen-mcp-extract |
| `tokens.md` | ✅ Present | oxygen-mcp-extract |
| `accessibility.md` | ✅ Present | oxygen-mcp-extract |
| `checkbox-figma.md` | ✅ Present | figma-extract |
| `checkbox-pui.md` | ✅ Present | pui-mcp-extract |
| `checkbox-usage.md` | ❌ **Missing** | figma-extract-usage (not run) |

---

## Dimension scores

| Dimension | Score | Coverage | Notes |
|-----------|------:|---------|-------|
| Props completeness | 0.90 | 9/10 | Strong; CheckboxGroup may have undocumented props |
| Examples quality | 0.67 | 6/9 | Present but all prop-derived; no MCP-verified Storybook snippets |
| Token coverage | 0.25 | 2/8 | Only 2 spacing tokens; all color/type tokens absent |
| Accessibility | 0.80 | 8/10 | Solid but fully inferred; error state a11y missing |
| Figma fidelity | 0.67 | 6/9 | Anatomy and variants complete; token bindings and design context absent |
| PUI integration | 1.00 | 4/4 | ✅ PASS — `NO RELEVANT PUI CONTEXT` confirmed |
| Usage guidelines | 0.00 | 0/5 | ❌ File missing entirely |
| **Overall** | **0.64** | **35/55** | |

---

## Gaps

### SOURCE_GAP — Major (must resolve before full spec)

**GAP-001** · Usage Guidelines
> `checkbox-usage.md` is absent — `figma-extract-usage` skill was not run.
> **Fix:** Run `figma-extract-usage` for Checkbox.
> **Blocks:** Docusaurus usage section, Storybook Do/Don't panel.

**GAP-002** · Token Coverage
> Zero checkbox-specific semantic color tokens from any source. No border, background, checkmark, or hover color values are documented.
> **Fix:** Enable Figma Desktop Bridge → `figma_get_variables(namePattern='checkbox', resolveAliases=true)`.
> **Blocks:** Theming doc, dark-mode section, token table in spec.

**GAP-003** · Token Coverage
> No typography tokens for checkbox label text (font-size, line-height, weight).
> **Fix:** Retrieve via Desktop Bridge or search Oxygen theme SCSS.
> **Blocks:** Token table in spec.

**GAP-004** · Figma Fidelity
> Token-to-property bindings unavailable (Figma Variables API permission error). No color resolved for any state or mode.
> **Fix:** Run Desktop Bridge; call `get_design_context` on node `51776:5160`.
> **Depends on:** GAP-002.

### SOURCE_GAP — Minor

**GAP-005** · Figma Fidelity
> Exact input-to-label horizontal gap unknown — `get_design_context` unavailable.
> **Fix:** Re-run `get_design_context` with Desktop Bridge connected.

**GAP-006** · Figma Fidelity
> Component descriptions absent (Figma API bug without Desktop Bridge).
> **Fix:** Run Figma Desktop Bridge plugin; retry `figma_get_component`.

**GAP-007** · Examples Quality
> MCP returned 0 clean Storybook snippets. All examples are prop-derived, not verified.
> **Fix:** Extract from `Checkbox.documentation.stories.tsx` or Oxygen docs site.

**GAP-009** · Props Completeness _(heuristic)_
> CheckboxGroup documented with only `isHorizontal` (1 prop). Figma shows header, footer, and isError slots — may correspond to undocumented props.
> **Fix:** Verify CheckboxGroup full API against Storybook argsConfig or package source.

### DOC_GAP — Minor (auto-fixable by doc-rewrite)

**GAP-008** · Examples Quality
> No CheckboxGroup error state example (`isError=True` visible in Figma).
> **Fix:** Add `CheckboxGroup` error state example to `examples.md`.

**GAP-010** · Props Completeness
> Beta status (visible on Figma info card) not noted in any file.
> **Fix:** Add Beta stability notice to `props.md`.

**GAP-011** · Accessibility
> CheckboxGroup `isError` state has no documented a11y pattern (aria-describedby / aria-live).
> **Fix:** Add error state accessibility pattern to `accessibility.md`.

**GAP-012** · Accessibility _(heuristic)_
> `fieldset`/`legend` in CheckboxGroup is assumed, not verified from rendered DOM.
> **Fix:** Verify rendered output; update `accessibility.md` to reflect actual behavior.

**GAP-013** · Figma Fidelity
> Screenshot image tag in `checkbox-figma.md` has no src (broken `![...]` with no URL).
> **Fix:** Save screenshot to `img/checkbox-screenshot.png`; update image tag.

---

## Conflicts

None — no conflicting information between sources.

---

## Warnings (heuristic, advisory only)

**WARN-001** · Examples Quality
> `CheckboxGroup` example uses `{...}` placeholders — not runnable as-is.
> Substitute concrete state management before Storybook publishing.

**WARN-002** · Token Coverage
> `tokens.md` speculatively assigns `blue05`/`blue06` as primary interactive color — unconfirmed.
> Remove or clearly mark as unverified before doc-rewrite consumes this file.

**WARN-003** · Accessibility
> All `accessibility.md` content is inferred from WAI-ARIA patterns, not from Figma or MCP annotations.
> Validate against actual rendered component before publishing.

---

## Suggested next actions

1. **Immediate (unblocks doc-rewrite):** Run `figma-extract-usage` skill for Checkbox to generate `checkbox-usage.md` (GAP-001).
2. **Before full spec:** Enable Figma Desktop Bridge → re-run `figma_get_variables` and `get_design_context` to populate GAP-002 through GAP-006.
3. **doc-rewrite can start now** on: Props, Examples (with stub warning), Accessibility, PUI dimensions.
4. **Token and Usage Guidelines** dimensions should be stubs with `<!-- PENDING: GAP-002, GAP-001 -->` markers until sources are resolved.

_Source: doc-audit skill v1.0 · Extracted from component-lib/Checkbox/ · 2026-04-29_
