---
rubric_version: "1.0"
component: TextArea
package: "@8x8/oxygen-textarea"
extracted: "2026-04-29"
audited: "2026-04-29"
verdict: NO
verdict_reason: "3 unresolved CONFLICTs between Figma variant axes and Oxygen API — Size/Mode/Filled have no direct prop counterparts; doc-rewrite cannot proceed until alignment is confirmed."
files_found:
  - props.md
  - examples.md
  - tokens.md
  - accessibility.md
  - textarea-figma.md
  - textarea-pui.md
files_missing:
  - textarea-usage.md
scores:
  props_completeness: 0.85
  examples_quality: 0.78
  tokens_coverage: 0.75
  anatomy_structure: 0.89
  accessibility: 0.78
  figma_alignment: 0.62
  pui_context: 1.0
totals:
  doc_gaps: 6
  source_gaps: 5
  conflicts: 3
  warnings: 2
gaps:
  - id: GAP-001
    dimension: usage
    severity: major
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: "(absent)"
      location: "component-lib/TextArea/"
      finding: "textarea-usage.md does not exist — figma-extract-usage skill was not run"
    fix_action: "Run figma-extract-usage skill for TextArea to produce textarea-usage.md with Do/Don't usage guidelines from Figma"
    blocks:
      - docusaurus-generate
    dependency: []

  - id: GAP-002
    dimension: props_completeness
    severity: major
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: true
    evidence:
      source_file: accessibility.md
      location: "## Labelling section, lines 20–29"
      finding: "accessibility.md uses aria-label, aria-labelledby, aria-describedby in code examples, but props.md has no entry for these HTML pass-through attributes. Consumers will not know they are accepted."
    fix_action: "Add aria-label, aria-labelledby, aria-describedby (and required, aria-required) as HTML pass-through props to props.md with a note that the underlying <textarea> accepts all standard HTMLTextAreaElement attributes"
    blocks:
      - storybook-generate
    dependency: []

  - id: GAP-003
    dimension: accessibility
    severity: major
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: true
    evidence:
      source_file: accessibility.md
      location: "## Error state section, lines 94–98"
      finding: "The error state section documents visual border change and aria-describedby pattern, but omits aria-invalid='true' which is the standard ARIA attribute for marking invalid form fields. It is not mentioned anywhere in accessibility.md or props.md."
    fix_action: "Add aria-invalid='true' to the Error state section in accessibility.md and to the props table in props.md as an HTML pass-through attribute"
    blocks: []
    dependency:
      - GAP-002

  - id: GAP-004
    dimension: tokens_coverage
    severity: major
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: tokens.md
      location: "## Dark mode section, line 90"
      finding: "Dark mode token values are unresolved. tokens.md states 'Dark mode token aliases were not resolved (variables API not accessible)'. figma-console variables API requires Enterprise Figma plan."
    fix_action: "Run Figma Desktop Bridge plugin in Figma Desktop to resolve dark mode token aliases — re-run figma_get_variables with Desktop Bridge active"
    blocks:
      - dark-mode-implementation
    dependency: []

  - id: GAP-005
    dimension: examples_quality
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: true
    evidence:
      source_file: examples.md
      location: "## Error state section, lines 55–63"
      finding: "The error state example shows hasError={true} in isolation. accessibility.md documents the full accessible pattern (aria-describedby + role='alert' + error message element), but this is not reflected in examples.md."
    fix_action: "Replace the bare hasError example in examples.md with the accessible error pattern from accessibility.md (aria-describedby + role='alert')"
    blocks: []
    dependency:
      - GAP-003

  - id: GAP-006
    dimension: tokens_coverage
    severity: minor
    type: DOC_GAP
    confidence: heuristic
    auto_fixable: false
    evidence:
      source_file: tokens.md
      location: "## Text colors table, lines 36–46"
      finding: "tokens.md documents placeholder text color as --text/textcolor02 but does not document the text color for the Filled=True state (when the user has entered content). Figma inspection covered only the Filled=False baseline variant."
    fix_action: "Inspect Mode=Light, Size=Large, State=Rest, Filled=True variant (node 21722:35590) in Figma to confirm the input value text color token"
    blocks: []
    dependency: []

  - id: GAP-007
    dimension: figma_alignment
    severity: major
    type: CONFLICT
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: textarea-figma.md
      location: "## API — Variant axes table, line 57"
      finding: "Figma component has a Size variant axis with values Large/Medium/Small, implying three distinct visual densities. The Oxygen Textarea API (props.md) exposes no 'size' prop. Rows/cols control dimensions instead. doc-rewrite cannot decide how to document size without this resolved."
    fix_action: "Confirm with component owner: is size controlled exclusively via rows/cols, or is a size prop planned/hidden? Document the answer in props.md Notes section."
    blocks:
      - doc-rewrite
    dependency: []

  - id: GAP-008
    dimension: figma_alignment
    severity: major
    type: CONFLICT
    confidence: deterministic
    auto_fixable: true
    evidence:
      source_file: textarea-figma.md
      location: "## API — Variant axes table, line 56 + Gaps & conflicts, line 254"
      finding: "Figma has a Mode variant axis (Light/Dark). The Oxygen Textarea API has no 'mode' prop. figma.md states dark mode is 'controlled at the Oxygen theme provider level'. This is likely correct but is not confirmed in props.md and may confuse consumers."
    fix_action: "Add a note to props.md clarifying that dark/light mode is not a prop — it is inherited from the OxygenProvider theme context"
    blocks:
      - doc-rewrite
    dependency: []

  - id: GAP-009
    dimension: figma_alignment
    severity: minor
    type: CONFLICT
    confidence: heuristic
    auto_fixable: false
    evidence:
      source_file: textarea-figma.md
      location: "## API — Variant axes table, line 61 + Gaps & conflicts, line 256"
      finding: "Figma has a Filled variant axis (False/True) with no direct Oxygen prop. The filled state appears to be a derived visual representation of whether value is non-empty. This is not confirmed from the Oxygen source."
    fix_action: "Confirm whether Filled=True/False in Figma maps to value !== '' in code (no explicit prop) — document in props.md or add a note in the value prop description"
    blocks:
      - doc-rewrite
    dependency: []

  - id: GAP-010
    dimension: accessibility
    severity: minor
    type: DOC_GAP
    confidence: heuristic
    auto_fixable: true
    evidence:
      source_file: accessibility.md
      location: "## WCAG 2.1 AA Checklist, line 115"
      finding: "The 1.4.3 Contrast cell says 'review contrast for disabled state (#8d8b7e on #c8c8bd)' but does not provide the actual ratio or PASS/FAIL verdict. Disabled text contrast is commonly a failure point."
    fix_action: "Calculate contrast ratio for #8d8b7e on #c8c8bd (approx 1.9:1 — likely FAIL for AA body text at 3:1 required, but disabled states are exempt under WCAG 1.4.3 exception) and document the exemption explicitly"
    blocks: []
    dependency: []

  - id: GAP-011
    dimension: anatomy_structure
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: tokens.md
      location: "## Size variants table, lines 79–84"
      finding: "Medium and Small input box heights are marked as approximate ('~56px', '~22px'). Only the Large variant (112px box) was directly verified from Figma get_design_context. Medium and Small heights were extrapolated from component metadata bounding boxes."
    fix_action: "Call get_design_context on node 21562:34998 (Medium/Rest) and 21562:35010 (Small/Rest) to confirm exact padding and content area heights"
    blocks: []
    dependency: []

  - id: GAP-012
    dimension: props_completeness
    severity: minor
    type: DOC_GAP
    confidence: heuristic
    auto_fixable: true
    evidence:
      source_file: props.md
      location: "## Notes section, line 86"
      finding: "props.md notes that 'hasError toggles the error border — error message display is handled at the form-field wrapper level, not inside this component.' The Figma design actually includes an Error Area with error icon + text as part of the component anatomy. This note may create confusion about where error messages live."
    fix_action: "Clarify in props.md Notes that the Figma component includes an Error Area as part of the visual anatomy, but the Oxygen Textarea component itself does not render this — consumers must render error text externally and connect it via aria-describedby"
    blocks: []
    dependency:
      - GAP-003

  - id: GAP-013
    dimension: figma_alignment
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: true
    evidence:
      source_file: props.md
      location: "## resize values table, lines 70–79"
      finding: "props.md documents the 'resize' prop (CSS resize behavior). Figma has a 'Resize grip' boolean toggle that shows/hides a visual grip image at the bottom-right corner. The relationship between these two is not explained — a consumer might think the Figma 'Resize grip' maps to the resize prop."
    fix_action: "Add a note under the resize prop in props.md clarifying that Figma's 'Resize grip' is a visual design element only; the resize prop controls CSS resize behavior, not grip visibility"
    blocks: []
    dependency: []

