---
rubric_version: "1.0"
component: Checkbox
package: "@8x8/oxygen-checkbox"
audit_date: "2026-05-12"
auditor: doc-audit skill
prior_audit: "2026-05-05"

file_inventory:
  present:
    - props.md
    - examples.md
    - tokens.md
    - accessibility.md
    - checkbox-figma.md
    - checkbox-pui.md
    - checkbox-usage.md   # NEW — editorial draft authored 2026-05-12
  missing: []

dimension_scores:
  props_completeness:   { score: 0.90, coverage: "9/10" }
  examples_quality:     { score: 0.67, coverage: "6/9"  }
  token_coverage:       { score: 0.62, coverage: "5/8"  }
  accessibility:        { score: 0.80, coverage: "8/10" }
  figma_fidelity:       { score: 0.78, coverage: "7/9"  }
  pui_integration:      { score: 1.00, coverage: "4/4"  }
  usage_guidelines:     { score: 0.80, coverage: "4/5"  }   # ▲ jumped from 0.00 — editorial draft present, mirrors docs page + derives Do/Don't pairs from intent; only deduction is "no Figma-sourced Do/Don't card frames"

overall_score: 0.80

counts:
  doc_gaps: 6
  source_gaps: 5
  conflicts: 0
  warnings: 2

verdict: YES
verdict_reason: >
  Zero CONFLICTs and zero blocker-severity gaps. The major usage_guidelines
  SOURCE_GAP from the prior audit (GAP-001) is now substantially addressed: an
  editorial checkbox-usage.md was authored 2026-05-12 from the published Oxygen
  docs page (https://oxygen.8x8.com/components/checkbox/usage, fetched via
  Claude_in_Chrome MCP) and cross-validated against the extracted MCP/Figma
  artifacts. Seven Do/Don't pairs are derived from the docs page Best Practices
  + Nesting intent + accessibility data. The remaining gap on this dimension is
  the absence of Figma-sourced Do/Don't card frames (no ↳ Checkbox examples page
  exists in Figma) — re-classified as a minor SOURCE_GAP awaiting Figma authoring.
  All other gaps are unchanged minor SOURCE_GAPs or auto-fixable DOC_GAPs from
  the prior audit. doc-rewrite can proceed on all dimensions.

