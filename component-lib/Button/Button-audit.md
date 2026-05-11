---
rubric_version: "1.0"
component: Button
audit_date: "2026-05-11"
auditor: doc-audit skill

files_found:
  - props.md
  - examples.md
  - tokens.md
  - accessibility.md
  - Button-figma.md
  - Button-usage.md

files_missing:
  - Button-pui.md

dimension_scores:
  props:        { score: 0.75, coverage: "9/12" }
  examples:     { score: 0.72, coverage: "7/10" }
  tokens:       { score: 0.78, coverage: "7/9"  }
  accessibility:{ score: 0.80, coverage: "6/8"  }
  figma:        { score: 0.70, coverage: "7/10" }
  usage:        { score: 0.72, coverage: "8/11 — editorial (no Figma examples page)" }
  pui:          { score: 0.00, coverage: "0/0 — SOURCE_GAP" }

available_dimensions_avg: 0.75
overall_avg: 0.64

counts:
  doc_gaps: 15
  source_gaps: 1
  conflicts: 3
  warnings: 3

verdict: NO
verdict_reason: >
  3 CONFLICTs found in the figma dimension — verdict is NO regardless of other gaps.
  CONFLICT-001: Secondary rest bg token is $action01 in Figma but action02 in tokens.md
  (visually different colors — requires designer confirmation).
  CONFLICT-002: Text button active bg is $active17 in Figma, but tokens.md assigns
  active17 to inverted variants only and shows no active bg for Text buttons.
  CONFLICT-003: Figma CSS export uses --actions/action09 for Primary bg; tokens.md
  names the same color action01 — naming scheme divergence.
  All three must be resolved before doc-rewrite proceeds.
  NOTE: GAP-004 (Button-usage.md missing) is RESOLVED — Button-usage.md was authored
  editorially from the published Oxygen docs page (2026-05-11). Usage now scores 0.72.

suggested_next_action: >
  1. Resolve GAP-001 (Secondary rest token): designer or token owner confirms
     whether Figma reference page has a copy-paste error, or tokens.md is stale.
  2. Resolve GAP-002 (Text active token): confirm whether active17 applies to
     non-inverted text buttons or a different token should be used.
  3. Resolve GAP-003 (CSS naming): decide canonical token name format across
     Figma CSS export and Oxygen token system.
  4. Run pui-mcp-extract → produces Button-pui.md (or confirm Button has no PUI context)
  5. Re-run doc-audit → verdict should reach PARTIAL or YES once CONFLICTs are resolved
  6. Run doc-rewrite → produces Button-spec.md
  Optional: Replace Button-usage.md editorial draft with figma-extract-usage output
  when a Figma "↳ Button examples" page with Do/Don't card frames is created.

