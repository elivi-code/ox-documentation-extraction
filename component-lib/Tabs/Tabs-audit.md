---
rubric_version: "1.0"
component: Tabs
package: "@8x8/oxygen-tabs"
audit_date: "2026-05-05"
auditor: doc-audit skill
prior_audit: "2026-04-30"

files_found:
  - props.md
  - examples.md
  - tokens.md
  - accessibility.md
  - Tabs-figma.md
  - Tabs-pui.md
  - Tabs-usage.md  # editorial — drafted via usage-advisor 2026-05-15; Figma cards still missing

files_missing: []

dimension_scores:
  props:        { score: 0.80, coverage: "8/10" }
  examples:     { score: 0.67, coverage: "6/9"  }
  tokens:       { score: 0.70, coverage: "7/10" }   # improved: semantic names + typography now in Tabs-figma.md
  accessibility: { score: 0.78, coverage: "7/9"  }
  figma:        { score: 0.78, coverage: "9/12" }   # improved: full color/token section added
  usage:        { score: 0.50, coverage: "editorial — Tabs-usage.md drafted via usage-advisor 2026-05-15; Figma Do/Don't cards still missing on examples page 85697:271849" }
  pui:          { score: 1.00, coverage: "PASS — NO RELEVANT PUI CONTEXT confirmed by engineer" }

available_dimensions_avg: 0.79
overall_avg: 0.68

counts:
  doc_gaps: 8
  source_gaps: 2
  conflicts: 0
  warnings: 3

verdict: "YES"
verdict_reason: >
  Zero CONFLICTs and zero blocker-severity gaps. Verdict unchanged from prior audit.
  Token dimension substantially improved: semantic token names (ui/ui01, actions/action01,
  text/textColor01/02, icon/icon01, interactive/focus01/disabled02, notification/notification01)
  and typography tokens (body01, bodyBold01, labelBold01) are now documented in
  Tabs-figma.md §Color & token bindings (added 2026-05-05 via figma_execute alias chain
  traversal). GAP-001 is now auto-fixable (data in figma.md); GAP-002 and GAP-005 are
  resolved. GAP-010 is now resolvable (bold-text intent confirmed).
  doc-rewrite can proceed on all dimensions.

