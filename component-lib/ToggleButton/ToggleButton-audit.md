---
rubric_version: "1.0"
component: ToggleButton
audit_date: "2026-04-29"
auditor: doc-audit skill

files_found:
  - props.md
  - examples.md
  - tokens.md
  - accessibility.md
  - ToggleButton-figma.md
  - ToggleButton-pui.md

files_missing: []

# 2026-05-15: ToggleButton-usage.md added as editorial draft (see GAP-003 status: partial-resolved-editorial)

dimension_scores:
  props:        { score: 0.83, coverage: "10/12" }
  examples:     { score: 0.80, coverage: "8/10" }
  tokens:       { score: 0.80, coverage: "8/10" }
  accessibility: { score: 0.88, coverage: "7/8"  }
  figma:        { score: 0.78, coverage: "7/9 — ⛔ 2 CONFLICTs" }
  usage:        { score: 0.70, coverage: "editorial draft present — Figma cards still missing" }
  pui:          { score: 1.00, coverage: "resolved — NO RELEVANT PUI CONTEXT" }

available_dimensions_avg: 0.85
overall_avg: 0.82

counts:
  doc_gaps: 4
  source_gaps: 5             # GAP-003 downgraded to partial-resolved-editorial but still counted as a SOURCE_GAP for Figma cards
  conflicts: 2
  warnings: 2

verdict: "NO"
verdict_reason: >
  2 CONFLICTs found — verdict is NO regardless of other scores.
  CONFLICT-001 (minor): Figma names the checked state property `isOn?`; OX prop is `isChecked`.
  The mapping is clear but the discrepancy is undocumented and will confuse doc-rewrite.
  CONFLICT-002 (major): Figma ToggleGroup component has an `isError` variant with a full
  InlineValidationMessage treatment. OX ToggleButtonGroup has no `isError` prop — the feature
  exists in the design spec but has no corresponding API. Requires designer/developer
  confirmation: is this intentional (consumers compose error handling manually) or a missing
  prop in the OX implementation?

suggested_next_action: >
  1. Resolve GAP-001 (naming map): add an explicit isOn?↔isChecked mapping note to
     ToggleButton-figma.md Persistent States table — one-liner fix.
  2. Resolve GAP-002 (isError conflict): confirm with designer/developer whether
     ToggleButtonGroup should expose an isError prop. If yes, it is missing from the
     OX implementation and props.md. If no, document the intended consumer-composition
     pattern in examples.md.
  3. Run figma-extract-usage → produces ToggleButton-usage.md.
  4. Re-run doc-audit → verdict should reach YES or PARTIAL.
  5. Run doc-rewrite → produces ToggleButton-spec.md.