gaps:
  - id: GAP-001
    dimension: figma
    severity: blocker
    type: CONFLICT
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: Button-figma.md
      location: "## Color & token bindings — Label Button Background token, Secondary / Rest"
      finding: >
        Figma Color Tokens Reference page (node 78525:28916) annotates Secondary rest
        background as $action01 (#0056E0, blue). tokens.md specifies action02 (#26252A,
        near-black) for the same slot. These are visually distinct colors — one source
        must be wrong.
    fix_action: "Designer/token owner to confirm correct token for Secondary rest bg; update the incorrect source file"
    blocks: [doc-rewrite/figma-dimension, doc-rewrite/tokens-dimension, docusaurus-generate, storybook-generate]
    dependency: []

  - id: GAP-002
    dimension: figma
    severity: blocker
    type: CONFLICT
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: Button-figma.md
      location: "## Color & token bindings — Label Button Background token, Text Primary / Active and Text Danger / Active"
      finding: >
        Figma shows $active17 as the active-state background token for both Text Primary
        and Text Danger variants. tokens.md defines active17 as 'Inverted primary button
        active; inverted text button active' — not standard text button.
        tokens.md does not document any active bg token for non-inverted text buttons.
        The two sources are irreconcilable without designer input.
    fix_action: "Confirm correct active bg token for non-inverted Text buttons; update tokens.md and/or Figma reference"
    blocks: [doc-rewrite/figma-dimension, doc-rewrite/tokens-dimension]
    dependency: []

  - id: GAP-003
    dimension: figma
    severity: major
    type: CONFLICT
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: Button-figma.md
      location: "## API — Component properties / Token coverage"
      finding: >
        Figma CSS export (get_design_context) emits var(--actions/action09, #0056e0)
        for Primary button background. tokens.md names the same hex value as semantic
        token 'action01'. The CSS path format 'actions/action09' does not match the
        token name 'action01' — two naming schemes coexist with no documented mapping.
    fix_action: "Document the mapping between Figma CSS variable names (--actions/actionNN) and Oxygen semantic token names (actionNN) — or adopt a single naming convention"
    blocks: [storybook-generate, docusaurus-generate]
    dependency: []

  - id: GAP-004
    dimension: usage
    severity: major
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    status: RESOLVED
    evidence:
      source_file: Button-usage.md
      location: "Button/ directory"
      finding: >
        RESOLVED 2026-05-11 — Button-usage.md created editorially from the published
        Oxygen docs page (https://oxygen.8x8.com/docs/components/button/usage, screenshot
        2026-05-11), cross-validated against all extracted MCP/Figma artifacts.
        7 Do/Don't pairs. Usage dimension now scores 0.72.
        Note: file is an editorial draft, NOT figma-extract-usage output. No Figma
        Do/Don't card frames exist. Replace with figma-extract-usage output if a
        Figma "↳ Button examples" page is created.
    fix_action: "No further action required for usage file existence. See GAP-018/019/020 for remaining usage DOC_GAPs."
    blocks: []
    dependency: []

  - id: GAP-005
    dimension: pui
    severity: major
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: ~
      location: "Button/ directory"
      finding: "Button-pui.md is absent — pui-mcp-extract skill has not been run. Button is a pure UI component and may have no relevant PUI context (notifications, navigation, session, event bus) — confirm before running."
    fix_action: "Run pui-mcp-extract for the Button component, or add <!-- NO RELEVANT PUI CONTEXT --> marker to a Button-pui.md stub to close this gap"
    blocks: [doc-rewrite/pui-dimension]
    dependency: []

  - id: GAP-006
    dimension: props
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: true
    evidence:
      source_file: props.md
      location: "## IconButton Props — size row"
      finding: "IconButton `size` prop type is listed as `iconButtonSize enum` but the enum values are not expanded"
    fix_action: "Add enum value table for iconButtonSize (values visible in examples.md usage: `iconButtonSize.${size}`)"
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
      location: "## ButtonGroup Props, ## DropdownButton Props, ## IconButton Props"
      finding: "Default values are absent for ButtonGroup (spacing, align), DropdownButton (size, isActive, isDisabled, fullWidth), and IconButton (isInverted) props"
    fix_action: "Add default values for sub-component props, or explicitly mark as '—' (none) per prop"
    blocks: []
    dependency: []

  - id: GAP-008
    dimension: props
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: Button-figma.md
      location: "## API — Component properties / Variant axes — Fluid 100%"
      finding: >
        Figma Label Button component set has a 'Fluid 100%' variant axis (False/True)
        controlling full-width layout. props.md does not document a fullWidth prop for
        the main Button component (only for DropdownButton). If the prop exists in the
        Oxygen implementation, it is undocumented.
    fix_action: "Confirm whether Button supports a fullWidth prop; add to props.md if so, or note the Figma axis maps differently (e.g. via CSS wrapper)"
    blocks: []
    dependency: []

  - id: GAP-009
    dimension: examples
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: true
    evidence:
      source_file: examples.md
      location: "## Variants section"
      finding: "`tertiary` variant is absent from the Variants code block; all other variants are shown"
    fix_action: "Add `<Button variant=\"tertiary\">`, `<Button variant=\"tertiary\" isActive>`, `<Button variant=\"tertiary\" isDisabled>` to the Variants section"
    blocks: []
    dependency: []

  - id: GAP-010
    dimension: examples
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: true
    evidence:
      source_file: examples.md
      location: "## IconButton — Custom size example, line 288"
      finding: "Template literal `iconButtonSize.${size}` is a Storybook arg placeholder — not valid JSX"
    fix_action: "Replace with a concrete enum value, e.g. `iconButtonSize.medium`, or expand into separate per-size examples"
    blocks: []
    dependency: [GAP-006]

  - id: GAP-011
    dimension: examples
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: true
    evidence:
      source_file: examples.md
      location: "## Circular (Control) Buttons — destructive block"
      finding: "`HangupIcon` is used in the destructive circular example but is not in the import statement"
    fix_action: "Add `HangupIcon` to the import, or replace with the actual icon name from @8x8/oxygen-icon"
    blocks: []
    dependency: []

  - id: GAP-012
    dimension: examples
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: true
    evidence:
      source_file: examples.md
      location: "## Sizes section"
      finding: "`big` size is listed in props.md as a valid ButtonSize value but has no example in the Sizes section"
    fix_action: "Add `<Button size=\"big\">Click me</Button>` to the Sizes section"
    blocks: []
    dependency: []

  - id: GAP-013
    dimension: tokens
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: true
    evidence:
      source_file: tokens.md
      location: "## Token-to-Variant Quick Reference"
      finding: "`tertiary` variant (non-reversed) is absent from the Token-to-Variant quick reference table"
    fix_action: "Add a `tertiary` row to the Token-to-Variant table with the correct rest/hover/active tokens"
    blocks: []
    dependency: []

  - id: GAP-014
    dimension: tokens
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: tokens.md
      location: "Entire file"
      finding: >
        No disabled-state tokens documented. Button-figma.md identifies the token names
        as disabled01 (bg) and disabled04 (text/icon) from Figma annotations, but their
        hex values and full semantic descriptions are absent from tokens.md.
        Blocked on GAP-001 resolution (if Secondary rest conflict changes token table
        structure). Token hex values require a separate lookup.
    fix_action: "Add disabled01 and disabled04 rows to tokens.md with hex values from the Oxygen theme; reference Button-figma.md Disabled-state tokens section"
    blocks: []
    dependency: [GAP-001]

  - id: GAP-015
    dimension: accessibility
    severity: minor
    type: DOC_GAP
    confidence: heuristic
    auto_fixable: true
    evidence:
      source_file: accessibility.md
      location: "## Keyboard Interactions / ## Screen Reader Guidance"
      finding: "`aria-pressed` is not mentioned for the `isActive` (toggle) state"
    fix_action: "Add a note that icon-only or toggle buttons using `isActive` should set `aria-pressed` accordingly"
    blocks: []
    dependency: []

  - id: GAP-016
    dimension: figma
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: Button-figma.md
      location: "## Structure & spacing — Density / size variants"
      finding: "Medium and Small button dimensions are marked NOT FOUND — only Large size (48px / 16px / 12px) was extractable from the available Figma data"
    fix_action: "Extract Medium and Small variant dimensions from the Label Button component set (node 15653:16329) by inspecting Medium and Small child variant nodes"
    blocks: []
    dependency: []

  - id: GAP-017
    dimension: figma
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: Button-figma.md
      location: "## API — Component properties / Token coverage"
      finding: "Figma Variables API returned empty — token bindings are inferred from text annotations only; actual variable-to-token mapping is unverified"
    fix_action: "Investigate whether the file uses a shared library for variables; re-run figma_get_variables with includePublished=true or check Figma Desktop for variable collections"
    blocks: []
    dependency: []

  - id: GAP-018
    dimension: usage
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: Button-usage.md
      location: "## Overview — Type matrix — Note block"
      finding: >
        Button-usage.md documents 'Soft', 'Disclosure', 'Optional', and 'Indeterminate'
        treatments as visible on the published docs page screenshot but absent from
        props.md (props.md:86 lists only primary/secondary/tertiary/tertiaryReversed/
        text/success/destructive). These may be composition patterns rather than
        first-class API variants. The relationship between docs-page types and the
        Oxygen API is currently unresolved.
    fix_action: "Confirm with Oxygen team whether Soft/Disclosure/Optional/Indeterminate are new API variants, composed treatments, or rebranded existing variants; update Button-usage.md type matrix and props.md accordingly"
    blocks: []
    dependency: []

  - id: GAP-019
    dimension: usage
    severity: minor
    type: DOC_GAP
    confidence: heuristic
    auto_fixable: false
    evidence:
      source_file: Button-usage.md
      location: "## Placement & alignment — inline comment"
      finding: >
        The Alignment section in Button-usage.md contains a <!-- TODO --> note indicating
        the exact wording from the published docs Alignment section was not captured at
        readable resolution in the screenshot. The 'primary right-aligned in dialogs'
        convention is described behaviourally but not as a verbatim transcription.
    fix_action: "Confirm exact wording from the published Oxygen docs Alignment section (https://oxygen.8x8.com/docs/components/button/usage) and update Button-usage.md Placement & alignment section"
    blocks: []
    dependency: []

  - id: GAP-020
    dimension: usage
    severity: minor
    type: DOC_GAP
    confidence: heuristic
    auto_fixable: false
    evidence:
      source_file: Button-usage.md
      location: "## Related components — inline comment"
      finding: >
        Related components list (ButtonGroup, DropdownButton, IconButton, TextLink) was
        derived from props.md and accessibility.md rather than confirmed against the
        published docs page Related section. Additional related components (e.g. Tooltip,
        Popover, ConfirmDialog) may be listed on the live page but are not verified.
    fix_action: "Confirm the full Related section from the published docs page and update Button-usage.md ## Related components"
    blocks: []
    dependency: []

warnings:
  - id: WARN-001
    dimension: props
    confidence: heuristic
    note: >
      `theme` prop is typed as `object` with no shape documentation.
      Downstream tooling (Storybook, Docusaurus) cannot generate a control for it.
      Consider requesting a TypeScript interface from the MCP or source code.

  - id: WARN-002
    dimension: accessibility
    confidence: heuristic
    note: >
      WCAG 2.5.3 (Label in Name) is not in the WCAG checklist. Icon buttons with
      visible tooltip text and `aria-label` should have matching values to satisfy
      this criterion. Advisory only.

  - id: WARN-003
    dimension: figma
    confidence: heuristic
    note: >
      Figma Type axis covers only Primary/Secondary/Text. The Oxygen ButtonVariant
      enum also includes tertiary, tertiaryReversed, success, and destructive.
      These likely exist in a separate Figma component set (circular/control buttons).
      figma-extract should be run against those nodes to complete Figma coverage.
# --- navigation ---
role: audit
pipeline_stage: blocked
pipeline_note: "Audit verdict NO — resolve 3 CONFLICTs before rewrite. Usage dimension now scored (0.72) — GAP-004 resolved 2026-05-11."
siblings:
  - "[[Button/props]]"
  - "[[Button/examples]]"
  - "[[Button/tokens]]"
  - "[[Button/accessibility]]"
  - "[[Button/Button-figma]]"
  - "[[Button/Button-usage]]"
tags:
  - oxygen
  - component/Button
  - role/audit
  - stage/blocked
---

# Button — Documentation Audit

> **Rubric version:** 1.0 · **Audit date:** 2026-05-11 · **Verdict:** NO

---

## File Inventory

| File | Status | Produced by |
|------|--------|-------------|
| `props.md` | ✅ Present | oxygen-mcp-extract |
| `examples.md` | ✅ Present | oxygen-mcp-extract |
| `tokens.md` | ✅ Present | oxygen-mcp-extract |
| `accessibility.md` | ✅ Present | oxygen-mcp-extract |
| `Button-figma.md` | ✅ Present | figma-extract |
| `Button-usage.md` | ✅ Present *(editorial, 2026-05-11)* | figma-extract-usage *(editorial substitute)* |
| `Button-pui.md` | ❌ **MISSING** | pui-mcp-extract |

---

## Dimension Scores

| Dimension | Score | Coverage | Status |
|-----------|-------|----------|--------|
| Props | 0.75 | 9/12 | ✅ Available |
| Examples | 0.72 | 7/10 | ✅ Available |
| Tokens | 0.78 | 7/9 | ✅ Available |
| Accessibility | 0.80 | 6/8 | ✅ Available |
| Figma | 0.70 | 7/10 | ✅ Available — ⛔ 3 CONFLICTs |
| Usage | 0.72 | 8/11 — editorial | ✅ Available *(editorial draft; no Figma card frames)* |
| PUI | 0.00 | — | ❌ SOURCE_GAP (major) |
| **Available avg** | **0.75** | | |
| **Overall avg** | **0.64** | | |

---

## Gap Summary

| Count | Category |
|-------|----------|
| 3 | CONFLICTs (1 blocker, 2 major) — **blocks doc-rewrite** |
| 1 | SOURCE_GAP (major) — PUI file missing |
| 15 | DOC_GAPs (all minor) |
| 3 | Warnings (heuristic, advisory) |

---

## Gaps

### CONFLICTs — must be resolved before doc-rewrite

#### GAP-001 · Figma/Tokens · BLOCKER

**Finding:** Secondary rest background token mismatch. Figma reference shows `$action01` (#0056E0, blue); tokens.md specifies `action02` (#26252A, near-black).
**Fix:** Designer/token owner confirms correct token; update the incorrect source.

#### GAP-002 · Figma/Tokens · BLOCKER

**Finding:** Text button active bg is `$active17` in Figma. tokens.md defines `active17` as an inverted-button token and documents no active bg for non-inverted text buttons.
**Fix:** Confirm correct active bg token for Text buttons and update both sources.

#### GAP-003 · Figma/Tokens · MAJOR

**Finding:** Figma CSS export uses `--actions/action09` for Primary bg; tokens.md names the same color `action01`. Naming schemes diverge with no documented mapping.
**Fix:** Document CSS variable → semantic token name mapping, or adopt a single convention.

---

### SOURCE_GAPs

#### GAP-004 · Usage · ~~MAJOR~~ **RESOLVED 2026-05-11**

`Button-usage.md` created editorially from the published Oxygen docs page. Usage now scores 0.72. See GAP-018/019/020 for remaining minor usage DOC_GAPs.

#### GAP-005 · PUI · MAJOR
**Finding:** `Button-pui.md` absent — `pui-mcp-extract` not run. Button is a pure UI component; confirm whether PUI context is applicable before running.
**Fix:** Run `pui-mcp-extract`, or add `<!-- NO RELEVANT PUI CONTEXT -->` stub to close gap.

---

### DOC_GAPs (all minor)

#### GAP-006 · Props · auto-fixable
`IconButton` `size` enum values not documented.
→ **Fix:** Expand enum value table.

#### GAP-007 · Props · requires human input
Default values absent for `ButtonGroup`, `DropdownButton`, `IconButton` sub-component props.
→ **Fix:** Add defaults or mark as `—`.

#### GAP-008 · Props · requires human input
`Fluid 100%` variant axis present in Figma Label Button but no `fullWidth` prop in props.md for Button.
→ **Fix:** Confirm whether Button supports `fullWidth`; add to props.md if so.

#### GAP-009 · Examples · auto-fixable
`tertiary` variant absent from Variants example block.
→ **Fix:** Add three standard state examples for `variant="tertiary"`.

#### GAP-010 · Examples · auto-fixable (depends GAP-006)
`iconButtonSize.${size}` on `examples.md:288` is a Storybook placeholder — invalid JSX.
→ **Fix:** Replace with a concrete enum value.

#### GAP-011 · Examples · auto-fixable
`HangupIcon` used in Circular/destructive example but missing from import.
→ **Fix:** Add `HangupIcon` to import.

#### GAP-012 · Examples · auto-fixable
`big` ButtonSize has no example in the Sizes section.
→ **Fix:** Add `<Button size="big">Click me</Button>`.

#### GAP-013 · Tokens · auto-fixable
`tertiary` variant absent from Token-to-Variant quick reference table.
→ **Fix:** Add row with correct tokens.

#### GAP-014 · Tokens · requires human input (depends GAP-001)
Disabled-state tokens (`disabled01` bg, `disabled04` text/icon) identified in figma.md but hex values absent from tokens.md.
→ **Fix:** Add `disabled01` and `disabled04` rows with hex values from Oxygen theme.

#### GAP-015 · Accessibility · auto-fixable
`aria-pressed` not mentioned for `isActive` toggle state.
→ **Fix:** Add note in Screen Reader Guidance.

#### GAP-016 · Figma · requires human input
Medium and Small button dimensions not measured — only Large (48px H / 16px pad) confirmed.
→ **Fix:** Inspect Medium and Small child variants of node `15653:16329`.

#### GAP-017 · Figma · requires human input
Figma Variables API returned empty — token bindings inferred from text annotations only.
→ **Fix:** Re-run `figma_get_variables` with `includePublished=true` or investigate shared library setup.

#### GAP-018 · Usage · requires human input *(NEW)*
`Soft`, `Disclosure`, `Optional`, `Indeterminate` treatments on docs page not verified against the Oxygen API.
→ **Fix:** Confirm with Oxygen team whether these are new variants, compositions, or renames; update `Button-usage.md` type matrix and `props.md`.

#### GAP-019 · Usage · requires human input *(NEW)*
Alignment section verbatim body copy from the published docs page not captured (TODO marker in file — screenshot resolution insufficient).
→ **Fix:** Read live docs page ([oxygen.8x8.com/docs/components/button/usage](https://oxygen.8x8.com/docs/components/button/usage)) and transcribe Alignment section.

#### GAP-020 · Usage · requires human input *(NEW)*
Related components list unconfirmed against the live docs page — additional entries (e.g. Tooltip, Popover, ConfirmDialog) may be present.
→ **Fix:** Confirm full Related section from the live docs page and update `Button-usage.md`.

---

## Warnings

**WARN-001 (Props):** `theme` prop typed as bare `object` — no shape. Storybook/Docusaurus controls cannot be generated.

**WARN-002 (Accessibility):** WCAG 2.5.3 (Label in Name) absent from checklist. Relevant for icon buttons with both tooltip and `aria-label`.

**WARN-003 (Figma):** Figma Type axis covers only Primary/Secondary/Text. Variants `tertiary`, `tertiaryReversed`, `success`, `destructive` likely in a separate circular/control button component set — run `figma-extract` against those nodes.

---

## Verdict: NO

**doc-rewrite is blocked until the 3 CONFLICTs are resolved.**

Progress since last audit (2026-04-28):
- ✅ `Button-usage.md` created — usage dimension raised from 0.00 → 0.72
- ✅ SOURCE_GAPs reduced from 2 → 1
- ✅ Overall avg raised from 0.54 → 0.64
- ⛔ 3 figma CONFLICTs unchanged — still blocking doc-rewrite

Resolve in this order:

```
1. Resolve GAP-001  → confirm Secondary rest bg token (designer/token owner)
2. Resolve GAP-002  → confirm Text button active bg token
3. Resolve GAP-003  → document CSS variable ↔ semantic token name mapping
4. Confirm GAP-005  → run pui-mcp-extract or add NO_PUI stub
5. Re-run doc-audit → verdict should reach PARTIAL or YES
6. Run doc-rewrite  → produces Button-spec.md
```

_Source: doc-audit skill · Rubric v1.0 · Updated 2026-05-11_