gaps:
  - id: GAP-001
    dimension: tokens
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: true
    evidence:
      source_file: tokens.md
      location: "## Color variables observed in Figma variants"
      finding: >
        tokens.md still contains unresolved Figma variable IDs (20136:253 etc.) without
        semantic names. The semantic token names are now available in Tabs-figma.md
        §Color & token bindings. doc-rewrite should pull token names from figma.md to
        populate the canonical token table.
    fix_action: "Update tokens.md using semantic names from Tabs-figma.md §Color & token bindings: ui/ui01, actions/action01, text/textColor01, text/textColor02, icon/icon01, interactive/focus01, interactive/disabled02, notification/notification01."
    blocks: [storybook-generate]
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
      source_file: Tabs-usage.md
      location: "component-lib/Tabs/Tabs-usage.md"
      finding: >
        Tabs-usage.md is now present as an editorial draft (drafted 2026-05-15 via
        usage-advisor Open mode from props.md + examples.md + accessibility.md + Tabs-figma.md).
        Upstream Figma source still missing: the 'Tabs — Examples' page (node 85697:271849)
        contains no `✅ Do — …` / `❌ Don't — …` card frames, so figma-extract-usage cannot run.
        Replace Tabs-usage.md wholesale with figma-extract-usage output once cards are authored.
    fix_action: "Author Do/Don't card frames on Figma examples page 85697:271849, then run figma-extract-usage Tabs to replace the editorial draft."
    blocks: []                   # no longer blocks doc-rewrite — editorial usage covers the dimension
    dependency: []

  - id: GAP-004
    dimension: figma
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: Tabs-figma.md
      location: "## Visual snapshots — all three image references"
      finding: >
        Three screenshot PNGs referenced in Tabs-figma.md (figma-tabs-variants.png,
        figma-tabs-disclosure.png, figma-tabs-popover-atom.png) are not present in the
        component-lib/Tabs/ directory.
    fix_action: "Re-capture and save PNGs from Figma nodes 85651:78740, 85651:78793, 86754:680 using figma_take_screenshot."
    blocks: [docusaurus-generate]
    dependency: []

  - id: GAP-006
    dimension: figma
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: true
    evidence:
      source_file: Tabs-figma.md
      location: "## Design properties / selectIcon row"
      finding: "selectIcon default icon is node 85016:131 — name not identified. Documented only as 'chevron icon'."
    fix_action: "Query figma_get_component for node 85016:131 to retrieve icon name; update selectIcon default in Tabs-figma.md."
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
      location: "## <Tab> — isStretched row"
      finding: "isStretched description is inferred (MCP returned eslint-disable comment instead of real doc string)."
    fix_action: "Verify isStretched behaviour from @8x8/oxygen-tabs source or Storybook; update description if incorrect."
    blocks: []
    dependency: []

  - id: GAP-008
    dimension: props
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: props.md
      location: "## <Tabs> and ## <Tab> — color prop, Default column"
      finding: "color prop default value undocumented for both <Tabs> and <Tab>."
    fix_action: "Check @8x8/oxygen-tabs source for color prop default; document in props.md."
    blocks: []
    dependency: []

  - id: GAP-009
    dimension: accessibility
    severity: minor
    type: DOC_GAP
    confidence: heuristic
    auto_fixable: true
    evidence:
      source_file: accessibility.md
      location: "## Keyboard interactions — table"
      finding: >
        Arrow key (Left/Right) navigation within the tablist is not documented. WAI-ARIA
        Authoring Practices for tablist pattern require Left/Right arrows to move focus
        between tabs.
    fix_action: "Confirm whether OX Tabs implements arrow key navigation; add Left/Right (and optionally Home/End) rows to keyboard interaction table."
    blocks: []
    dependency: []

  - id: GAP-010
    dimension: accessibility
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: true
    evidence:
      source_file: accessibility.md
      location: "## WCAG 2.1 Level AA compliance"
      finding: >
        WCAG 1.4.1 (Use of Color) not addressed in the checklist. The selected tab uses
        both a 2px blue underline AND bold text (typography/bodyBold01 — confirmed in
        Tabs-figma.md), so the component passes 1.4.1 (two non-color indicators). This
        should be explicitly documented in the WCAG table.
    fix_action: "Add WCAG 1.4.1 row to accessibility.md WCAG table: PASS — selected state indicated by underline (actions/action01) + bold text (bodyBold01), not color alone."
    blocks: []
    dependency: []

  - id: GAP-011
    dimension: all-ox-files
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: true
    evidence:
      source_file: props.md / examples.md / tokens.md / accessibility.md
      location: "'See also' nav line in each file"
      finding: >
        All four OX files reference 'figma.md' in their See also nav line — the actual
        filename is 'Tabs-figma.md'. All four cross-links are broken.
    fix_action: "Replace 'figma.md' → 'Tabs-figma.md' in the See also line of props.md, examples.md, tokens.md, accessibility.md."
    blocks: []
    dependency: []

  - id: GAP-012
    dimension: examples
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: examples.md
      location: "## Basic usage — note block"
      finding: >
        No MCP-sourced code examples exist (OX MCP returned 0 clean snippets). All code
        was constructed from prop definitions. No examples for icon, badge, or hasDropdown.
    fix_action: "Source real usage examples from @8x8/oxygen-tabs Storybook or source repo."
    blocks: []
    dependency: []

