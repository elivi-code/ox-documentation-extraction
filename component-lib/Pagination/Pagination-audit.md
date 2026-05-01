---
rubric_version: "1.0"
component: Pagination
package: "@8x8/oxygen-pagination"
extracted: "2026-05-01"
audited: "2026-05-01"

verdict: "NO"
verdict_reason: "2 CONFLICTs must be resolved by a human before doc-rewrite can proceed."

scores:
  props:         { score: 0.80, coverage: "8/10" }
  examples:      { score: 0.63, coverage: "5/8"  }
  tokens:        { score: 0.22, coverage: "2/9"  }
  accessibility: { score: 0.78, coverage: "7/9"  }
  figma:         { score: 0.78, coverage: "7/9"  }
  usage:         { score: 0.00, coverage: "0/7"  }
  pui:           { score: 1.00, coverage: "N/A — confirmed no PUI context" }

counts:
  doc_gaps:    4
  source_gaps: 11
  conflicts:   2
  warnings:    2

files_present:
  - props.md
  - examples.md
  - tokens.md
  - accessibility.md
  - Pagination-figma.md
  - figma-screenshot-Pagination.png

files_missing:
  - Pagination-usage.md   # figma-extract-usage not run → SOURCE_GAP
  - Pagination-pui.md     # intentionally omitted — no PUI context confirmed → PASS