warnings:
  - id: WARN-001
    confidence: heuristic
    finding: "examples.md discloses that examples were synthesized from the API (not from actual MCP Storybook stories). This is honest and correct, but the examples have not been run against a real Oxygen installation. They may contain subtle prop usage errors."
    recommendation: "Validate examples against a live Storybook or sandbox before publishing"

  - id: WARN-002
    confidence: heuristic
    finding: "accessibility.md WCAG guidance is inferred from component type (native <textarea>) since Figma had no accessibility annotations. The guidance is standard-compliant, but has not been validated against the actual Oxygen Textarea implementation (e.g., whether aria-label/aria-labelledby are correctly passed through)."
    recommendation: "Test accessibility guidance against the live component with VoiceOver or NVDA before publishing"
---

# TextArea — Documentation Audit

**Verdict: NO** — 3 unresolved CONFLICTs between Figma variant axes and Oxygen API must be resolved before doc-rewrite can proceed.

---

## File inventory

| File | Status | Severity if absent |
|------|--------|--------------------|
| `props.md` | ✅ Present | — |
| `examples.md` | ✅ Present | — |
| `tokens.md` | ✅ Present | — |
| `accessibility.md` | ✅ Present | — |
| `textarea-figma.md` | ✅ Present | — |
| `textarea-usage.md` | ❌ **Missing** | major (SOURCE_GAP — figma-extract-usage not run) |
| `textarea-pui.md` | ✅ Present (`<!-- NO RELEVANT PUI CONTEXT -->` = PASS) | — |