gaps:
  - id: GAP-001
    dimension: figma
    severity: minor
    type: CONFLICT
    confidence: deterministic
    auto_fixable: true
    evidence:
      source_file: ToggleButton-figma.md
      location: "## API — Component properties / Persistent states table"
      finding: >
        Figma property for the checked state is `isOn?` (values: false/true).
        OX prop is `isChecked` (bool). The Persistent States table in figma.md
        documents both names side-by-side, which is correct, but the mapping is
        not called out as a naming divergence in the Gaps section header —
        doc-rewrite will need an explicit note to avoid silently using the wrong
        name in generated output.
    fix_action: "Add an explicit note in ToggleButton-figma.md Persistent States table: 'Figma isOn? maps to OX isChecked — same concept, different names'"
    blocks: [doc-rewrite/figma-dimension]
    dependency: []

  - id: GAP-002
    dimension: figma
    severity: major
    type: CONFLICT
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: ToggleButton-figma.md
      location: "## API — Component properties / Persistent states — Error (group), isError=True"
      finding: >
        Figma ToggleGroup component set has a dedicated `isError` variant axis (False/True).
        When `isError=True`, the footer slot renders an InlineValidationMessage with an
        error icon and red error text using `--error/error01`. OX `ToggleButtonGroup`
        (from get-component-info and get-component-props) exposes only `isHorizontal`
        and `children` — no `isError` prop. The design specifies error-state behaviour
        that the API does not support.
    fix_action: >
      Confirm with developer/designer: (a) ToggleButtonGroup should expose an isError
      prop — add to props.md and flag as implementation gap; OR (b) consumers are expected
      to compose error handling manually below the group — document the pattern in examples.md.
    blocks: [doc-rewrite/props-dimension, doc-rewrite/examples-dimension, docusaurus-generate]
    dependency: []

  - id: GAP-003
    dimension: usage
    severity: minor              # downgraded 2026-05-15: editorial usage now present
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    status: partial-resolved-editorial
    resolved_date: 2026-05-15
    evidence:
      source_file: ToggleButton-usage.md
      location: "component-lib/ToggleButton/ToggleButton-usage.md"
      finding: >
        ToggleButton-usage.md is now present as an editorial draft (drafted 2026-05-15 from
        the Oxygen web docs at oxygen.8x8.com/components/toggle/usage combined with the
        extracted MCP/Figma artifacts in this folder). Upstream Figma source still missing:
        the Toggle examples page (node 50606:95349) contains no `✅ Do — …` / `❌ Don't — …`
        card frames, so figma-extract-usage cannot run.
        Replace ToggleButton-usage.md wholesale with figma-extract-usage output once cards
        are authored.
    fix_action: "Author Do/Don't card frames on Figma examples page 50606:95349, then run figma-extract-usage ToggleButton to replace the editorial draft."
    blocks: []                   # no longer blocks doc-rewrite — editorial usage covers the dimension
    dependency: []

  - id: GAP-004
    dimension: figma
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: ToggleButton-figma.md
      location: "## API — Component properties / Token coverage"
      finding: >
        figma_get_component_details failed (Desktop Bridge not running). Component keys
        for all three component sets (Toggle Input, Toggle, Toggle Group) were not retrieved.
        These keys are needed for programmatic component instantiation in downstream tooling.
    fix_action: "Open Figma Desktop, enable Desktop Bridge plugin, re-run figma_get_component_details for nodes 51776:7539, 51776:7580, 52689:99119"
    blocks: [storybook-generate]
    dependency: []

  - id: GAP-005
    dimension: figma
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: ToggleButton-figma.md
      location: "## Color & token bindings"
      finding: >
        figma_get_variables failed (Enterprise plan or Desktop Bridge required). Token
        bindings in tokens.md are inferred from Figma CSS export output, not verified
        from the Figma Variables API. Alias chain (e.g. whether --ui/ui33 resolves via
        a collection alias) is unconfirmed.
    fix_action: "Enable Desktop Bridge or obtain Enterprise API access; re-run figma_get_variables with resolveAliases=true against file 5YihJ5WuDvnvrlrRMC4sBp"
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
      location: "## ToggleButton props — value row"
      finding: >
        `value` prop type is documented as `number | string | bool | { id: string }`
        (cleaned from MCP HTML). The shape variant `{ id: string }` has no usage
        documentation — when would a consumer pass an object with an id field?
        No example covers this case.
    fix_action: "Add a note or example showing when value={id: '...'} is appropriate — likely for identifying items in a group by ID"
    blocks: []
    dependency: []

  - id: GAP-007
    dimension: props
    severity: minor
    type: DOC_GAP
    confidence: heuristic
    auto_fixable: false
    evidence:
      source_file: props.md
      location: "## Package exports"
      finding: >
        Toggle Input (switch-only, 40×24px) appears as a separate Figma component set
        with its own variant structure. props.md does not clarify whether Toggle Input
        is individually importable from @8x8/oxygen-toggle-button, or whether it is only
        a Figma design concept rendered by ToggleButton internally when label=null.
    fix_action: "Check @8x8/oxygen-toggle-button package exports for a named ToggleInput export; document its API if present, or add a note clarifying it is internal-only"
    blocks: []
    dependency: []

  - id: GAP-008
    dimension: tokens
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: true
    evidence:
      source_file: tokens.md
      location: "## Spacing (from Figma guidelines) — $spacing02 / $spacing03"
      finding: >
        Spacing values are referenced as `$spacing02` (4px) and `$spacing03` (8px) using
        Figma's legacy dollar-sign token syntax. The Oxygen token system uses CSS variable
        format (e.g. `--spacing-02`). The canonical token names and their exact CSS variable
        equivalents are undocumented.
    fix_action: "Resolve $spacing02/$spacing03 against the Oxygen spacing token table (get-theme-tokens category=spacing); update tokens.md with canonical CSS variable names"
    blocks: []
    dependency: []

  - id: GAP-009
    dimension: figma
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: ToggleButton-figma.md
      location: "## Interaction states — hover row"
      finding: >
        The Figma examples page (node 50606:95349) state diagram lists 'Hover' and
        'isOn - Hover' as named states with corresponding Toggle instances. However,
        hover is not modelled as a separate variant axis in the component sets, and
        the visual change (fill colour or knot movement) is not annotated. The hover
        treatment is unknown.
    fix_action: "Inspect the hover-state Toggle instances on the examples page (Col 2, rows 1 and 5) using figma_get_component on those specific instance nodes to determine hover fill tokens"
    blocks: []
    dependency: []