warnings:
  - id: WARN-001
    dimension: props
    confidence: heuristic
    note: >
      forwardedRef is listed as required by the OX MCP but has a null default value. For a
      ref-forwarding prop this is unusual — required with a null default implies the component
      will accept a null ref gracefully, but the API is ambiguous. Downstream type generation
      may emit a non-optional ref parameter.

  - id: WARN-002
    dimension: accessibility
    confidence: heuristic
    note: >
      ARIA roles in accessibility.md are labelled 'inferred from component nature'. The actual
      Oxygen implementation may render as plain div/button elements without role="tablist" /
      role="tab" / aria-selected. Verify against the rendered DOM before shipping docs.

  - id: WARN-003
    dimension: figma
    confidence: heuristic
    note: >
      tabsDisclosure inherits an 'active' press state from Icon Button, but the tabs
      COMPONENT_SET exposes only 'rest' and 'hover' variant axes. Press-state visual (if any)
      is undocumented.
# --- navigation (added by component-map) ---
role: audit
pipeline_stage: spec_complete
pipeline_note: "Canonical spec written — pipeline complete"
siblings:
  - "[[Tabs/props]]"
  - "[[Tabs/examples]]"
  - "[[Tabs/tokens]]"
  - "[[Tabs/accessibility]]"
  - "[[Tabs/Tabs-figma]]"
  - "[[Tabs/Tabs-pui]]"
  - "[[Tabs/Tabs-spec]]"
tags:
  - oxygen
  - component/Tabs
  - role/audit
  - stage/spec_complete
---

# Tabs — Documentation Audit

> **Verdict: YES** — doc-rewrite can proceed on all dimensions.
> Token and typography gaps resolved 2026-05-05.
>
> Rubric version: 1.0 · Prior audit: 2026-04-30 · Re-audited: 2026-05-05

---

## File Inventory

| File | Status | Produced by |
|------|--------|-------------|
| `props.md` | ✅ Present | oxygen-mcp-extract |
| `examples.md` | ✅ Present | oxygen-mcp-extract |
| `tokens.md` | ✅ Present | oxygen-mcp-extract |
| `accessibility.md` | ✅ Present | oxygen-mcp-extract |
| `Tabs-figma.md` | ✅ Present | figma-extract |
| `Tabs-usage.md` | 🟡 Present (editorial — drafted 2026-05-15 via usage-advisor; Figma cards still missing) | usage-advisor / pending figma-extract-usage |
| `Tabs-pui.md` | ✅ Present — `NO RELEVANT PUI CONTEXT` | pui-mcp-extract |

---

## Dimension Scores

| Dimension | Score | Coverage | Notes |
|-----------|-------|----------|-------|
| Props | 0.80 | 8/10 | ✅ Available |
| Examples | 0.67 | 6/9 | ✅ Available |
| Tokens | 0.70 | 7/10 | ✅ ▲ **Improved from 0.50** — semantic names + typography now in Tabs-figma.md |
| Accessibility | 0.78 | 7/9 | ✅ Available |
| Figma | 0.78 | 9/12 | ✅ ▲ **Improved from 0.67** — full color/token section added |
| Usage | 0.00 | — | ❌ SOURCE_GAP (major) — file missing |
| PUI | 1.00 | PASS | ✅ Resolved — no relevant context |
| **Available avg** | **0.79** | | ▲ up from 0.74 |
| **Overall avg** | **0.68** | | ▲ up from 0.63 |

---

## Resolved since prior audit (2026-04-30)

| Was | Resolution |
|-----|-----------|
| GAP-001: variable IDs unresolved → not auto-fixable | **Reclassified** — semantic token names now in `Tabs-figma.md §Color & token bindings`; gap is now auto-fixable by doc-rewrite pulling from figma.md |
| GAP-002 (major SOURCE_GAP): no typography tokens | **Resolved** — `body01`, `bodyBold01`, `labelBold01` documented in `Tabs-figma.md §Typography tokens` (confirmed via figma_execute 2026-05-05) |
| GAP-005: selected tab bold text not documented | **Resolved** — `typography/bodyBold01` confirmed as selected-tab text style; documented in `Tabs-figma.md §Color & token bindings` |
| GAP-010 (blocked by GAP-005): WCAG 1.4.1 unresolvable | **Unblocked** — bold-text intent now confirmed; WCAG 1.4.1 can be documented as PASS (underline + bold = two indicators) |