---

## Dimension scores

| Dimension | Score | Coverage | Notes |
|-----------|-------|----------|-------|
| Props completeness | 0.85 | 21/23 props | Missing ARIA pass-through props (aria-label, aria-invalid) |
| Examples quality | 0.78 | 7/9 scenarios | Missing accessible error pattern; examples synthesized (not MCP-sourced) |
| Tokens coverage | 0.75 | 6/8 areas | Dark mode unresolved; filled text color not verified |
| Anatomy / structure | 0.89 | 8/9 elements | Medium/Small heights approximate only |
| Accessibility | 0.78 | 7/9 criteria | Missing aria-invalid; disabled contrast ratio unverified |
| Figma alignment | 0.62 | 5/8 checks | 3 active CONFLICTs: Size / Mode / Filled variant axes |
| PUI context | 1.00 | N/A | Confirmed no relevance — PASS |

**Overall: 0.81 weighted average** _(conflicts suppress verdict regardless of score)_

---

## Gaps summary

### Blockers / Majors requiring human decision

| ID | Type | Dimension | Summary |
|----|------|-----------|---------|
| GAP-007 | **CONFLICT** | Figma alignment | `Size` variant (Large/Medium/Small) has no `size` prop in Oxygen API |
| GAP-008 | **CONFLICT** | Figma alignment | `Mode` (Light/Dark) variant has no `mode` prop — confirm theme-provider explanation |
| GAP-004 | SOURCE_GAP | Tokens | Dark mode tokens unresolved (need Figma Desktop Bridge) |
| GAP-002 | DOC_GAP | Props | ARIA pass-through props missing from props.md |
| GAP-003 | DOC_GAP | Accessibility | `aria-invalid` missing from error state guidance |
| GAP-001 | SOURCE_GAP | Usage | `textarea-usage.md` absent — figma-extract-usage not run |

### Minors (auto-fixable by doc-rewrite once conflicts resolved)

| ID | Type | Dimension | Auto-fix? | Summary |
|----|------|-----------|-----------|---------|
| GAP-009 | CONFLICT | Figma alignment | No | `Filled` variant has no prop — confirm derived state |
| GAP-005 | DOC_GAP | Examples | Yes | Bare error example needs accessible pattern |
| GAP-006 | DOC_GAP | Tokens | No | Filled=True text color not verified |
| GAP-010 | DOC_GAP | Accessibility | Yes | Disabled contrast ratio unverified (WCAG exemption applies) |
| GAP-011 | SOURCE_GAP | Anatomy | No | Medium/Small heights approximate only |
| GAP-012 | DOC_GAP | Props | Yes | Error Area location note needs clarification |
| GAP-013 | DOC_GAP | Figma alignment | Yes | `resize` prop vs Figma `Resize grip` distinction unclear |

### Warnings (heuristic — advisory only)

| ID | Summary |
|----|---------|
| WARN-001 | Examples synthesized from API, not validated against live Storybook |
| WARN-002 | Accessibility guidance inferred from component type, not Figma annotations |

---

## Required actions before doc-rewrite

1. **Resolve GAP-007** (Size conflict): Confirm with component owner whether `size` is an undocumented/planned prop or whether sizing is intentionally rows/cols only.
2. **Resolve GAP-008** (Mode conflict): Confirm dark mode is theme-provider controlled only — add a one-line note to props.md if so (this is auto-fixable once confirmed).
3. **Resolve GAP-009** (Filled conflict): Confirm `Filled=True` maps to `value !== ''` — no prop needed, just documentation.
4. **Run figma-extract-usage** (GAP-001): Execute the `figma-extract-usage` skill to produce `textarea-usage.md` with Do/Don't guidelines.

Once the 3 conflicts are resolved and textarea-usage.md is produced, **verdict upgrades to YES** and doc-rewrite can proceed. GAP-002, GAP-003, GAP-005, GAP-010, GAP-012, GAP-013 are all auto-fixable by doc-rewrite.

---

## Next action

```
Resolve CONFLICTs → re-run doc-audit → then doc-rewrite
```

Or if conflicts are immediately answerable:
- GAP-008 (Mode): almost certainly theme-provider → mark resolved, add note
- GAP-009 (Filled): almost certainly derived state → mark resolved
- GAP-007 (Size): requires component owner input

_Source: doc-audit skill v1.0 · Audited 2026-04-29_