gaps:
  - id: GAP-001
    dimension: tokens
    severity: major
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: tokens.md
      location: "## Theme Tokens"
      finding: "OX MCP returned 0 results for search query 'pagination'. No named theme tokens exist for this component in the Oxygen token registry."
    fix_action: "Run 'get-theme-tokens' with alternative search terms (e.g. 'select', 'ui05', 'interactive') or check if Pagination inherits tokens from Select/Button components upstream."
    blocks: [tokens.md, Pagination-spec.md]
    dependency: []

  - id: GAP-002
    dimension: tokens
    severity: major
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: Pagination-figma.md
      location: "## Gaps & conflicts → Incomplete data"
      finding: "figma_get_variables failed — token collection data unavailable. figma_get_styles returned empty. Tokens were extracted only from inline CSS variable references in the design context code output."
    fix_action: "Enable Figma Desktop Bridge plugin or ensure FIGMA_ACCESS_TOKEN has Variables API access to retrieve the full variable collection."
    blocks: [tokens.md, Pagination-spec.md]
    dependency: []

  - id: GAP-003
    dimension: tokens
    severity: major
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: true
    evidence:
      source_file: Pagination-figma.md
      location: "## Color & token bindings"
      finding: "tokens.md contains no token data. Pagination-figma.md documents --text/textcolor01, --ui/ui05, --interactive/disabled01, --interactive/disabled04, --typography/body01/*, --typography/label01/* — these are not reflected in tokens.md."
    fix_action: "doc-rewrite should pull color/typography tokens from Pagination-figma.md '## Color & token bindings' and '## Text styles' into tokens.md."
    blocks: [Pagination-spec.md]
    dependency: []

  - id: GAP-004
    dimension: props
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: props.md
      location: "### PaginationSize"
      finding: "OX MCP returned type 'PaginationSize' without expanding the enum values. props.md records the inferred values ('default', 'small') confirmed via usage docs and Figma, but these are not from the MCP type definition."
    fix_action: "Look up PaginationSize enum in the @8x8/oxygen-pagination package source to confirm exact string values."
    blocks: [props.md, Pagination-spec.md]
    dependency: []

  - id: GAP-005
    dimension: props
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: true
    evidence:
      source_file: props.md
      location: "## Props table"
      finding: "MCP returned empty description strings for: canGoBack, canGoNext, numberOfPages, pageNumber, rowsPerPage, rowsPerPageOptions, size. props.md fills these with inferred descriptions; they are not verbatim from the source."
    fix_action: "doc-rewrite may use inferred descriptions; flag inferred fields with a note for human review."
    blocks: [Pagination-spec.md]
    dependency: []

  - id: GAP-006
    dimension: examples
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: examples.md
      location: "## Basic Usage"
      finding: "Only 1 code example returned by OX MCP (BasicUsage). No example for disabled state, dark mode, or size=small with all required props."
    fix_action: "Add examples to Storybook or MCP source for disabled, small, and dark variants."
    blocks: [examples.md, Pagination-spec.md]
    dependency: []

  - id: GAP-007
    dimension: examples
    severity: minor
    type: DOC_GAP
    confidence: heuristic
    auto_fixable: true
    evidence:
      source_file: examples.md
      location: "## Sizes"
      finding: "The small size example shows only the size prop without all required props, making the snippet non-functional as shown."
    fix_action: "doc-rewrite should expand size example to include all required props (canGoBack, canGoNext, etc.) so it is copy-pasteable."
    blocks: [Pagination-spec.md]
    dependency: []

  - id: GAP-008
    dimension: accessibility
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: accessibility.md
      location: "top-level note"
      finding: "All accessibility content is inferred from component type and standard patterns. Neither OX MCP nor Figma annotations provided explicit a11y data."
    fix_action: "Designer should add ARIA role, focus order, and keyboard interaction annotations to the Figma component. Oxygen team should add a11y guidance to MCP documentation."
    blocks: [accessibility.md]
    dependency: []

  - id: GAP-009
    dimension: figma
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: Pagination-figma.md
      location: "## Accessibility (from Figma annotations only)"
      finding: "No ARIA role, focus order, or keyboard interaction annotations in Figma. Marked '<!-- NOT ANNOTATED IN FIGMA -->'."
    fix_action: "Designer to add accessibility annotations to the Pagination component set in Figma."
    blocks: [Pagination-figma.md]
    dependency: []

  - id: GAP-010
    dimension: figma
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: Pagination-figma.md
      location: "## Interaction states"
      finding: "No hover, focus, or pressed states in the Figma component set. Only Default and Disabled variants present."
    fix_action: "Designer to add transient state variants (hover, focus-visible, pressed) to the Figma component set."
    blocks: [Pagination-figma.md]
    dependency: []

  - id: GAP-011
    dimension: figma
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: Pagination-figma.md
      location: "## Gaps & conflicts → figma_get_component_details failed"
      finding: "figma_get_component_details requires Figma Desktop Bridge. Full variant key map and component key were not retrieved."
    fix_action: "Re-run figma-extract with Figma Desktop Bridge plugin active to obtain component key and full variant map."
    blocks: []
    dependency: []

  - id: GAP-012
    dimension: tokens
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: Pagination-figma.md
      location: "## Color & token bindings → Token coverage"
      finding: "10 hardcoded values flagged: Select widths (88px/72px), container widths (640px/547px/288px), button padding (10px/6px/4px), border-radius (6px). None have token bindings."
    fix_action: "Design system team to evaluate whether these dimensions should be tokenised; until tokenised this is expected behaviour (not a doc gap)."
    blocks: []
    dependency: []

  - id: GAP-013
    dimension: usage
    severity: major
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: "Pagination-usage.md"
      location: "file missing"
      finding: "Pagination-usage.md does not exist. figma-extract-usage skill was not run. Do/Don't editorial guidance from Figma 'Pagination — Examples' page is absent."
    fix_action: "Run figma-extract-usage for Pagination if a 'Pagination — Examples' Figma page exists. If no such page exists, note as SOURCE_GAP and proceed."
    blocks: [Pagination-spec.md]
    dependency: []

  - id: GAP-014
    dimension: tokens
    severity: minor
    type: SOURCE_GAP
    confidence: heuristic
    auto_fixable: false
    evidence:
      source_file: Pagination-figma.md
      location: "## Gaps & conflicts"
      finding: "figma_get_styles returned 0 styles from the file. Cannot confirm whether the typography tokens (typography/body01/*, typography/label01/*) resolve to named library styles."
    fix_action: "Verify typography token names against the Oxygen design system style library when Figma API access improves."
    blocks: []
    dependency: []

