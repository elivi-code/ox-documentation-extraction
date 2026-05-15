---
component: TextField
rubric_version: "1.0"
audit_date: "2026-05-15"
auditor: doc-audit skill (claude-opus-4-7)
verdict: "YES"
verdict_reason: "No CONFLICTs. No blocker-severity gaps. 4 major gaps remaining (was 5 — usage source gap demoted to minor after TextField-usage.md editorial draft landed). Doc-rewrite can proceed; dark-mode visual specs still pending source data."

files_found:
  - props.md
  - examples.md
  - tokens.md
  - accessibility.md
  - figma.md
  - TextField-pui.md
  - TextField-usage.md

files_missing:
  - TextField-figma.md   # present as figma.md — naming convention violation only

scores:
  props:         { coverage: "7/9",   score: 0.78 }
  examples:      { coverage: "10/14", score: 0.71 }
  tokens:        { coverage: "9/12",  score: 0.75 }
  accessibility: { coverage: "12/15", score: 0.80 }
  figma:         { coverage: "11/15", score: 0.73 }
  usage:         { coverage: "1/1",   score: 0.70 }
  pui:           { coverage: "1/1",   score: 1.00 }

overall_score: 0.78

gap_counts:
  blockers:  0
  major:     4
  minor:     9
  conflicts: 0
  warnings:  5

