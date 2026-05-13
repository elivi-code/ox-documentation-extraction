---
rubric_version: "1.0"
component: Input
extracted: "2026-04-29"
audit_date: "2026-04-29"
auditor: doc-audit skill

files_found:
  - props.md
  - examples.md
  - tokens.md
  - accessibility.md
  - Input-figma.md
  - Input-pui.md
  - Input-usage.md   # editorial draft added 2026-05-13 (mirrors published docs page)

files_missing: []

verdict: "NO"
verdict_reason: "1 CONFLICT present — resolve Search input isReadOnly discrepancy before doc-rewrite"

scores:
  props_api:       { score: 0.82, coverage: "9/11" }
  examples:        { score: 0.83, coverage: "10/12" }
  design_tokens:   { score: 0.45, coverage: "5/11" }
  accessibility:   { score: 0.91, coverage: "10/11" }
  figma_spec:      { score: 0.87, coverage: "13/15" }
  usage_do_dont:   { score: 0.85, coverage: "1/1"  }  # Editorial Input-usage.md added 2026-05-13 — mirrors published docs page; 8 Do/Don't pairs derived from docs + extracted artefacts. Score capped below 1.0 because pairs are editorial, not from a Figma "↳ Input examples" Do/Don't page.
  pui_context:     { score: 1.00, coverage: "n/a — NO RELEVANT PUI CONTEXT marker present" }

overall_score: 0.82  # Recalculated 2026-05-13 after editorial Input-usage.md (mirrors docs page) added — usage dimension lifted from 0.00 to 0.85; verdict still NO until CONFLICT-001 resolved.

counts:
  doc_gaps: 4
  source_gaps: 12  # GAP-016 resolved 2026-05-13; GAP-017 added (Text area + Search input usage scope)
  conflicts: 1
  warnings: 4

