---
rubric_version: "1.0"
component: TextArea
package: "@8x8/oxygen-textarea"
extracted: "2026-04-29"
audited: "2026-04-29"
rewrite_run: "2026-06-05"
verdict: "NO"
verdict_reason: "3 unresolved CONFLICTs between Figma variant axes and Oxygen API — Size/Mode/Filled have no direct prop counterparts; CONFLICT markers inserted in spokes; resolve before promoting to authoritative."
files_found:
  - source/props.md
  - source/examples.md
  - source/tokens.md
  - source/accessibility.md
  - source/textarea-figma.md
  - source/textarea-pui.md
  - source/textarea-usage-draft.md
files_missing:
  - source/textarea-usage.md
scores:
  props_completeness: 1.0
  examples_quality: 0.89
  tokens_coverage: 0.75
  anatomy_structure: 0.89
  accessibility: 1.0
  figma_alignment: 0.70
  pui_context: 1.0
totals:
  doc_gaps_applied: 6
  doc_gaps_remaining: 1
  source_gaps: 3
  conflicts: 3
  warnings: 2
gaps:
  - id: GAP-001
    dimension: usage
    severity: major
    type: SOURCE_GAP
    status: stub_inserted
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: "(absent)"
      location: "component-lib/TextArea/source/"
      finding: "textarea-usage.md does not exist — figma-extract-usage skill was not run"
    fix_action: "Run figma-extract-usage skill for TextArea to produce textarea-usage.md with Do/Don't usage guidelines from Figma"
    stub_target: "TextArea.usage.md"
    blocks:
      - docusaurus-generate
    dependency: []

  - id: GAP-002
    dimension: props_completeness
    severity: major
    type: DOC_GAP
    status: applied
    applied_date: "2026-06-05"
    confidence: deterministic
    auto_fixable: true
    evidence:
      source_file: source/accessibility.md
      location: "## Labelling section, lines 20–29"
      finding: "accessibility.md uses aria-label, aria-labelledby, aria-describedby in code examples, but props.md had no entry for these HTML pass-through attributes."
    fix_action: "Added aria-label, aria-labelledby, aria-describedby, aria-invalid, aria-required, required as HTML pass-through props to source/props.md with a note about HTMLTextAreaElement pass-through"
    blocks:
      - storybook-generate
    dependency: []

  - id: GAP-003
    dimension: accessibility
    severity: major
    type: DOC_GAP
    status: applied
    applied_date: "2026-06-05"
    confidence: deterministic
    auto_fixable: true
    evidence:
      source_file: source/accessibility.md
      location: "## Error state section"
      finding: "aria-invalid='true' was missing from the error state pattern in accessibility.md and props.md."
    fix_action: "Added aria-invalid='true' to Error state section in source/accessibility.md; aria-invalid added to props table in source/props.md via GAP-002"
    blocks: []
    dependency:
      - GAP-002

  - id: GAP-004
    dimension: tokens_coverage
    severity: major
    type: SOURCE_GAP
    status: stub_inserted
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: source/tokens.md
      location: "## Dark mode section"
      finding: "tokens.md has a stale 'not resolved' note for dark mode. Dark values are available in source/textarea-figma.md (resolved 2026-05-05 via figma_execute alias chain traversal) but tokens.md was not re-extracted."
    fix_action: "Re-extract tokens.md with Figma Desktop Bridge active to confirm dark mode token aliases match the resolved values in textarea-figma.md"
    stub_target: "TextArea.tokens.md"
    blocks:
      - dark-mode-implementation
    dependency: []

  - id: GAP-005
    dimension: examples_quality
    severity: minor
    type: DOC_GAP
    status: applied
    applied_date: "2026-06-05"
    confidence: deterministic
    auto_fixable: true
    evidence:
      source_file: source/examples.md
      location: "## Error state section"
      finding: "Error state example showed hasError={true} in isolation without accessible pattern."
    fix_action: "Replaced bare hasError example in source/examples.md with full accessible error pattern (label, aria-invalid, aria-describedby, role='alert')"
    blocks: []
    dependency:
      - GAP-003

  - id: GAP-006
    dimension: tokens_coverage
    severity: minor
    type: DOC_GAP
    status: skip
    confidence: heuristic
    auto_fixable: false
    evidence:
      source_file: source/tokens.md
      location: "## Text colors table"
      finding: "tokens.md does not document the text color for the Filled=True state (when user has entered content). Only Filled=False baseline was verified."
    fix_action: "Inspect Mode=Light, Size=Large, State=Rest, Filled=True variant (node 21722:35590) in Figma to confirm the input value text color token"
    skip_reason: "Requires manual Figma inspection — cannot be auto-fixed"
    skip_marker: "TextArea.tokens.md"
    blocks: []
    dependency: []

  - id: GAP-007
    dimension: figma_alignment
    severity: major
    type: CONFLICT
    status: conflict_marker_inserted
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: source/textarea-figma.md
      location: "## API — Variant axes table"
      finding: "Figma component has a Size variant axis with values Large/Medium/Small. The Oxygen Textarea API exposes no 'size' prop — sizing is controlled via rows/cols."
    fix_action: "Confirm with component owner: is size controlled exclusively via rows/cols, or is a size prop planned/hidden? Document the answer."
    conflict_markers_in:
      - TextArea.props.md
      - TextArea.anatomy.md
    blocks:
      - authoritative-promotion
    dependency: []

  - id: GAP-008
    dimension: figma_alignment
    severity: major
    type: CONFLICT
    status: conflict_marker_inserted
    confidence: deterministic
    auto_fixable: true
    evidence:
      source_file: source/textarea-figma.md
      location: "## API — Variant axes table + Gaps & conflicts"
      finding: "Figma has a Mode variant axis (Light/Dark). The Oxygen Textarea API has no 'mode' prop. figma.md states dark mode is 'controlled at the Oxygen theme provider level'."
    fix_action: "Confirm dark mode is OxygenProvider-controlled; once confirmed, add a one-line note to props.md and mark resolved"
    conflict_markers_in:
      - TextArea.props.md
    blocks:
      - authoritative-promotion
    dependency: []

  - id: GAP-009
    dimension: figma_alignment
    severity: minor
    type: CONFLICT
    status: conflict_marker_inserted
    confidence: heuristic
    auto_fixable: false
    evidence:
      source_file: source/textarea-figma.md
      location: "## API — Variant axes table + Gaps & conflicts"
      finding: "Figma has a Filled variant axis (False/True) with no direct Oxygen prop. Likely a derived visual state when value !== '' but not confirmed from Oxygen source."
    fix_action: "Confirm whether Filled=True/False in Figma maps to value !== '' in code — document in props.md value prop description"
    conflict_markers_in:
      - TextArea.anatomy.md
      - TextArea.props.md
    blocks:
      - authoritative-promotion
    dependency: []

  - id: GAP-010
    dimension: accessibility
    severity: minor
    type: DOC_GAP
    status: applied
    applied_date: "2026-06-05"
    confidence: heuristic
    auto_fixable: true
    evidence:
      source_file: source/accessibility.md
      location: "## WCAG 2.1 AA Checklist"
      finding: "WCAG 1.4.3 cell did not provide contrast ratio or PASS/FAIL verdict for disabled state colours."
    fix_action: "Added contrast ratio (~1.9:1 for #8d8b7e on #c8c8bd) and explicit WCAG 1.4.3 Note 1 exemption to source/accessibility.md"
    blocks: []
    dependency: []

  - id: GAP-011
    dimension: anatomy_structure
    severity: minor
    type: SOURCE_GAP
    status: stub_inserted
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: source/textarea-figma.md
      location: "## Size variants table"
      finding: "Medium and Small input box heights are approximate. Only the Large variant (112px box) was directly verified from Figma get_design_context."
    fix_action: "Call get_design_context on node 21562:34998 (Medium/Rest) and 21562:35010 (Small/Rest) to confirm exact heights"
    stub_target: "TextArea.anatomy.md"
    blocks: []
    dependency: []

  - id: GAP-012
    dimension: props_completeness
    severity: minor
    type: DOC_GAP
    status: applied
    applied_date: "2026-06-05"
    confidence: heuristic
    auto_fixable: true
    evidence:
      source_file: source/props.md
      location: "## Notes section"
      finding: "hasError note was ambiguous about where the Error Area is rendered."
    fix_action: "Clarified in source/props.md Notes that Figma's Error Area is not rendered by the Oxygen component — consumers must render error text externally via aria-describedby"
    blocks: []
    dependency:
      - GAP-003

  - id: GAP-013
    dimension: figma_alignment
    severity: minor
    type: DOC_GAP
    status: applied
    applied_date: "2026-06-05"
    confidence: deterministic
    auto_fixable: true
    evidence:
      source_file: source/props.md
      location: "## resize values table"
      finding: "The relationship between the resize prop and Figma's 'Resize grip' toggle was not explained."
    fix_action: "Added a note under the resize values table in source/props.md clarifying that Figma's 'Resize grip' is a design-only affordance, not mapped to the resize prop"
    blocks: []
    dependency: []