gaps:
  - id: GAP-001
    dimension: usage_guidelines
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: "checkbox-usage.md (present, editorial)"
      location: "Pairs section (frontmatter pipeline_note + FIGMA EXAMPLES PAGE banner)"
      finding: >
        checkbox-usage.md is present as an editorial draft. No Figma ↳ Checkbox
        examples page with ✅ Do / ❌ Don't card frames exists, so the 7 Do/Don't
        pairs in the file are editorially derived from the docs page Best
        Practices + Nesting sections plus the extracted MCP/Figma artifacts —
        not from Figma card frames. This is documented in the file's
        pipeline_note frontmatter and the STATUS banner.
    fix_action: "If a Figma ↳ Checkbox examples page is ever created with Do/Don't card frames, run figma-extract-usage to replace the editorial draft. Until then, the editorial pairs are the canonical usage guidance."
    blocks: [] # no longer blocks docusaurus-usage-section or storybook-do-dont-panel — editorial content is consumable
    dependency: []

  - id: GAP-002
    dimension: token_coverage
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: true
    evidence:
      source_file: tokens.md
      location: "## Color palette section — speculative blue05/blue06 assignment (tokens.md:55)"
      finding: >
        tokens.md still contains speculative language about blue05/blue06 as the
        primary interactive colour. The actual resolved token is ui/ui22 →
        color/blue/blue05 (#0056e0 Light, #ccddf9 Dark). tokens.md should be
        updated to reflect the confirmed binding. Source data is in
        checkbox-figma.md §3 and checkbox-usage.md "Behaviour > States".
    fix_action: >
      Update tokens.md: replace speculative palette section with confirmed
      semantic tokens (ui/ui21, ui/ui22, interactive/disabled02,
      interactive/focus01, text/textColor01, error/error01) sourced from
      checkbox-figma.md §3. Remove WARN-002 speculative assignment.
    blocks: [token-table-in-spec]
    dependency: []

  - id: GAP-003
    dimension: token_coverage
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: checkbox-figma.md
      location: "## 3. Color and token bindings — Typography tokens section absent"
      finding: >
        No typography variable bindings were found on the Checkbox Input
        component set (confirmed via deep figma_execute scan — only 5
        color/focus variables bound). Label text typography is not bound at
        component level — likely inherited from theme. This is likely by design,
        not a gap in the component, but cannot be confirmed without checking
        the Oxygen theme layer.
    fix_action: "Verify in Oxygen theme SCSS whether Checkbox label inherits typography from a theme variable or is hardcoded. Document the mechanism in tokens.md."
    blocks: [token-table-in-spec]
    dependency: []

  - id: GAP-004
    dimension: figma_fidelity
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: checkbox-figma.md
      location: "## 4. Structure and spacing — Gap between input and label (checkbox-figma.md:178)"
      finding: >
        Exact horizontal gap between checkbox input (20px) and label text is not
        measured. get_design_context unavailable (Figma Desktop not connected at
        time of extraction). Value noted as unknown in checkbox-figma.md and
        called out in checkbox-usage.md Anatomy and Sizes sections.
    fix_action: "Re-run get_design_context on node 51776:5081 with Figma Desktop connected to get auto-layout gap value for input-to-label spacing."
    blocks: [spacing-spec-in-spec]
    dependency: []

  - id: GAP-005
    dimension: figma_fidelity
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: checkbox-figma.md
      location: "## 5. Figma annotations — <!-- NOT FOUND IN FIGMA RESPONSE -->"
      finding: "Component descriptions absent from Figma REST API response (known Figma API bug without Desktop Bridge)."
    fix_action: "Run Figma Desktop Bridge plugin; retry figma_get_component to surface component description/design intent."
    blocks: [design-intent-section]
    dependency: []

  - id: GAP-006
    dimension: examples_quality
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: examples.md
      location: "Data gap notice, lines 28-31"
      finding: >
        Oxygen MCP returned 0 clean code examples (cleanExamples: true). All
        examples are derived from prop definitions, not verified Storybook
        source. The ControlledCheckbox wrapper pattern from Storybook is
        mentioned but not shown. checkbox-usage.md uses prop-derived examples
        as a fallback.
    fix_action: "Obtain clean examples from Storybook source (Checkbox.documentation.stories.tsx) or from Oxygen documentation site."
    blocks: [storybook-examples-section]
    dependency: []

  - id: GAP-007
    dimension: examples_quality
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: true
    evidence:
      source_file: examples.md
      location: "No CheckboxGroup error state example present"
      finding: >
        Figma confirms CheckboxGroup has an isError variant. No example showing
        CheckboxGroup with isError=True is present in examples.md.
        checkbox-usage.md Pair 6 sketches an inline-error pattern but does not
        use a CheckboxGroup isError prop (which is not yet in the API — see
        GAP-008).
    fix_action: "Add CheckboxGroup error state example to examples.md using isError prop (verify prop name against CheckboxGroup API; see GAP-008)."
    blocks: [error-state-example-in-spec]
    dependency: [GAP-008]

  - id: GAP-008
    dimension: props_completeness
    severity: minor
    type: SOURCE_GAP
    confidence: heuristic
    auto_fixable: false
    evidence:
      source_file: props.md
      location: "## CheckboxGroup Props (props.md:72-78) — only 1 prop listed"
      finding: >
        CheckboxGroup documented with only isHorizontal (1 prop). Figma shows
        header, footer, and isError slots that may correspond to undocumented
        CheckboxGroup props not returned by the MCP. checkbox-usage.md surfaces
        this in the Beta-API banner and the Gaps table.
    fix_action: "Verify CheckboxGroup full prop list against Storybook argsConfig or package source. Add error, label, hint props if they exist."
    blocks: [checkboxgroup-props-table-in-spec]
    dependency: []

  - id: GAP-009
    dimension: props_completeness
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: true
    evidence:
      source_file: props.md
      location: "Checkbox screenshot shows Beta badge on info card"
      finding: >
        Beta status (visible on Figma info card) not noted in props.md.
        checkbox-usage.md surfaces the Beta notice in its banner, but the
        canonical home for stability state is props.md.
    fix_action: "Add Beta stability notice to props.md near the component heading."
    blocks: [spec-stability-notice]
    dependency: []

  - id: GAP-010
    dimension: accessibility
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: true
    evidence:
      source_file: accessibility.md
      location: "## Nesting and group accessibility"
      finding: >
        The isError state for CheckboxGroup has no documented a11y pattern
        (aria-describedby / aria-live) in accessibility.md. checkbox-usage.md
        Pair 6 sketches one (role="alert" on the inline error + aria-describedby
        on the submit button) but the canonical pattern is not yet captured in
        accessibility.md.
    fix_action: "Add error state accessibility pattern to accessibility.md: aria-describedby linking CheckboxGroup to its error message, or aria-live='polite' on error container. Reference the pattern sketched in checkbox-usage.md Pair 6."
    blocks: [a11y-error-pattern-in-spec]
    dependency: []

  - id: GAP-011
    dimension: accessibility
    severity: minor
    type: DOC_GAP
    confidence: heuristic
    auto_fixable: true
    evidence:
      source_file: accessibility.md
      location: "## Nesting and group accessibility (accessibility.md:86)"
      finding: >
        accessibility.md recommends fieldset/legend for CheckboxGroup but notes
        it 'should be handled' by the component — unverified. checkbox-usage.md
        Pair 5 also flags this as unverified.
    fix_action: "Verify rendered CheckboxGroup DOM output for fieldset/legend presence. Update accessibility.md and checkbox-usage.md to reflect actual behavior."
    blocks: [a11y-group-role-in-spec]
    dependency: []

warnings:
  - id: WARN-001
    dimension: examples_quality
    confidence: heuristic
    finding: >
      examples.md uses '{...}' placeholder props in CheckboxGroup example — not
      runnable as-is. checkbox-usage.md was authored to avoid this anti-pattern
      (all 7 pairs use named handlers).
    advisory: "Replace placeholder props in examples.md with concrete state hooks before publishing to Storybook."

  - id: WARN-002
    dimension: accessibility
    confidence: heuristic
    finding: >
      All accessibility.md content is inferred from WAI-ARIA patterns and prop
      definitions — no Figma annotations or MCP accessibility data confirmed it.
      Content is likely correct but carries heuristic confidence only.
      checkbox-usage.md mirrors accessibility.md and inherits the same caveat.
    advisory: "Validate accessibility.md content against the actual rendered component before publishing."
# --- navigation (added by component-map) ---
role: audit
pipeline_stage: spec_ready
pipeline_note: "Audit verdict YES — doc-rewrite can run; usage dimension now covered by editorial draft (2026-05-12)"
siblings:
  - "[[Checkbox/props]]"
  - "[[Checkbox/examples]]"
  - "[[Checkbox/tokens]]"
  - "[[Checkbox/accessibility]]"
  - "[[Checkbox/checkbox-figma]]"
  - "[[Checkbox/checkbox-pui]]"
  - "[[Checkbox/checkbox-usage]]"
tags:
  - oxygen
  - component/Checkbox
  - role/audit
  - stage/spec_ready
---

# Checkbox — Audit Report

> **Verdict: YES** — doc-rewrite can proceed on all dimensions.
> Usage dimension covered by editorial draft as of 2026-05-12; token bindings resolved 2026-05-05; remaining gaps are all minor or auto-fixable.
>
> Rubric version: 1.0 · Prior audit: 2026-05-05 · Re-audited: 2026-05-12

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
| `checkbox-usage.md` | ✅ **NEW** — editorial draft | editorial (docs-mirrored, 2026-05-12) |

---

## Dimension scores

| Dimension | Score | Coverage | Notes |
|-----------|------:|---------|-------|
| Props completeness | 0.90 | 9/10 | Strong; CheckboxGroup may have undocumented props |
| Examples quality | 0.67 | 6/9 | Present but prop-derived; no verified Storybook snippets |
| Token coverage | 0.62 | 5/8 | 4 color/state tokens confirmed in checkbox-figma.md; tokens.md still needs updating (DOC_GAP GAP-002) |
| Accessibility | 0.80 | 8/10 | Solid but fully inferred; error state a11y pattern still missing |
| Figma fidelity | 0.78 | 7/9 | Color/token bindings resolved 2026-05-05 |
| PUI integration | 1.00 | 4/4 | ✅ PASS — `NO RELEVANT PUI CONTEXT` confirmed |
| Usage guidelines | 0.80 | 4/5 | ▲ **Jumped from 0.00** — editorial draft present, mirrors docs page + 7 derived Do/Don't pairs; only deduction is "no Figma-sourced Do/Don't card frames" |
| **Overall** | **0.80** | **43/55** | ▲ up from 0.68 |

---

## Resolved since prior audit (2026-05-05)

| Was | Resolution |
|-----|-----------|
| GAP-001 (major SOURCE_GAP): checkbox-usage.md missing entirely | **Substantially resolved** — editorial checkbox-usage.md authored 2026-05-12 from published Oxygen docs page + extracted MCP/Figma artifacts. 7 Do/Don't pairs derived from docs page intent. Gap downgraded to minor SOURCE_GAP (no Figma ↳ Checkbox examples page exists) and no longer blocks docusaurus/storybook downstreams. |

---

## Gaps

### SOURCE_GAP — Minor

**GAP-001** · Usage Guidelines _(downgraded — was major)_
> `checkbox-usage.md` is present as an editorial draft. Do/Don't pairs are derived from the published Oxygen docs page (Variants + Nesting + Best Practices) plus the extracted MCP/Figma data — not from Figma Do/Don't card frames (no `↳ Checkbox examples` page exists in Figma).
> **Fix:** If a Figma `↳ Checkbox examples` page is created with Do/Don't card frames, run `figma-extract-usage` to replace the editorial draft.

**GAP-003** · Token Coverage
> No typography variable bindings found at component level (confirmed via deep `figma_execute` scan). May be theme-inherited.
> **Fix:** Verify in Oxygen theme SCSS whether label typography is hardcoded or inherited. Document in `tokens.md`.

**GAP-004** · Figma Fidelity
> Exact input-to-label horizontal gap unknown — `get_design_context` unavailable.
> **Fix:** Re-run `get_design_context` on node `51776:5081` with Figma Desktop connected.

**GAP-005** · Figma Fidelity
> Component descriptions absent (Figma API bug without Desktop Bridge).
> **Fix:** Run Figma Desktop Bridge; retry `figma_get_component`.

**GAP-006** · Examples Quality
> MCP returned 0 clean Storybook snippets. All examples are prop-derived.
> **Fix:** Extract from `Checkbox.documentation.stories.tsx` or Oxygen docs site.

**GAP-008** · Props Completeness _(heuristic)_
> CheckboxGroup documented with only `isHorizontal`. Figma shows header/footer/isError slots.
> **Fix:** Verify CheckboxGroup full API against Storybook argsConfig.

### DOC_GAP — Minor (auto-fixable by doc-rewrite)

**GAP-002** · Token Coverage
> `tokens.md` still has speculative blue05/blue06 language. Actual token is `ui/ui22` → #0056e0. Source data in `checkbox-figma.md §3` and `checkbox-usage.md` Behaviour table.
> **Fix:** Update `tokens.md` with confirmed semantic tokens from `checkbox-figma.md`.

**GAP-007** · Examples Quality
> No CheckboxGroup `isError` state example.
> **Fix:** Add error state example to `examples.md` (depends on GAP-008 — confirm `isError` is a real API prop).

**GAP-009** · Props Completeness
> Beta status not noted in `props.md` (only surfaced in `checkbox-usage.md` banner).
> **Fix:** Add Beta notice to `props.md`.

**GAP-010** · Accessibility
> CheckboxGroup error state has no a11y pattern in `accessibility.md`. `checkbox-usage.md` Pair 6 sketches one — promote to `accessibility.md`.
> **Fix:** Add error state accessibility pattern to `accessibility.md`.

**GAP-011** · Accessibility _(heuristic)_
> `fieldset`/`legend` in CheckboxGroup assumed, not verified.
> **Fix:** Verify rendered DOM; update `accessibility.md` and `checkbox-usage.md` Pair 5.

---

## Conflicts

None.

---

## Warnings (heuristic, advisory only)

**WARN-001** · Examples Quality
> `examples.md` CheckboxGroup example uses `{...}` placeholders — not runnable as-is. `checkbox-usage.md` was authored to avoid this anti-pattern (all 7 pairs use named handlers).

**WARN-002** · Accessibility
> All `accessibility.md` content is inferred, not confirmed from Figma or MCP annotations. `checkbox-usage.md` mirrors `accessibility.md` and inherits the same caveat.

---

## Suggested next actions

1. **doc-rewrite can run now** — zero CONFLICTs, zero blockers. All seven dimensions have source data.
2. **tokens.md update (GAP-002):** doc-rewrite should pull confirmed color tokens from `checkbox-figma.md §3` and `checkbox-usage.md` Behaviour table into the tokens table.
3. **Optional enrichment:** Verify `CheckboxGroup` full API (GAP-008); confirm `fieldset`/`legend` auto-wrapping (GAP-011); add Beta notice to `props.md` (GAP-009).
4. **If Figma authors create a `↳ Checkbox examples` page** with Do/Don't card frames, run `figma-extract-usage Checkbox` and replace the editorial draft (GAP-001).

_Source: doc-audit skill v1.0 · Re-audited from component-lib/Checkbox/ · 2026-05-12_