gaps:
  - id: GAP-001
    dimension: props_api
    severity: minor
    type: DOC_GAP
    confidence: heuristic
    auto_fixable: true
    evidence:
      source_file: props.md
      location: "## Props table, Default column"
      finding: "All 16 props show '—' for default. OX MCP returned no default values. Defaults for boolean flags (isDisabled, isReadOnly, hasError, etc.) are implicitly false but not stated."
    fix_action: "Add implicit defaults (false for booleans, undefined for optionals) to the props table in props.md"
    blocks: [storybook-args, docusaurus-props-table]
    dependency: []

  - id: GAP-002
    dimension: props_api
    severity: major
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: props.md
      location: "## Props table, Description column"
      finding: "6 props have empty descriptions as returned by OX MCP: size, suffix, focus, fixed, autoSuffixWidth, autoPrefixWidth"
    fix_action: "Add descriptions for size, suffix, focus, fixed, autoSuffixWidth, autoPrefixWidth — requires OX source code or README review"
    blocks: [docusaurus-props-table]
    dependency: []

  - id: GAP-003
    dimension: examples
    severity: major
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: examples.md
      location: "Footer note"
      finding: "OX MCP get-component-examples returned 0 clean Storybook snippets. All examples are hand-derived from prop API and Figma annotations — not verified against actual component runtime."
    fix_action: "Retrieve live Storybook examples from oxygen.8x8.com or component source; add verified snippets to examples.md"
    blocks: [storybook-generate]
    dependency: []

  - id: GAP-004
    dimension: examples
    severity: minor
    type: DOC_GAP
    confidence: heuristic
    auto_fixable: true
    evidence:
      source_file: examples.md
      location: "Missing section"
      finding: "No example for Search input variant. Figma documents a distinct Search input component set with a leading search icon, but examples.md only covers the text input API."
    fix_action: "Add Search input example showing iconLeft=SearchIcon + type='search' pattern"
    blocks: []
    dependency: []

  - id: GAP-005
    dimension: examples
    severity: minor
    type: DOC_GAP
    confidence: heuristic
    auto_fixable: true
    evidence:
      source_file: examples.md
      location: "Missing section"
      finding: "autoPrefixWidth prop is documented in props.md but no prefix usage example exists in examples.md"
    fix_action: "Add prefix example alongside the suffix example in examples.md"
    blocks: []
    dependency: []

  - id: GAP-006
    dimension: design_tokens
    severity: major
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: tokens.md
      location: "## Tokens not captured"
      finding: "Focus ring / border color token not captured. Variables API was unavailable (REST API permission error; Desktop Bridge not connected)."
    fix_action: "Re-run figma-extract with Desktop Bridge running in Figma Desktop to retrieve variable bindings; add focus ring token to tokens.md"
    blocks: [docusaurus-tokens-table, storybook-theming]
    dependency: []

  - id: GAP-007
    dimension: design_tokens
    severity: major
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: tokens.md
      location: "## Tokens not captured"
      finding: "Error border color token not captured (Variables API unavailable)."
    fix_action: "Re-run figma-extract with Variables API access; add error border token to tokens.md"
    blocks: [docusaurus-tokens-table]
    dependency: []

  - id: GAP-008
    dimension: design_tokens
    severity: major
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: tokens.md
      location: "## Tokens not captured"
      finding: "Disabled state background token not captured."
    fix_action: "Re-run figma-extract with Variables API access; add disabled background token to tokens.md"
    blocks: [docusaurus-tokens-table]
    dependency: []

  - id: GAP-009
    dimension: design_tokens
    severity: major
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: tokens.md
      location: "## Tokens not captured"
      finding: "Read-only state background token not captured."
    fix_action: "Re-run figma-extract with Variables API access; add read-only background token to tokens.md"
    blocks: [docusaurus-tokens-table]
    dependency: []

  - id: GAP-010
    dimension: design_tokens
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: tokens.md
      location: "## Text color tokens, textColor02 row"
      finding: "textColor02 dark mode value not captured — cell shows '*(dark value not captured)*'"
    fix_action: "Re-run figma-extract with Variables API; populate textColor02 dark value in tokens.md"
    blocks: []
    dependency: []

  - id: GAP-011
    dimension: design_tokens
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: tokens.md
      location: "## Error tokens, error01 row"
      finding: "error01 dark mode value not captured — cell shows '*(dark value not captured)*'"
    fix_action: "Re-run figma-extract with Variables API; populate error01 dark value in tokens.md"
    blocks: []
    dependency: []

  - id: GAP-012
    dimension: accessibility
    severity: minor
    type: DOC_GAP
    confidence: heuristic
    auto_fixable: true
    evidence:
      source_file: accessibility.md
      location: "## Color contrast table, Placeholder text row"
      finding: "Placeholder text contrast ratio (#6C6862 on #F4F3EE) is flagged as '⚠ Verify' but the actual calculated ratio is not provided."
    fix_action: "Calculate contrast ratio for #6C6862 / #F4F3EE and document the result; flag as FAIL if < 4.5:1"
    blocks: [docusaurus-accessibility]
    dependency: []

  - id: GAP-013
    dimension: accessibility
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: accessibility.md
      location: "## Color contrast table, Focus ring row"
      finding: "Focus ring color token is unknown (GAP-006); cannot verify 1.4.11 Non-text contrast criterion."
    fix_action: "Resolve GAP-006 first, then verify focus ring contrast and update accessibility.md checklist"
    blocks: []
    dependency: [GAP-006]

  - id: GAP-014
    dimension: figma_spec
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: Input-figma.md
      location: "## Color & token bindings, Effect styles section"
      finding: "figma_get_styles returned 0 styles. Effect styles (shadows etc.) not documented."
    fix_action: "Re-run figma_get_styles with Desktop Bridge connected; add any effect styles found to Input-figma.md"
    blocks: []
    dependency: []

  - id: GAP-015
    dimension: figma_spec
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: Input-figma.md
      location: "action_required warning in figma_get_component response"
      finding: "Figma component description field was not reliably retrieved (REST API known bug; requires Desktop Bridge). Documentation link points to oxygen.8x8.com/docs/Contribution/intro which is a generic URL, not component-specific."
    fix_action: "Run figma_get_component with Desktop Bridge running to retrieve accurate component description; update figma.md description"
    blocks: []
    dependency: []

  - id: GAP-016
    dimension: usage_do_dont
    severity: minor   # Was major; downgraded 2026-05-13 — editorial Input-usage.md now mirrors published docs page
    type: DOC_GAP    # Was SOURCE_GAP; flipped because the missing artefact is the editorial doc, which has now been authored
    confidence: deterministic
    auto_fixable: true   # Resolved by hand on 2026-05-13
    status: resolved
    resolved_date: "2026-05-13"
    resolved_by: "editorial draft authored from https://oxygen.8x8.com/components/textinput/usage + extracted MCP/Figma artefacts (Claude_in_Chrome MCP)"
    evidence:
      source_file: Input-usage.md   # now present
      location: "component-lib/Input/Input-usage.md"
      finding: "Editorial Input-usage.md exists (mirrors published docs page; 8 Do/Don't pairs derived from docs + extracted artefacts). Figma '↳ Input examples' page with Do/Don't card frames remains absent — re-run figma-extract-usage if such a page is ever created."
    fix_action: "(resolved by editorial authorship 2026-05-13) — replace with figma-extract-usage output if a Figma '↳ Input examples' page with Do/Don't card frames is created upstream."
    blocks: []
    dependency: []

  - id: GAP-017
    dimension: usage_do_dont
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    introduced: "2026-05-13"
    evidence:
      source_file: Input-usage.md
      location: "frontmatter `scope:` + Gaps table"
      finding: "Input-usage.md is scoped to Text input only. Two sibling Figma component sets share the Input canvas — Text area (21562:34985) and Search input (25655:40530) — but are not covered by this usage doc. Text area has its own folder (component-lib/TextArea/); Search input has no Oxygen package of its own and is the locus of CONFLICT-001."
    fix_action: "When Search input's API is clarified (CONFLICT-001 resolved), decide whether to (a) fold Search affordances into Input-usage.md as an extended scope, or (b) author a separate Search-usage doc. TextArea usage is owned by component-lib/TextArea/."
    blocks: [docusaurus-usage-section]
    dependency: [CONFLICT-001]