warnings:
  - id: WARN-001
    dimension: accessibility
    confidence: heuristic
    note: >
      accessibility.md documents aria-checked="mixed" for isIndeterminate. Native HTML
      checkbox indeterminate state is set via the JS .indeterminate property, which
      does NOT change aria-checked — it remains false. If SwitchBase sets aria-checked
      explicitly, this is correct; if it relies purely on native behaviour, the claim
      may be inaccurate. Verify against the SwitchBase implementation.

  - id: WARN-002
    dimension: accessibility
    confidence: heuristic
    note: >
      WCAG 1.4.11 (Non-text Contrast) is marked ⚠️ in the checklist —
      default toggle base (#6c6862) on white background needs contrast verification.
      Calculated ratio: #6c6862 on #ffffff ≈ 4.6:1 which PASSES 3:1. The ⚠️ in
      accessibility.md should be updated to ✅ pending confirmation of the actual
      background context.
# --- navigation (added by component-map) ---
role: audit
pipeline_stage: blocked
pipeline_note: "Audit verdict NO — resolve CONFLICTs before rewrite"
siblings:
  - "[[ToggleButton/props]]"
  - "[[ToggleButton/examples]]"
  - "[[ToggleButton/tokens]]"
  - "[[ToggleButton/accessibility]]"
  - "[[ToggleButton/ToggleButton-figma]]"
  - "[[ToggleButton/ToggleButton-pui]]"
  - "[[ToggleButton/ToggleButton-usage]]"
tags:
  - oxygen
  - component/ToggleButton
  - role/audit
  - stage/blocked
---

# ToggleButton — Documentation Audit

> **Rubric version:** 1.0 · **Audit date:** 2026-04-29 · **Verdict:** NO

---

## File Inventory

| File | Status | Produced by |
|------|--------|-------------|
| `props.md` | ✅ Present | oxygen-mcp-extract |
| `examples.md` | ✅ Present | oxygen-mcp-extract |
| `tokens.md` | ✅ Present | oxygen-mcp-extract |
| `accessibility.md` | ✅ Present | oxygen-mcp-extract |
| `ToggleButton-figma.md` | ✅ Present | figma-extract |
| `ToggleButton-pui.md` | ✅ Present — NO RELEVANT PUI CONTEXT | pui-mcp-extract |
| `ToggleButton-usage.md` | ✅ Present — _editorial draft 2026-05-15_ | editorial (replace with figma-extract-usage once Figma cards exist) |

---

## Dimension Scores

| Dimension | Score | Coverage | Status |
|-----------|-------|----------|--------|
| Props | 0.83 | 10/12 | ✅ Available |
| Examples | 0.80 | 8/10 | ✅ Available |
| Tokens | 0.80 | 8/10 | ✅ Available |
| Accessibility | 0.88 | 7/8 | ✅ Available |
| Figma | 0.78 | 7/9 | ✅ Available — ⛔ 2 CONFLICTs |
| Usage | 0.70 | editorial draft present | ⚠️ partial-resolved-editorial — Figma cards still missing |
| PUI | 1.00 | resolved | ✅ No relevant context (confirmed) |
| **Available avg** | **0.85** | | |
| **Overall avg** | **0.82** | | _was 0.73 before GAP-003 partial resolution 2026-05-15_ |

---

## Gap Summary

| Count | Category |
|-------|----------|
| 2 | CONFLICTs (1 minor auto-fixable, 1 major requires human) — **blocks doc-rewrite** |
| 5 | SOURCE_GAPs (5 minor — GAP-003 partial-resolved-editorial 2026-05-15; 4 others unchanged) |
| 4 | DOC_GAPs (all minor) |
| 2 | Warnings (heuristic, advisory) |

---

## Gaps

### CONFLICTs — must be resolved before doc-rewrite

#### GAP-001 · Figma · MINOR · auto-fixable

**Finding:** Figma names the checked state `isOn?`; OX prop is `isChecked`. The mapping is already documented in the Persistent States table but is not explicitly flagged as a naming divergence.
**Fix:** Add a one-line note in ToggleButton-figma.md: _"Figma `isOn?` = OX `isChecked` — same concept, different naming convention."_

#### GAP-002 · Figma/Props · MAJOR · requires human input

**Finding:** Figma ToggleGroup has a full `isError` variant (error icon + red message text). OX `ToggleButtonGroup` has no `isError` prop (`isHorizontal` and `children` only). The design specifies error-state behaviour that the API cannot produce.
**Fix:** Designer/developer confirms whether `isError` should be added to `ToggleButtonGroup`; or document the consumer-composition pattern for showing errors below a group.

---

### SOURCE_GAPs

#### GAP-003 · Usage · MINOR · _partial-resolved-editorial 2026-05-15_
**Finding:** `ToggleButton-usage.md` is now present as an editorial draft (drafted 2026-05-15 from the Oxygen web docs at [oxygen.8x8.com/components/toggle/usage](https://oxygen.8x8.com/components/toggle/usage) combined with the extracted MCP/Figma artifacts). The upstream Figma source — `✅ Do — …` / `❌ Don't — …` card frames on the Toggle examples page (`50606:95349`) — is still missing.
**Fix:** Author Do/Don't cards on the Figma examples page, then run `figma-extract-usage ToggleButton` and replace the editorial draft wholesale.

#### GAP-004 · Figma · MINOR
**Finding:** `figma_get_component_details` failed (Desktop Bridge not running). Component keys for all three component sets not retrieved.
**Fix:** Enable Desktop Bridge; re-run `figma_get_component_details` for nodes `51776:7539`, `51776:7580`, `52689:99119`.

#### GAP-005 · Figma/Tokens · MINOR
**Finding:** `figma_get_variables` failed. Token bindings are inferred from CSS export, not verified from the Variables API. Alias chains unconfirmed.
**Fix:** Enable Desktop Bridge or Enterprise API; re-run `figma_get_variables` with `resolveAliases=true`.

#### GAP-009 · Figma · MINOR
**Finding:** Hover state visible in the examples page state diagram but no visual-change annotation exists. Hover treatment (fill, knot change) is unknown.
**Fix:** Inspect hover-state Toggle instances on examples page via `figma_get_component` to determine hover tokens.

---

### DOC_GAPs (all minor)

#### GAP-006 · Props · auto-fixable
`value` prop shape variant `{ id: string }` has no usage documentation or example.
→ **Fix:** Add a note or example showing when `value={{ id: '...' }}` is appropriate.

#### GAP-007 · Props · requires human input
Toggle Input not confirmed as individually importable from `@8x8/oxygen-toggle-button`.
→ **Fix:** Check package exports for a named `ToggleInput` export; document or clarify.

#### GAP-008 · Tokens · auto-fixable
`$spacing02` / `$spacing03` use Figma's legacy syntax; canonical OX CSS variable names undocumented.
→ **Fix:** Look up spacing tokens via `get-theme-tokens category=spacing`; update `tokens.md`.

---

## Warnings

**WARN-001 (Accessibility):** `aria-checked="mixed"` for `isIndeterminate` may be incorrect — native HTML checkbox `.indeterminate` does not change `aria-checked`. Verify against `SwitchBase` source.

**WARN-002 (Accessibility):** WCAG 1.4.11 marked ⚠️ for default toggle base (#6c6862 on white). Calculated contrast ≈ 4.6:1 which passes 3:1 minimum — the ⚠️ likely should be ✅. Confirm against actual background context.

---

## Verdict: NO

**doc-rewrite is blocked until both CONFLICTs are resolved.**

Resolve in this order:

```
1. Fix GAP-001  → add isOn?↔isChecked mapping note to ToggleButton-figma.md (1 line)
2. Resolve GAP-002  → designer/developer confirms isError API intent
3. (Done — editorial 2026-05-15) ToggleButton-usage.md is present as an editorial draft
   → Figma cards on examples page 50606:95349 are still required to replace it with
   figma-extract-usage output. GAP-003 is partial-resolved-editorial.
4. (Optional) Fix GAP-008   → resolve $spacing02/$spacing03 token names
5. Re-run doc-audit         → verdict should reach YES
6. Run doc-rewrite          → produces ToggleButton-spec.md
```

_Source: doc-audit skill · Rubric v1.0 · 2026-04-29_