warnings:
  - id: WARN-001
    confidence: heuristic
    finding: "examples.md discloses that examples were synthesized from the API (not from actual MCP Storybook stories). The examples have not been run against a real Oxygen installation."
    recommendation: "Validate examples against a live Storybook or sandbox before publishing"

  - id: WARN-002
    confidence: heuristic
    finding: "accessibility.md WCAG guidance is inferred from component type (native <textarea>) since Figma had no accessibility annotations. The guidance is standard-compliant, but has not been validated against the actual Oxygen Textarea implementation."
    recommendation: "Test accessibility guidance against the live component with VoiceOver or NVDA before publishing"
# --- navigation ---
role: audit
pipeline_stage: rewrite_partial
pipeline_note: "doc-rewrite ran 2026-06-05 — 6 DOC_GAPs applied, 3 CONFLICT markers inserted; resolve CONFLICTs to promote to authoritative"
siblings:
  - "[[TextArea]]"
  - "[[TextArea.props]]"
  - "[[TextArea.anatomy]]"
  - "[[TextArea.tokens]]"
  - "[[TextArea.usage]]"
  - "[[TextArea.accessibility]]"
  - "[[TextArea.platform]]"
  - "[[TextArea.composition]]"
tags:
  - oxygen
  - component/TextArea
  - role/audit
  - stage/rewrite_partial