conflicts:
  - id: CONFLICT-001
    dimension: props_api
    evidence:
      source_a: { file: props.md, location: "## Props table, isReadOnly row", claim: "isReadOnly prop exists on Input component" }
      source_b: { file: Input-figma.md, location: "## Gaps & conflicts table", claim: "Figma Search input component set has no Read Only variant axis; only Text input and Text area have it" }
    finding: "The OX API exposes isReadOnly on the Input component globally, but the Figma Search input component set has no corresponding Read Only variant. It is unclear whether: (a) Search input intentionally does not support read-only, (b) the Figma is incomplete, or (c) isReadOnly silently applies but lacks a Figma representation."
    fix_action: "Clarify with designer whether Search input supports isReadOnly. If yes: add Read Only variant to Figma Search input. If no: document the constraint in props.md and add note that isReadOnly is not applicable to Search input."
    blocks: [docusaurus-props-table, storybook-stories]

warnings:
  - id: WARN-001
    confidence: heuristic
    finding: "Props size, suffix, focus, fixed, autoSuffixWidth, autoPrefixWidth lack descriptions. These may have well-known semantics but should be confirmed against OX source to avoid misuse."
  - id: WARN-002
    confidence: heuristic
    finding: "Text area component is documented in Figma spec but is not explicitly covered as a separate OX component in props.md or examples.md. Verify whether TextArea is a separate OX package (@8x8/oxygen-textarea?) or a mode of the Input component."
  - id: WARN-003
    confidence: heuristic
    finding: "Search input is documented as a Figma component set but has no corresponding OX package or import in props.md. May map to Input + iconLeft=SearchIcon + type='search', or may be a separate package."
  - id: WARN-004
    confidence: heuristic
    finding: "Placeholder text contrast (#6C6862 on #F4F3EE) is a likely WCAG 1.4.3 failure risk. At estimated contrast ~3.8:1 this falls below the 4.5:1 AA threshold for normal text."
# --- navigation (added by component-map) ---
role: audit
pipeline_stage: blocked
pipeline_note: "Audit verdict NO — resolve CONFLICT-001 (Search isReadOnly) before rewrite. Editorial Input-usage.md added 2026-05-13."
siblings:
  - "[[Input/props]]"
  - "[[Input/examples]]"
  - "[[Input/tokens]]"
  - "[[Input/accessibility]]"
  - "[[Input/Input-figma]]"
  - "[[Input/Input-pui]]"
  - "[[Input/Input-usage]]"
tags:
  - oxygen
  - component/Input
  - role/audit
  - stage/blocked
---

# Input — Audit Report

**Component:** Input  
**Audit date:** 2026-04-29 *(extracted)* · **Re-audited:** 2026-05-13 *(after editorial Input-usage.md added)*  
**Rubric version:** 1.0  
**Verdict:** ❌ NO — resolve 1 conflict before doc-rewrite (CONFLICT-001)