---

## Gap Summary

| Count | Category |
|-------|----------|
| 0 | CONFLICTs — **no blocks on doc-rewrite** |
| 2 | SOURCE_GAPs (1 major, 1 minor) |
| 8 | DOC_GAPs (all minor) |
| 3 | Warnings (heuristic, advisory) |

---

## Gaps

### SOURCE_GAP — Minor (partial-resolved-editorial 2026-05-15)

**GAP-003** · Usage — _partial-resolved-editorial_
> `Tabs-usage.md` is now present as an editorial draft (drafted 2026-05-15 via `usage-advisor` Open mode). The upstream Figma source — `✅ Do — …` / `❌ Don't — …` card frames on examples page `85697:271849` — is still missing.
> **Fix:** Author Do/Don't cards on the Figma examples page, then run `figma-extract-usage Tabs` and replace the editorial draft wholesale.

### SOURCE_GAP — Minor

**GAP-004** · Figma
> Three screenshot PNGs missing: `figma-tabs-variants.png`, `figma-tabs-disclosure.png`, `figma-tabs-popover-atom.png`.
> **Fix:** Re-capture from nodes `85651:78740`, `85651:78793`, `86754:680`.

### DOC_GAP — Minor (auto-fixable)

**GAP-001** · Tokens (now auto-fixable)
> `tokens.md` still has unresolved variable IDs. Semantic names are now in `Tabs-figma.md §Color & token bindings`.
> **Fix:** Update `tokens.md` with semantic names from `Tabs-figma.md`.

**GAP-006** · Figma
> `selectIcon` default icon is node `85016:131` — name not identified.
> **Fix:** Query `figma_get_component` for `85016:131`.

**GAP-009** · Accessibility
> Arrow key (Left/Right) navigation not documented for tablist pattern.
> **Fix:** Confirm implementation; add rows to keyboard interaction table.

**GAP-010** · Accessibility (now unblocked)
> WCAG 1.4.1 row missing from checklist. Bold-text intent now confirmed — component passes.
> **Fix:** Add WCAG 1.4.1 row: PASS — selected state uses underline + bold, not color alone.

**GAP-011** · All OX files
> "See also" links reference `figma.md` — actual filename is `Tabs-figma.md`. All four links broken.
> **Fix:** Update all four OX files.

### DOC_GAP — Minor (requires external verification)

**GAP-007** · Props
> `isStretched` description is inferred (MCP returned eslint-disable comment).
> **Fix:** Verify from source or Storybook.

**GAP-008** · Props
> `color` prop default undocumented for both `<Tabs>` and `<Tab>`.
> **Fix:** Check package source.

**GAP-012** · Examples
> No MCP-sourced code examples — all constructed from prop definitions. No icon/badge/hasDropdown examples.
> **Fix:** Source from `@8x8/oxygen-tabs` Storybook.

---

## Warnings

**WARN-001 (Props):** `forwardedRef` listed as required with null default — ambiguous API. Type generation may emit non-optional ref.

**WARN-002 (Accessibility):** ARIA roles are "inferred" in `accessibility.md`. Verify against rendered DOM.

**WARN-003 (Figma):** `tabsDisclosure` press state inherited from Icon Button but not captured in the Tabs component set variant axes.

---

## Suggested next actions

```
1. Fix GAP-011 (broken cross-links) → 5-min auto-fix before rewrite
2. Run doc-rewrite          → produces Tabs-spec.md
3. Add WCAG 1.4.1 to a11y  → GAP-010 (now unblocked — auto-fixable)
4. Update tokens.md         → GAP-001 (pull from Tabs-figma.md §Color & token bindings)
5. Save screenshots         → GAP-004
6. Run figma-extract-usage  → GAP-003
7. Verify ARIA roles        → WARN-002
8. Confirm arrow keys       → GAP-009
```

_Source: doc-audit skill v1.0 · Re-audited from component-lib/Tabs/ · 2026-05-05_