gaps:
  - id: GAP-001
    dimension: usage
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: TextField-usage.md
      location: "frontmatter `source_type: editorial`; `<!-- FIGMA EXAMPLES PAGE: absent -->`"
      finding: "TextField-usage.md exists as an editorial draft authored from extracted artifacts and oxygen.8x8.com/components/textinput/usage. No Figma `↳ TextField examples` page exists, so figma-extract-usage cannot run. Do/Don't pairs are provisional and need designer review."
    fix_action: "Create a Figma `↳ TextField examples` page with Do/Don't frames, then run figma-extract-usage to replace the editorial draft with canonical pairs."
    blocks: []
    dependency: []

  - id: GAP-002
    dimension: props
    severity: major
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: props.md
      location: "## Type references, line 79"
      finding: "`ActionTarget` type is documented as `/* resolved from ActionTarget — likely '_blank' | '_self' | '_parent' | '_top' */`. This is a guess, not a verified type. The actual union members are unknown."
    fix_action: "Look up ActionTarget in the @8x8/oxygen-text-field package source and replace the comment with the real union type values."
    blocks:
      - props table completeness
      - TypeScript consumer correctness
    dependency: []

  - id: GAP-003
    dimension: props
    severity: major
    type: DOC_GAP
    confidence: heuristic
    auto_fixable: false
    evidence:
      source_file: props.md
      location: "Rows otherInputProps / otherLabelProps / otherActionProps (lines 64–66)"
      finding: "Three props — otherInputProps, otherLabelProps, otherActionProps — have empty descriptions in the MCP response and are labelled 'Alternative pass-through' with no indication of whether they are deprecated, superseded by inputProps/labelProps/actionProps, or a parallel API. Their intended use is unknown."
    fix_action: "Verify deprecation status of otherInputProps / otherLabelProps / otherActionProps in the package source; add a deprecation notice if applicable, or add a usage description if they serve a distinct purpose."
    blocks:
      - props table accuracy
      - consumer guidance
    dependency: []

  - id: GAP-004
    dimension: examples
    severity: major
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: true
    evidence:
      source_file: examples.md
      location: "## Error state (lines 40–49)"
      finding: "The error state example sets `hasError` and passes the error message via `description`. Figma shows the error message renders in a dedicated 'Error Area' (icon + red text), separate from hint text. In the Oxygen component `description` is the hint/helper text prop. Using `description` for an error message is incorrect — there is no example showing how to display the actual error message string (which appears to require a separate prop or pattern not yet documented)."
    fix_action: "Investigate how the error message text is passed to the component (separate prop vs description, or aria pattern) and update the error state example accordingly. If no prop exists, document the recommended pattern."
    blocks:
      - storybook error example
      - docusaurus error state docs
    dependency: []

  - id: GAP-005
    dimension: figma
    severity: major
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: figma.md
      location: "## Visual states (all state sections)"
      finding: "All visual state descriptions and screenshots are Light mode only. The Figma canvas has a full Dark mode variant set (68 dark symbols across the three component families) but no dark-mode state specifications, tokens, or screenshots were captured."
    fix_action: "Re-run Figma extraction targeting dark-mode symbol nodes (e.g. node 22155:36800 for Dark/Large/Rest) to capture dark-mode visual specs and screenshots."
    blocks:
      - dark mode design spec
      - storybook dark theme story
    dependency: []

  - id: GAP-006
    dimension: figma
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: true
    evidence:
      source_file: figma.md
      location: "File name on disk: figma.md"
      finding: "The expected file name per the pipeline convention is TextField-figma.md. The file exists with correct content but wrong name. This will cause doc-audit and doc-rewrite to report it as missing unless the naming is corrected."
    fix_action: "Rename figma.md to TextField-figma.md in component-lib/TextField/."
    blocks:
      - doc-rewrite file lookup
    dependency: []

  - id: GAP-007
    dimension: tokens
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: tokens.md
      location: "## Text tokens, --text/textColor02 row"
      finding: "--text/textColor02 dark mode value is listed as '—' (unknown). The MCP token search for 'input' only returned the light value (#6C6862 implied from Figma). Dark mode value not retrieved from OX token API."
    fix_action: "Run get-theme-tokens with search='textColor02' to retrieve the dark mode value and update tokens.md."
    blocks:
      - dark mode token table completeness
    dependency: []

  - id: GAP-008
    dimension: tokens
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: tokens.md
      location: "## Error tokens, --error/error01 row"
      finding: "--error/error01 dark mode value is listed as '—' (unknown). Only extracted from Figma code snippets (light mode #CB2233). Dark value not retrieved from OX token API."
    fix_action: "Run get-theme-tokens with search='error01' to retrieve the dark mode error colour and update tokens.md."
    blocks:
      - dark mode token table completeness
    dependency: []

  - id: GAP-009
    dimension: tokens
    severity: minor
    type: DOC_GAP
    confidence: heuristic
    auto_fixable: false
    evidence:
      source_file: tokens.md
      location: "## Border / UI tokens (lines 21–26)"
      finding: "Tokens ui01, ui02, ui03, ui32 were returned by a generic 'border' search against the OX token API. Their descriptions reference 'cards and divider lines', 'secondary background surface', etc. None of their descriptions mention TextField specifically. It is unclear which (if any) of these tokens are actually used by the TextField component vs being general system tokens surfaced by the search."
    fix_action: "Verify which border/UI tokens are actually applied within the TextField component internals; remove or annotate any that are not TextField-specific."
    blocks:
      - token table accuracy
    dependency: []

  - id: GAP-010
    dimension: figma
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: figma.md
      location: "## Visual states > Disabled state"
      finding: "Disabled state is described as 'reduced opacity applied at container level' with no specific opacity value or token reference. No Figma design context was retrieved for a disabled variant node."
    fix_action: "Run get_design_context on a disabled variant node (e.g. 22155:36842 Light/Medium/Disabled) to capture the exact opacity value and any colour overrides."
    blocks:
      - disabled state spec completeness
    dependency: []

  - id: GAP-011
    dimension: examples
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: true
    evidence:
      source_file: examples.md
      location: "(absent)"
      finding: "No example demonstrates the infoBoxText + infoBoxButtonLabel props. These props control an info tooltip beside the label (documented in props.md lines 59–60) and are unique to this component. No usage example exists for them."
    fix_action: "Add an example showing infoBoxText and infoBoxButtonLabel usage to examples.md."
    blocks:
      - docusaurus info tooltip documentation
    dependency: []

  - id: GAP-012
    dimension: props
    severity: minor
    type: DOC_GAP
    confidence: heuristic
    auto_fixable: false
    evidence:
      source_file: props.md
      location: "Rows focus (line 54) and fixed (line 55)"
      finding: "`focus` ('Programmatically set focused state') and `fixed` ('Prevents input from collapsing when empty') have inferred descriptions — the MCP returned empty descriptions for both. The behaviour of `fixed` in particular is not self-evident from the prop name."
    fix_action: "Verify the actual behaviour of `focus` and `fixed` from the package source and replace the inferred descriptions with accurate ones."
    blocks:
      - props table accuracy
    dependency: []

  - id: GAP-013
    dimension: tokens
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: tokens.md
      location: "## Padding table (lines 70–74)"
      finding: "Padding values are only confirmed for Medium/default size (from Figma code context). Small and Large padding values for text input are not confirmed — they may differ from Medium."
    fix_action: "Run get_design_context on a Small and Large text input variant to confirm padding values for those sizes."
    blocks:
      - size-specific styling spec
    dependency: []