---

## File inventory

| File | Status | Produced by |
|------|--------|-------------|
| `props.md` | ✅ Present | oxygen-mcp-extract |
| `examples.md` | ✅ Present | oxygen-mcp-extract |
| `tokens.md` | ✅ Present | oxygen-mcp-extract |
| `accessibility.md` | ✅ Present | oxygen-mcp-extract |
| `Input-figma.md` | ✅ Present | figma-extract |
| `Input-pui.md` | ✅ Present (NO RELEVANT PUI CONTEXT) | pui-mcp-extract |
| `Input-usage.md` | ✅ Present (editorial — mirrors published docs page) | hand-authored 2026-05-13 |
| `Input-usage.html` | ✅ Present (HTML render of usage doc) | hand-authored 2026-05-13 |

---

## Dimension scores

| Dimension | Score | Coverage | Status |
|-----------|-------|----------|--------|
| Props / API | 0.82 | 9/11 | ⚠ Major gap (empty prop descriptions) |
| Examples | 0.83 | 10/12 | ⚠ Major gap (0 Storybook snippets) |
| Design / Tokens | 0.45 | 5/11 | ❌ Multiple major gaps (Variables API unavailable) |
| Accessibility | 0.91 | 10/11 | ✅ Strong |
| Figma spec | 0.87 | 13/15 | ✅ Good |
| Usage / Do-Don't | 0.85 | 1/1 | ✅ Editorial draft present (mirrors docs page; 8 Do/Don't pairs) — capped <1.0 until Figma examples page is built |
| PUI context | 1.00 | n/a | ✅ Resolved (no relevant context) |
| **Overall** | **0.82** | | |

---

## Verdict

> ❌ **NO — resolve conflicts first**
>
> **CONFLICT-001** must be resolved before doc-rewrite can produce an authoritative spec. The `isReadOnly` prop exists in the OX API but the Search input Figma component set has no corresponding Read Only variant. This ambiguity would propagate incorrect documentation if left unresolved.
>
> ~~Once CONFLICT-001 is resolved, the main blocker for a complete doc-rewrite is **GAP-016** (`Input-usage.md` missing) and **GAP-003** (0 Storybook examples).~~ **Update 2026-05-13:** GAP-016 is now **resolved** — an editorial `Input-usage.md` (plus an HTML render) was authored on 2026-05-13 mirroring the published Oxygen docs page at `https://oxygen.8x8.com/components/textinput/usage` and cross-validated against the extracted MCP/Figma artefacts. The remaining blocker for a complete doc-rewrite is **CONFLICT-001** plus **GAP-003** (0 Storybook examples — source gap requiring upstream work). Doc-rewrite can begin on available dimensions with `PARTIAL` scope once CONFLICT-001 is closed.

---

## Conflicts (must resolve before rewrite)

### CONFLICT-001 — isReadOnly on Search input
**Dimension:** Props/API  
**Sources in conflict:**
- `props.md` — `isReadOnly` listed as a valid prop on the Input component
- `Input-figma.md` — Search input component set has no `Read Only` variant axis (only Text input and Text area have it)

**Finding:** It is unclear whether Search input intentionally omits read-only support or whether the Figma is simply incomplete.

**Fix action:** Clarify with designer. If Search input supports `isReadOnly` → add Read Only variant to Figma Search input. If not → document the constraint in `props.md` and note that `isReadOnly` does not apply to Search input.

---

## Gaps

### By severity

#### Major (6)

| ID | Dimension | Type | Finding |
|----|-----------|------|---------|
| GAP-002 | Props/API | SOURCE_GAP | 6 props have empty OX descriptions (`size`, `suffix`, `focus`, `fixed`, `autoSuffixWidth`, `autoPrefixWidth`) |
| GAP-003 | Examples | SOURCE_GAP | OX MCP returned 0 Storybook snippets — all examples are hand-derived |
| GAP-006 | Design/Tokens | SOURCE_GAP | Focus ring color token missing (Variables API unavailable) |
| GAP-007 | Design/Tokens | SOURCE_GAP | Error border color token missing |
| GAP-008 | Design/Tokens | SOURCE_GAP | Disabled state background token missing |
| GAP-009 | Design/Tokens | SOURCE_GAP | Read-only state background token missing |

#### Minor (10)