conflicts:
  - id: CON-001
    dimension: figma
    severity: major
    type: CONFLICT
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: Pagination-figma.md
      location: "## API — Variant axes → breakpoint"
      finding: "Figma has a 'breakpoint' variant axis with values '> 548px' and '< 548px'. This axis controls visibility of the rows-per-page section. The Oxygen React prop API (@8x8/oxygen-pagination) has no 'breakpoint' prop — responsive layout is expected to be managed by the consuming application."
    fix_action: "Human decision required: (A) Document as consumer responsibility in the spec — no React prop, consumer controls responsive layout via CSS/container queries. (B) Raise with Oxygen team whether a responsive prop should be added. Resolve before doc-rewrite to determine spec wording."
    blocks: [Pagination-spec.md]
    dependency: []

  - id: CON-002
    dimension: figma
    severity: major
    type: CONFLICT
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: Pagination-figma.md
      location: "## API — Boolean toggles → rowsPerPage"
      finding: "Figma has a 'rowsPerPage' boolean toggle that shows/hides the entire rows-per-page section. The Oxygen prop 'rowsPerPageOptions: number[]' is an array of values — it implies the section renders when the array is provided, but the semantics differ. Figma models it as a visibility toggle; React models it as a data provider."
    fix_action: "Human decision required: Confirm whether passing an empty array or omitting 'rowsPerPageOptions' hides the rows-per-page section (matching Figma intent). Document the mapping in the spec. Resolve before doc-rewrite."
    blocks: [Pagination-spec.md]
    dependency: []

warnings:
  - id: WARN-001
    dimension: accessibility
    confidence: heuristic
    finding: "accessibility.md is comprehensive but entirely inferred. The ARIA labels suggested (e.g. aria-label='Pagination') may not match actual component implementation. Spot-check against rendered DOM before publishing."

  - id: WARN-002
    dimension: tokens
    confidence: heuristic
    finding: "Token values in Pagination-figma.md were extracted from inline CSS variable fallback values in the Figma design context code (e.g. '--text/textcolor01, #26252a'). The token names are likely correct but the hex fallbacks may differ from actual resolved values in the theme. Verify against the Oxygen token library."
---

# Pagination — Doc Audit

**Verdict: NO** — 2 conflicts must be resolved by a human before `doc-rewrite` can run.

---

## File inventory

| File | Status | Notes |
|------|--------|-------|
| `props.md` | ✅ present | 11 props, usePagination hook, install/import snippets |
| `examples.md` | ✅ present | 1 functional example; anatomy, sizes, when-to-use |
| `tokens.md` | ✅ present | Nearly empty — MCP returned 0 tokens; size table only |
| `accessibility.md` | ✅ present | Comprehensive but entirely inferred — no MCP or Figma source |
| `Pagination-figma.md` | ✅ present | Anatomy, 4 variant axes, color tokens, structure, 2 conflicts logged |
| `figma-screenshot-Pagination.png` | ✅ present | Downloaded |
| `Pagination-usage.md` | ❌ missing | figma-extract-usage not run → GAP-013 |
| `Pagination-pui.md` | ⏭ skipped | pui-mcp-extract confirmed no relevant context → PASS |

---

## Dimension scores

| Dimension | Score | Coverage | Summary |
|-----------|-------|----------|---------|
| Props | 0.80 | 8/10 | All props present; PaginationSize enum undocumented; descriptions inferred for 6 props |
| Examples | 0.63 | 5/8 | 1 complete example; missing disabled, small (complete), dark mode |
| Tokens | 0.22 | 2/9 | MCP returned 0 tokens; Figma tokens identified but not in tokens.md; 10 hardcoded values |
| Accessibility | 0.78 | 7/9 | Full WCAG checklist + keyboard + ARIA; all inferred, no upstream source |
| Figma | 0.78 | 7/9 | Anatomy, variants, tokens, structure complete; missing styles API, variables, hover states |
| Usage | 0.00 | 0/7 | File missing — figma-extract-usage not run |
| PUI | 1.00 | N/A | Confirmed no relevant PUI context |