---

# TextArea — Documentation Audit

**Verdict: NO** — 3 unresolved CONFLICTs between Figma variant axes and Oxygen API. doc-rewrite ran on 2026-06-05 with CONFLICT markers inserted; spokes are in `draft` status pending resolution.

---

## doc-rewrite run (2026-06-05)

| Action | Count | Gap IDs |
|--------|-------|---------|
| DOC_GAPs applied to source files | 6 | GAP-002, GAP-003, GAP-005, GAP-010, GAP-012, GAP-013 |
| SOURCE_GAPs stubbed in spokes | 3 | GAP-001, GAP-004, GAP-011 |
| CONFLICTs — markers inserted | 3 | GAP-007, GAP-008, GAP-009 |
| DOC_GAPs skipped (manual) | 1 | GAP-006 |
| Source files moved to `source/` | 8 | flat layout → canonical layout |
| Spokes written | 8 | hub + 7 spokes |

---

## File inventory

| File | Status | Notes |
|------|--------|-------|
| `source/props.md` | ✅ Present (modified) | 6 ARIA pass-through props added; Error Area note clarified; resize/grip note added |
| `source/examples.md` | ✅ Present (modified) | Error state replaced with accessible pattern |
| `source/tokens.md` | ✅ Present | Unmodified — dark mode note is stale (see GAP-004) |
| `source/accessibility.md` | ✅ Present (modified) | aria-invalid added to Error state; WCAG 1.4.3 disabled exemption documented |
| `source/textarea-figma.md` | ✅ Present | Unmodified |
| `source/textarea-pui.md` | ✅ Present | Unmodified — confirmed no PUI relevance |
| `source/textarea-usage-draft.md` | ✅ Present (draft) | Editorial draft by usage-advisor; not canonical |
| `source/textarea-usage.md` | ❌ **Missing** | GAP-001 STUB — run figma-extract-usage |

---

## Dimension scores