warnings:
  - id: WARN-001
    dimension: accessibility
    confidence: heuristic
    evidence:
      source_file: accessibility.md
      location: "## WCAG 2.1 AA checklist, 1.4.3 row"
      finding: "Placeholder/hint text uses --text/textColor02 (#6C6862) on --ui/ui05 (#F4F3EE) background. Computed contrast ratio ≈ 3.8:1 — below the 4.5:1 AA threshold for normal text. WCAG allows lower contrast for placeholder text specifically (it is advisory text), but if textColor02 is also used for typed input values in the Rest/not-Filled state, this would be a contrast failure."
    advisory: "Verify whether --text/textColor02 is used for typed input values (not only placeholder). If yes, this is a WCAG 1.4.3 violation that must be raised with design."

  - id: WARN-002
    dimension: examples
    confidence: heuristic
    evidence:
      source_file: examples.md
      location: "## With icons, line 93"
      finding: "Icon example imports SearchIcon from '@8x8/oxygen-icons'. This package name was not confirmed from the OX MCP — it was inferred. The correct import path may differ."
    advisory: "Confirm the icon package name via get-component-info or list-components before publishing the example."

  - id: WARN-003
    dimension: figma
    confidence: heuristic
    evidence:
      source_file: figma.md
      location: "## Component documentation link (line 194)"
      finding: "All three Figma component families link to https://oxygen.8x8.com/docs/Contribution/intro (the Oxygen contribution guide), not a TextField-specific documentation page. This appears to be a placeholder in Figma rather than a real component doc link."
    advisory: "Check whether a TextField-specific Oxygen docs page exists and update figma.md if so."

  - id: WARN-004
    dimension: accessibility
    confidence: heuristic
    evidence:
      source_file: accessibility.md
      location: "## Screen reader guidance"
      finding: "The info icon button beside the label (rendered from _base_form_label atom, TypeIcon component) must have an accessible name. The current guidance says to set aria-label via inputProps, but this may not target the icon button — inputProps passes to the input element, not the label atom."
    advisory: "Verify the correct prop to pass an accessible name to the info icon button and update the guidance in accessibility.md."

  - id: WARN-005
    dimension: usage
    confidence: heuristic
    evidence:
      source_file: TextField-usage.md
      location: "frontmatter `source_type: editorial`; gaps section GAP-USAGE-001..005"
      finding: "TextField-usage.md is an editorial draft sourced from oxygen.8x8.com/components/textinput/usage and the extracted artifacts — not from a Figma examples page. Do/Don't pairs cover free-form vs known-choices, label-vs-placeholder, description-vs-placeholder, readOnly-vs-disabled, error-with-text, and width-to-content. The OX usage page does not address prefix/suffix/icon/action patterns, maxLength ergonomics, labelOrientation='row', or multi-line input — those pairs are editorial inference."
    advisory: "Have a designer review the 6 Do/Don't pairs and replace with figma-extract-usage output once a `↳ TextField examples` Figma page is created."

# --- navigation (added by component-map) ---
role: audit
pipeline_stage: spec_ready
pipeline_note: "Audit verdict YES — doc-rewrite can run; usage now editorial (was missing)"
siblings:
  - "[[TextField/props]]"
  - "[[TextField/examples]]"
  - "[[TextField/tokens]]"
  - "[[TextField/accessibility]]"
  - "[[TextField/figma]]"
  - "[[TextField/TextField-pui]]"
  - "[[TextField/TextField-usage]]"
tags:
  - oxygen
  - component/TextField
  - role/audit
  - stage/spec_ready
---

# TextField — Audit Report

**Audit date:** 2026-05-15 (re-audit after editorial usage doc landed; original audit 2026-04-29)
**Rubric version:** 1.0
**Verdict:** ✅ YES — ready for doc-rewrite

> No conflicts. No blocker-severity gaps. Doc-rewrite can proceed. The usage dimension is now covered editorially (score 0.70) — replace with figma-extract-usage output when a Figma examples page is created. Dark-mode visual specs still pending source data (GAP-005).

---

## File inventory

| File | Status | Notes |
|------|--------|-------|
| `props.md` | ✅ Present | |
| `examples.md` | ✅ Present | |
| `tokens.md` | ✅ Present | |
| `accessibility.md` | ✅ Present | |
| `TextField-figma.md` | ⚠️ Wrong name | Present as `figma.md` — content complete, filename non-conformant (GAP-006) |
| `TextField-usage.md` | ✅ Present (editorial) | Sourced from oxygen.8x8.com/components/textinput/usage + extracted artifacts; not figma-extract-usage output (GAP-001, WARN-005) |
| `TextField-pui.md` | ✅ Present | PASS — explicit no-context marker, rejection rationale documented |

---

## Dimension scores