---

## Conflicts (must resolve before rewrite)

### CON-001 — `breakpoint` Figma axis has no React prop

**Dimension:** figma · **Severity:** major

Figma models a `breakpoint` variant axis (`> 548px` / `< 548px`) that hides the rows-per-page section on small screens. The `@8x8/oxygen-pagination` React component has no corresponding prop.

**Decision required:** Choose one:
- **(A)** Document responsive behaviour as consumer's responsibility — no React prop, consumer wraps/conditionally renders. This is the most likely intended design.
- **(B)** Escalate to Oxygen team to add a `breakpoint` or `hideRowsPerPage` prop.

---

### CON-002 — `rowsPerPage` Figma boolean ≠ `rowsPerPageOptions` React prop

**Dimension:** figma · **Severity:** major

Figma shows a `rowsPerPage: boolean` toggle that shows/hides the rows-per-page section. The React prop `rowsPerPageOptions: number[]` provides the list of options — its absence likely hides the section, but this is not documented.

**Decision required:** Confirm: does omitting `rowsPerPageOptions` (or passing `[]`) cause the rows-per-page section to not render? Document this mapping explicitly in the spec.

---

## Doc gaps (auto-fixable by doc-rewrite)

| ID | Dimension | Severity | Finding |
|----|-----------|----------|---------|
| GAP-003 | tokens | major | Figma tokens (--text/textcolor01, --ui/ui05, --interactive/disabled01/04, typography/*) documented in Pagination-figma.md but absent from tokens.md |
| GAP-005 | props | minor | 6 required props have empty MCP descriptions; inferred descriptions used |
| GAP-007 | examples | minor | Small size snippet is non-functional (missing all required props) |

## Source gaps (need upstream work)

| ID | Dimension | Severity | Finding |
|----|-----------|----------|---------|
| GAP-001 | tokens | major | OX MCP returns 0 theme tokens for "pagination" |
| GAP-002 | tokens | major | Figma Variables API unavailable — token collection data missing |
| GAP-004 | props | minor | PaginationSize enum values inferred, not from MCP source |
| GAP-006 | examples | minor | No disabled or dark-mode code examples in MCP |
| GAP-008 | accessibility | minor | No a11y data from MCP or Figma annotations — all inferred |
| GAP-009 | figma | minor | No accessibility annotations in Figma file |
| GAP-010 | figma | minor | No hover/focus/pressed states in Figma variant set |
| GAP-011 | figma | minor | figma_get_component_details unavailable (Desktop Bridge) |
| GAP-012 | tokens | minor | 10 hardcoded values in Figma with no token bindings |
| GAP-013 | usage | major | Pagination-usage.md missing — figma-extract-usage not run |
| GAP-014 | tokens | minor | figma_get_styles returned empty — typography style names unverified |

---

## Warnings (heuristic — advisory only)

| ID | Finding |
|----|---------|
| WARN-001 | accessibility.md is entirely inferred. Spot-check ARIA labels against rendered DOM before publishing. |
| WARN-002 | Token hex fallbacks extracted from Figma design context may differ from resolved theme values. Verify against Oxygen token library. |

---

## Suggested next actions

1. **Resolve CON-001** — Decide whether `breakpoint` behaviour is a consumer concern or a new prop. Update the spec wording accordingly.
2. **Resolve CON-002** — Confirm that omitting `rowsPerPageOptions` hides the rows-per-page UI section; document the mapping.
3. **Run `figma-extract-usage`** (GAP-013) — Check if a "Pagination — Examples" Figma page exists and run the skill.
4. **After conflicts resolved** — Run `doc-rewrite` to produce `Pagination-spec.md`. It can auto-fix GAP-003, GAP-005, GAP-007.