| Dimension | Score (original) | Score (current) | Change | Remaining gaps |
|-----------|-----------------|-----------------|--------|----------------|
| Props completeness | 0.85 | **1.0** | +0.15 | None — GAP-002, GAP-012 applied |
| Examples quality | 0.78 | **0.89** | +0.11 | WARN-001 (synthesized) |
| Tokens coverage | 0.75 | **0.75** | — | GAP-004 stub, GAP-006 skip |
| Anatomy / structure | 0.89 | **0.89** | — | GAP-011 stub |
| Accessibility | 0.78 | **1.0** | +0.22 | None — GAP-003, GAP-010 applied |
| Figma alignment | 0.62 | **0.70** | +0.08 | GAP-007, GAP-008, GAP-009 (CONFLICTs) |
| PUI context | 1.00 | **1.0** | — | — |

**Overall: 0.89 weighted average** _(CONFLICTs suppress verdict regardless of score)_

---

## Gaps summary

### CONFLICTs — unresolved (block authoritative promotion)

| ID | Spoke(s) | Summary | Likely answer |
|----|----------|---------|---------------|
| GAP-007 | anatomy, props | Figma `Size` axis (L/M/S) has no `size` prop | Rows/cols intentional — confirm with owner |
| GAP-008 | props | Figma `Mode` axis has no `mode` prop | OxygenProvider theme — almost certainly correct |
| GAP-009 | anatomy, props | Figma `Filled` axis has no Oxygen prop | Derived from `value !== ''` — almost certainly correct |

### SOURCE_GAPs — stubbed in spokes

| ID | Spoke | Summary |
|----|-------|---------|
| GAP-001 | usage | `textarea-usage.md` absent — STUB in TextArea.usage.md |
| GAP-004 | tokens | `tokens.md` dark mode note stale — STUB in TextArea.tokens.md (dark values available in figma.md) |
| GAP-011 | anatomy | Medium/Small heights approximate — STUB in TextArea.anatomy.md |

### DOC_GAPs — applied

| ID | File modified | Summary |
|----|--------------|---------|
| GAP-002 | source/props.md | Added 6 ARIA pass-through props |
| GAP-003 | source/accessibility.md | Added aria-invalid to error state |
| GAP-005 | source/examples.md | Accessible error pattern |
| GAP-010 | source/accessibility.md | WCAG 1.4.3 disabled contrast exemption |
| GAP-012 | source/props.md | Error Area rendering clarification |
| GAP-013 | source/props.md | resize prop vs Figma Resize grip distinction |

### DOC_GAPs — skipped (manual)

| ID | Spoke | Summary |
|----|-------|---------|
| GAP-006 | tokens | Filled=True input text color — inspect Figma node 21722:35590 manually |

### Warnings (advisory)

| ID | Summary |
|----|---------|
| WARN-001 | Examples synthesized from API, not validated against live Storybook |
| WARN-002 | Accessibility guidance inferred from component type, not Figma annotations |

---

## Required actions to finalize

1. **Resolve GAP-007** (Size): Confirm with component owner — rows/cols intentional, or size prop planned?
2. **Resolve GAP-008** (Mode): Confirm theme-provider controls dark/light mode — update CONFLICT marker to resolved note in TextArea.props.md
3. **Resolve GAP-009** (Filled): Confirm `Filled=True` = `value !== ''` — update CONFLICT marker to resolved note
4. **Run figma-extract-usage** (GAP-001): Produces canonical `textarea-usage.md`; replaces draft content in TextArea.usage.md

Once 3 CONFLICTs are resolved, **verdict upgrades to YES**, spokes promote from `draft` to `partial`/`complete`, and TextArea.md status promotes accordingly.

---

## Next action

Easiest path — two are nearly self-answering:
- **GAP-008** (Mode): almost certainly OxygenProvider — add confirmed note to TextArea.props.md, remove CONFLICT marker
- **GAP-009** (Filled): almost certainly derived state — add confirmed note to TextArea.props.md / TextArea.anatomy.md, remove CONFLICT marker
- **GAP-007** (Size): requires component owner confirmation

_Source: doc-audit skill v1.0 · Audited 2026-04-29 · Updated post-doc-rewrite 2026-06-05_