| Dimension | Coverage | Score | Status |
|-----------|----------|-------|--------|
| Props | 7/9 | 0.78 | ⚠️ |
| Examples | 10/14 | 0.71 | ⚠️ |
| Tokens | 9/12 | 0.75 | ⚠️ |
| Accessibility | 12/15 | 0.80 | ⚠️ |
| Figma / Visual | 11/15 | 0.73 | ⚠️ |
| Usage guidelines | 1/1 | 0.70 | ⚠️ (editorial discount — needs designer review) |
| PUI context | 1/1 | 1.00 | ✅ |
| **Overall** | | **0.78** | |

_Previous overall: 0.68 (2026-04-29). Bump driven by usage dimension going 0.00 → 0.70 after [TextField-usage.md](./TextField-usage.md) landed._

---

## Gaps

### Major (4)

**GAP-002** · DOC_GAP · `props` dimension
`ActionTarget` type is unresolved — documented as a guess comment in props.md.
→ Look up `ActionTarget` in the package source and replace with the real union.

**GAP-003** · DOC_GAP · `props` dimension
`otherInputProps`, `otherLabelProps`, `otherActionProps` have no descriptions and unknown deprecation status.
→ Verify in package source; add deprecation notice or usage description.

**GAP-004** · DOC_GAP · `examples` dimension · auto-fixable
Error state example passes error message via `description`, but Figma shows a separate Error Area with a distinct prop/pattern. This example is misleading.
→ Investigate the correct error message prop/pattern and rewrite the example.

**GAP-005** · SOURCE_GAP · `figma` dimension
All visual state specs are Light-mode only. 68 Dark-mode symbol variants exist in Figma but were not captured.
→ Re-run Figma extraction on dark-mode variant nodes.

### Minor (9)

| ID | Dimension | Type | Finding | Auto-fixable |
|----|-----------|------|---------|:---:|
| GAP-001 | usage | SOURCE_GAP | TextField-usage.md present as editorial draft; no Figma examples page exists — figma-extract-usage cannot run | ❌ |
| GAP-006 | figma | DOC_GAP | File named `figma.md` — should be `TextField-figma.md` | ✅ |
| GAP-007 | tokens | SOURCE_GAP | `--text/textColor02` dark mode value missing | ❌ |
| GAP-008 | tokens | SOURCE_GAP | `--error/error01` dark mode value missing | ❌ |
| GAP-009 | tokens | DOC_GAP (heuristic) | Border tokens ui01–ui32 listed without confirmed TextField-specific usage | ❌ |
| GAP-010 | figma | SOURCE_GAP | Disabled state lacks opacity value — no design context captured for disabled variant | ❌ |
| GAP-011 | examples | DOC_GAP | No example for `infoBoxText` + `infoBoxButtonLabel` | ✅ |
| GAP-012 | props | DOC_GAP (heuristic) | `focus` and `fixed` props have inferred descriptions only | ❌ |
| GAP-013 | tokens | SOURCE_GAP | Padding values for Small/Large text input not confirmed from Figma | ❌ |

---

## Warnings (advisory, heuristic)

**WARN-001** · Accessibility
`--text/textColor02` (#6C6862 on #F4F3EE) has a contrast ratio ≈ 3.8:1. Acceptable for placeholder text, but verify it is not also applied to typed input values.

**WARN-002** · Examples
`@8x8/oxygen-icons` import in the icons example was inferred — confirm the actual package name before publishing.

**WARN-003** · Figma
All Figma component documentation links point to the contribution guide, not a TextField component page — likely a Figma placeholder.

**WARN-004** · Accessibility
The mechanism for setting an accessible name on the info icon button is unclear — `inputProps` targets the input element, not the label atom's icon button.

**WARN-005** · Usage (new — 2026-05-15)
TextField-usage.md is an editorial draft (not Figma-sourced). 6 Do/Don't pairs grounded in props.md, accessibility.md, and oxygen.8x8.com/components/textinput/usage. The OX page does not cover prefix/suffix/icon/action patterns, `maxLength` ergonomics, `labelOrientation="row"`, or multi-line input — those areas are editorial inference. Have a designer review and replace with figma-extract-usage output when a Figma examples page is created.

---

## Suggested next actions

1. **Rename `figma.md` → `TextField-figma.md`** (GAP-006 — 1 min, unblocks doc-rewrite file lookup)
2. **Investigate error message prop** (GAP-004 — unblocks examples dimension; error docs are currently misleading)
3. **Designer review of TextField-usage.md** (WARN-005) and creation of a Figma `↳ TextField examples` page so figma-extract-usage can replace the editorial draft (GAP-001)
4. **Re-run Figma extraction on dark variants** to fill GAP-005, GAP-010
5. **Fetch missing token dark values** for textColor02 and error01 (GAP-007, GAP-008)
6. **Proceed to doc-rewrite** — can start immediately on all dimensions; usage now covered editorially.