| ID | Dimension | Type | Finding |
|----|-----------|------|---------|
| GAP-001 | Props/API | DOC_GAP | All props show `—` for default; implicit booleans default to `false` but not stated |
| GAP-004 | Examples | DOC_GAP | No Search input example in examples.md |
| GAP-005 | Examples | DOC_GAP | No prefix/autoPrefixWidth example |
| GAP-010 | Design/Tokens | SOURCE_GAP | `textColor02` dark mode value not captured |
| GAP-011 | Design/Tokens | SOURCE_GAP | `error01` dark mode value not captured |
| GAP-012 | Accessibility | DOC_GAP | Placeholder contrast ratio calculated but not verified (#6C6862 on #F4F3EE) |
| GAP-013 | Accessibility | SOURCE_GAP | Focus ring contrast cannot be verified (depends on GAP-006) |
| GAP-014 | Figma spec | SOURCE_GAP | Effect styles returned 0 from Figma |
| GAP-015 | Figma spec | SOURCE_GAP | Component description unreliable (Desktop Bridge not running during extraction) |
| GAP-017 | Usage/Do-Don't | SOURCE_GAP | Text area + Search input usage docs absent — Input-usage.md is scoped to Text input only (added 2026-05-13). Text area has its own folder; Search input shares the API surface but lacks a Read Only Figma variant (CONFLICT-001). Document Search separately when its API is clarified. |

#### Resolved (1) — historical record

| ID | Resolution |
|----|-----------|
| GAP-016 | ~~`Input-usage.md` entirely missing~~ → **Resolved 2026-05-13** by editorial authorship (mirrors published Oxygen docs page at `https://oxygen.8x8.com/components/textinput/usage`, fetched via Claude_in_Chrome MCP; 8 Do/Don't pairs cross-validated against extracted artefacts; HTML render also written). Replace with `figma-extract-usage` output if a Figma `↳ Input examples` page with Do/Don't card frames is ever created. |

---

## Warnings (heuristic — advisory only)

| ID | Finding |
|----|---------|
| WARN-001 | Props `size`, `suffix`, `focus`, `fixed`, `autoSuffixWidth`, `autoPrefixWidth` lack descriptions — confirm semantics against OX source |
| WARN-002 | Text area is documented in Figma but unclear if it maps to the Input package or a separate `@8x8/oxygen-textarea` package |
| WARN-003 | Search input is documented in Figma but has no OX package/import — likely `Input + iconLeft + type='search'`; verify |
| WARN-004 | Placeholder text contrast (#6C6862 on #F4F3EE) is a likely WCAG AA failure (~3.8:1 estimated, below 4.5:1 threshold) |

---

## Recommended actions (priority order)

1. **Resolve CONFLICT-001** — Clarify with designer whether Search input supports `isReadOnly`. Unblocks doc-rewrite.
2. **Re-run `figma-extract` with Desktop Bridge** (GAP-006–011, 014–015) — Unlocks variable bindings for focus ring, error border, disabled/read-only backgrounds, and dark-mode token values.
3. **Retrieve OX prop descriptions** (GAP-002) — Check `@8x8/oxygen-input` README or source code for descriptions of `size`, `suffix`, `focus`, `fixed`, `autoSuffixWidth`, `autoPrefixWidth`.
4. **Add Storybook snippets** (GAP-003) — Run component in Storybook at oxygen.8x8.com and extract verified code examples.
5. **Verify placeholder contrast** (WARN-004, GAP-012) — Calculate #6C6862 / #F4F3EE ratio; flag WCAG failure if confirmed.
6. **Clarify TextArea and Search input as OX packages** (WARN-002, WARN-003, GAP-017) — Determine if separate packages exist; either document Search separately or fold its affordances into Input docs.
7. **(Optional, when a Figma `↳ Input examples` page is created)** — Run `figma-extract-usage` to replace the editorial `Input-usage.md` with Figma-sourced Do/Don't cards.

---

## Auto-fixable gaps (doc-rewrite can handle without human input)

| ID | Action |
|----|--------|
| GAP-001 | Add implicit boolean defaults (`false`) to props table |
| GAP-004 | Add Search input code example |
| GAP-005 | Add prefix/autoPrefixWidth example |
| GAP-012 | Calculate and document placeholder contrast ratio |

---

_Source: doc-audit skill · Rubric v1.0 · Initial audit 2026-04-29 · **Re-audited 2026-05-13** after editorial Input-usage.md added_
