---
rubric_version: "1.0"
component: Select
package: "@8x8/oxygen-select"
audit_date: "2026-04-29"
auditor: doc-audit skill

files_found:
  - props.md
  - examples.md
  - tokens.md
  - accessibility.md
  - select-pui.md

files_missing:
  - select-figma.md
  - select-usage.md

verdict: NO
verdict_rationale: >
  Two deterministic CONFLICTs exist in the source data: (1) the `isAsync` prop
  has type `boolean` in get-component-info but type `IsAsync` in
  get-component-props — both authoritative OX MCP endpoints disagree; (2) the
  MCP examples use `ref={selectRef}` directly while props.md documents
  `forwardedRef` as the ref prop — it is unclear whether both patterns are
  supported simultaneously. These must be resolved before doc-rewrite can
  produce a spec without risk of incorrect type or usage guidance.
  Additionally, select-figma.md is missing (blocker SOURCE_GAP), which would
  independently produce a PARTIAL verdict. With CONFLICTs present, NO takes
  precedence.

scores:
  props_completeness:      0.78
  examples_coverage:       0.65
  token_coverage:          0.35
  accessibility:           0.78
  figma_alignment:         0.15
  usage_guidelines:        0.25
  cross_file_consistency:  0.78
  overall:                 0.53

gap_counts:
  doc_gaps: 8
  source_gaps: 5
  conflicts: 2
  warnings: 3

gaps:
  - id: GAP-001
    dimension: figma_alignment
    severity: blocker
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: "(absent)"
      location: "component-lib/Select/"
      finding: >
        select-figma.md does not exist. figma-extract was not run. The Figma
        Desktop Bridge plugin was not available during this session so
        get_design_context failed. Metadata (node structure) and a screenshot
        were captured via get_metadata and get_screenshot, but these are
        insufficient for a full figma.md file — variant properties, token
        bindings, spacing values, and design annotations were not extracted.
        The Figma node 2105:2 in file 5YihJ5WuDvnvrlrRMC4sBp contains the
        Select component set with ~80 variants across Mode × Size × State ×
        Open × Error dimensions plus a leading-visuals frame (icon/status/avatar).
    fix_action: >
      Open Figma Desktop Bridge plugin, then run the figma-extract skill for
      Select targeting node 2105:2, file 5YihJ5WuDvnvrlrRMC4sBp. The
      metadata already captured shows the variant naming convention:
      "Mode=Light, Size=Large, State=Rest, Open=False, Error=False".
    blocks:
      - figma_alignment dimension
      - token_coverage (component-level tokens)
      - props_completeness (Figma-only props or design annotations)
    dependency: []

  - id: GAP-002
    dimension: cross_file_consistency
    severity: major
    type: CONFLICT
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: props.md
      location: "props.md line 31 vs get-component-props MCP response"
      finding: >
        The `isAsync` prop has two conflicting type definitions from the same
        authoritative source (OX MCP, two different endpoints):
        - get-component-info returns: `type: "boolean"`, `default: "false"`
        - get-component-props returns: `type: "IsAsync"` (a distinct named type)
        props.md currently documents `type: boolean` (from get-component-info).
        It is unclear whether `IsAsync` is an enum, a branded boolean, or an
        alias for boolean. If `IsAsync` is a union type with values beyond
        true/false, the props.md documentation is incomplete.
    fix_action: >
      Inspect the `@8x8/oxygen-select` package source or TypeScript exports
      to find the `IsAsync` type definition. If it is `type IsAsync = boolean`,
      props.md is correct — add a note. If it has additional values, update
      the type column and add the valid values.
    blocks:
      - props.md type accuracy
      - doc-rewrite type generation
    dependency: []

  - id: GAP-003
    dimension: cross_file_consistency
    severity: major
    type: CONFLICT
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: examples.md
      location: "examples.md line 42 vs props.md line 19"
      finding: >
        props.md documents `forwardedRef: React.Ref<any>` as the prop for
        attaching a ref to the Select instance. However, the MCP Storybook
        example (FocusableSelect) uses `<Select ref={selectRef} options={options} />`
        — the standard React `ref=` prop, not `forwardedRef=`. Both came from
        authoritative OX MCP data (different endpoints). It is unclear whether:
        (a) the component uses React.forwardRef and both `ref=` and `forwardedRef=`
        work, (b) `forwardedRef` is deprecated in favour of `ref=`, or (c) the
        example is incorrect.
    fix_action: >
      Check the Select component source — specifically whether it wraps in
      React.forwardRef. If it does, document that `ref=` works (standard
      React pattern) AND optionally `forwardedRef=` as a legacy prop. If
      `forwardedRef` is the only supported pattern, the Storybook example is
      wrong. Update props.md and examples.md to match confirmed behaviour.
    blocks:
      - props.md ref prop accuracy
      - examples.md correctness
    dependency: []

  - id: GAP-004
    dimension: props_completeness
    severity: major
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: props.md
      location: "props.md — options prop row"
      finding: >
        The `options` prop is typed as `SelectOption[]` but `SelectOption` is
        never defined. The examples show both flat options `{ value, label }`
        and grouped options `{ label: string, options: SelectOption[] }`. It
        is undocumented whether `SelectOption` supports additional fields
        (e.g. `icon`, `isDisabled`, `description`) or what the grouping
        shape looks like as a TypeScript interface.
    fix_action: >
      Inspect the `@8x8/oxygen-select` package for the `SelectOption` type
      export. Add a type definition block to props.md showing the full
      interface, including the grouped option variant and any optional fields
      (icon, isDisabled, etc.).
    blocks:
      - props.md type completeness
      - examples.md correctness
    dependency: []

  - id: GAP-005
    dimension: props_completeness
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: true
    evidence:
      source_file: examples.md
      location: "examples.md lines 53–70 (SelectModal example)"
      finding: >
        `menuPortalTarget` is used in the Select-in-Modal example
        (`menuPortalTarget={portalTarget}`) but this prop is not in props.md.
        It is a react-select pass-through prop, but because it is demonstrated
        in an official Storybook example it is effectively part of the Oxygen
        API surface and should be documented.
    fix_action: >
      Add `menuPortalTarget` to props.md with type `HTMLElement | null`,
      default `null`, and description "Renders the dropdown menu through a
      React portal to the provided element. Required when using Select inside
      a Modal to prevent z-index and overflow clipping issues."
    blocks:
      - props.md completeness
    dependency: []

  - id: GAP-006
    dimension: props_completeness
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: true
    evidence:
      source_file: examples.md
      location: "examples.md lines 38–40 (MenuPlacement example)"
      finding: >
        `menuPlacement` is used in the MenuPlacement example
        (`menuPlacement="auto"`) but this prop is not in props.md. It is
        a react-select prop but is explicitly demonstrated in a Storybook
        example, making it part of the documented API.
    fix_action: >
      Add `menuPlacement` to props.md with type `'auto' | 'top' | 'bottom'`,
      default `'bottom'`, and description "Controls where the dropdown menu
      opens relative to the input. 'auto' switches to 'top' when near the
      bottom of the viewport."
    blocks:
      - props.md completeness
    dependency: []

  - id: GAP-007
    dimension: examples_coverage
    severity: minor
    type: DOC_GAP
    confidence: heuristic
    auto_fixable: true
    evidence:
      source_file: examples.md
      location: "examples.md — all examples"
      finding: >
        No example demonstrates the error state. `hasError` is a documented
        prop that renders a red border. The Figma component set has Error=True
        variants for all sizes and modes, yet no code example shows how to
        combine `hasError` with an error message below the field.
    fix_action: >
      Add an error state example to examples.md showing `hasError={true}` with
      a visible error message element below the Select (presumably a sibling
      `<p>` or Oxygen FormField helper component — confirm the pattern from
      Storybook).
    blocks: []
    dependency: []

  - id: GAP-008
    dimension: examples_coverage
    severity: minor
    type: DOC_GAP
    confidence: heuristic
    auto_fixable: true
    evidence:
      source_file: examples.md
      location: "examples.md — all examples"
      finding: >
        No example demonstrates the disabled state (`isDisabled={true}`), even
        though it is a core form field state and the Figma component has explicit
        Disabled variants. The FocusableSelect Storybook story specifically tests
        programmatic focus on a disabled select, suggesting disabled + focusable
        is an important edge case.
    fix_action: >
      Add a disabled example to examples.md. Cross-reference with the
      FocusableSelect example to explain that React Hook Forms may programmatically
      focus a disabled Select on validation error.
    blocks: []
    dependency: []

  - id: GAP-009
    dimension: examples_coverage
    severity: minor
    type: DOC_GAP
    confidence: heuristic
    auto_fixable: true
    evidence:
      source_file: examples.md
      location: "examples.md — all examples"
      finding: >
        No example demonstrates async loading (`isAsync={true}` + `loadOptions`).
        Async Select is a documented pattern (with its own boolean prop and
        loadOptions callback) and is a materially different usage mode from
        sync. The MCP description references the react-select async docs but
        no code example is provided.
    fix_action: >
      Add an async example to examples.md showing `isAsync={true}` with a
      `loadOptions` function that returns a Promise of options. Reference
      https://react-select.com/async.
    blocks: []
    dependency: []

  - id: GAP-010
    dimension: examples_coverage
    severity: minor
    type: DOC_GAP
    confidence: heuristic
    auto_fixable: true
    evidence:
      source_file: examples.md
      location: "examples.md — all examples"
      finding: >
        No example shows size variants (`size="small"`, `size="large"`) or
        the 'default' size. The size prop has 3 values and the Figma shows
        Small (76px), Medium (84px), Large (92px) with distinct heights but
        examples.md does not demonstrate how to switch sizes.
    fix_action: >
      Add a size variants example to examples.md demonstrating all three
      `size` values side by side. Note the 'default' → Medium naming
      discrepancy.
    blocks: []
    dependency: []

  - id: GAP-011
    dimension: token_coverage
    severity: major
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: tokens.md
      location: "tokens.md — Theme tokens table"
      finding: >
        The Oxygen MCP token search for 'select' returned only 1 token (`ui01`).
        tokens.md has a state × token mapping table but all entries except the
        `ui01` selected-state background use placeholder text ("Internal border
        token", "Internal hover token", etc.). The actual token names for input
        border, focus ring, error colour, disabled opacity, and text colour
        are unknown. This is a SOURCE_GAP — the token registry query was
        insufficiently targeted.
    fix_action: >
      Re-run get-theme-tokens with broader search terms: 'border', 'focus',
      'error', 'disabled', 'interactive', 'input'. Also inspect the
      @8x8/oxygen-select package source to find which CSS variables / theme
      tokens are consumed. Update tokens.md with confirmed token names.
    blocks:
      - tokens.md completeness
      - doc-rewrite token section
    dependency: [GAP-001]

  - id: GAP-012
    dimension: props_completeness
    severity: minor
    type: DOC_GAP
    confidence: heuristic
    auto_fixable: true
    evidence:
      source_file: props.md
      location: "props.md — size prop row"
      finding: >
        The `size` prop documents values `'default' | 'large' | 'small'` but
        does not explain that `'default'` corresponds to the Figma "Medium"
        variant. This disconnect between the code API ('default') and the
        design system label ('Medium') is confusing for engineers cross-
        referencing Figma and code.
    fix_action: >
      Add a note to the `size` prop description: "Note: `'default'` in code
      corresponds to the 'Medium' size in Figma." Update the Figma Variants
      table to show the code value alongside the Figma label.
    blocks: []
    dependency: []

  - id: GAP-013
    dimension: accessibility
    severity: minor
    type: SOURCE_GAP
    confidence: heuristic
    auto_fixable: false
    evidence:
      source_file: accessibility.md
      location: "accessibility.md — all sections"
      finding: >
        All accessibility guidance in accessibility.md is inferred from
        react-select's known implementation and WAI-ARIA combobox pattern. The
        Oxygen MCP returned no explicit accessibility documentation for this
        component. The Figma file (node 2105:2) was not fully inspected for
        ARIA annotations. It is unconfirmed whether the Oxygen Select wrapper
        adds or modifies any ARIA attributes beyond react-select's defaults.
    fix_action: >
      Inspect component DOM output in a browser (or component source) to
      confirm ARIA roles, aria-expanded, aria-haspopup, aria-labelledby
      and aria-invalid are applied correctly. Update accessibility.md with
      confirmed values. If Figma annotations exist, run figma-extract to
      capture them.
    blocks: []
    dependency: [GAP-001]

  - id: GAP-014
    dimension: usage_guidelines
    severity: major
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: "(absent)"
      location: "component-lib/Select/"
      finding: >
        select-usage.md does not exist. figma-extract-usage was not run.
        The Do/Don't visual examples from Figma have not been captured.
        Basic usage guidance (when to use / when not to use) was extracted
        from the OX MCP usage field and included in examples.md, but this is
        a text summary only — no paired visual Do/Don't examples are present.
    fix_action: >
      Run the figma-extract-usage skill for Select. If the Figma page has
      no Do/Don't frames, request the designer to add them following the
      figma-draw template convention.
    blocks:
      - docusaurus usage-guidelines section
      - storybook usage stories
    dependency: []

  - id: GAP-015
    dimension: figma_alignment
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: props.md
      location: "props.md — Figma Variants table"
      finding: >
        The Figma Variants table in props.md was derived from node name strings
        in the metadata XML (e.g. "Mode=Light, Size=Large, State=Rest,
        Open=False, Error=False"), not from a full figma-extract. The leading
        visuals frame (node 69857:19373) shows icon/status/avatar types for
        both modes but these are not documented as variants or as a prop in
        props.md. It is unknown whether leading visuals correspond to the
        `iconLeft` prop or a separate Figma-only design element.
    fix_action: >
      After running figma-extract (GAP-001), check whether the leading visuals
      frame (node 69857:19373) maps to the `iconLeft` prop. If so, add a note
      in props.md. If the avatar/status types are not yet implemented in code,
      flag as a design–code gap.
    blocks: []
    dependency: [GAP-001]

warnings:
  - id: WARN-001
    dimension: examples_coverage
    confidence: heuristic
    finding: >
      The Modal example uses `menuPortalTarget={portalTarget}` with a
      callback-style ref `portalRef={el => setPortalTarget(el)}`. This pattern
      relies on the Modal component supporting a `portalRef` prop. If Modal's
      API has changed (or `portalRef` is named differently), the example will
      be incorrect. The example was sourced directly from a Storybook story
      so it was correct at extract time, but should be validated against the
      current @8x8/oxygen-modal release.
    recommendation: >
      Validate the Modal + Select example against the current version of
      @8x8/oxygen-modal before publishing.

  - id: WARN-002
    dimension: token_coverage
    confidence: heuristic
    finding: >
      tokens.md contains a state × token mapping table where most entries use
      placeholder text ("Internal border token", "Internal focus ring", etc.).
      These placeholders were written because the MCP returned no data — they
      are not confirmed token names and will confuse engineers who rely on the
      table for implementation.
    recommendation: >
      Before doc-rewrite, replace or explicitly mark all "Internal xxx token"
      entries as UNKNOWN until resolved via GAP-011.

  - id: WARN-003
    dimension: props_completeness
    confidence: heuristic
    finding: >
      The select-pui.md file uses `<!-- NONE IDENTIFIED -->` markers in each
      section rather than the canonical `<!-- NO RELEVANT PUI CONTEXT -->` marker
      that the doc-audit skill treats as an explicit positive signal. The intent
      is clear but the marker is non-standard. If a future pipeline step does
      a string match for the canonical marker, it will not find it.
    recommendation: >
      Replace the section-level `<!-- NONE IDENTIFIED -->` markers in
      select-pui.md with a single top-level
      `<!-- NO RELEVANT PUI CONTEXT -->` line immediately after the frontmatter
      comment block.
---

# Select — Audit Report

> **Verdict: NO — resolve conflicts before doc-rewrite**
>
> Two deterministic CONFLICTs in the OX MCP source data must be resolved first:
> `isAsync` type (`boolean` vs `IsAsync`) and `ref=` vs `forwardedRef=` prop naming.
> Additionally, `select-figma.md` is a blocker SOURCE_GAP (Desktop Bridge was
> offline). Once GAP-002 and GAP-003 are resolved, and select-figma.md is produced,
> the verdict becomes PARTIAL → YES.

**Audit date:** 2026-04-29 | **Rubric version:** 1.0

---

## File inventory

| File | Status | Lines | Produced by |
|------|--------|-------|-------------|
| `props.md` | ✅ Present | 100 | oxygen-mcp-extract |
| `examples.md` | ✅ Present | 156 | oxygen-mcp-extract |
| `tokens.md` | ✅ Present | 42 | oxygen-mcp-extract |
| `accessibility.md` | ✅ Present | 67 | oxygen-mcp-extract |
| `select-pui.md` | ✅ Present (no PUI context) | 21 | pui-mcp-extract |
| `select-figma.md` | ❌ Missing | — | figma-extract |
| `select-usage.md` | ❌ Missing | — | figma-extract-usage |

---

## Dimension scores

| Dimension | Score | Coverage | Status |
|-----------|-------|----------|--------|
| Props completeness | 0.78 | 33 props present; 2 pass-throughs from examples undocumented; `SelectOption` type undefined | ⚠️ Minor + Major gaps |
| Examples coverage | 0.65 | 7 examples; missing error / disabled / async / size variants | ⚠️ Minor gaps |
| Token coverage | 0.35 | 1 of ~8 expected tokens returned from MCP; state table uses placeholders | ❌ Major source gap |
| Accessibility | 0.78 | Complete inferred structure; not confirmed from source or Figma | ⚠️ Inferred only |
| Figma alignment | 0.15 | No figma.md; only metadata + screenshot captured | ❌ Blocker source gap |
| Usage guidelines | 0.25 | Text-only from OX MCP; no Do/Don't visual examples | ❌ Major source gap |
| Cross-file consistency | 0.78 | 2 deterministic CONFLICTs in source data | ❌ Conflicts |
| **Overall** | **0.53** | | |

---

## Conflicts (must resolve before doc-rewrite)

| ID | Dimension | Finding |
|----|-----------|---------|
| GAP-002 | Cross-file consistency | `isAsync` type: `boolean` (get-component-info) vs `IsAsync` (get-component-props) |
| GAP-003 | Cross-file consistency | `ref=` used in Storybook examples vs `forwardedRef=` documented in props table |

---

## Gaps

### Blockers

| ID | Type | Dimension | Finding |
|----|------|-----------|---------|
| GAP-001 | SOURCE_GAP | Figma alignment | `select-figma.md` missing — Desktop Bridge offline during extract session |

### Major gaps

| ID | Type | Dimension | Finding |
|----|------|-----------|---------|
| GAP-004 | DOC_GAP | Props completeness | `SelectOption` type shape not defined anywhere in docs |
| GAP-011 | SOURCE_GAP | Token coverage | MCP returned only `ui01`; all other state tokens undocumented |
| GAP-014 | SOURCE_GAP | Usage guidelines | `select-usage.md` missing — figma-extract-usage not run |

### Minor gaps

| ID | Type | Dimension | Finding |
|----|------|-----------|---------|
| GAP-005 | DOC_GAP | Props completeness | `menuPortalTarget` used in Modal example but absent from props table |
| GAP-006 | DOC_GAP | Props completeness | `menuPlacement` used in MenuPlacement example but absent from props table |
| GAP-007 | DOC_GAP | Examples coverage | No error state example (`hasError={true}`) |
| GAP-008 | DOC_GAP | Examples coverage | No disabled state example (`isDisabled={true}`) |
| GAP-009 | DOC_GAP | Examples coverage | No async example (`isAsync={true}` + `loadOptions`) |
| GAP-010 | DOC_GAP | Examples coverage | No size variants example |
| GAP-012 | DOC_GAP | Props completeness | `size='default'` ≠ Figma "Medium" — naming discrepancy not explained |
| GAP-013 | SOURCE_GAP | Accessibility | All a11y guidance inferred; not confirmed from source or Figma |
| GAP-015 | SOURCE_GAP | Figma alignment | Leading visuals (icon/status/avatar) in Figma not mapped to `iconLeft` prop |

---

## Warnings (heuristic — advisory only)

| ID | Dimension | Finding |
|----|-----------|---------|
| WARN-001 | Examples | Modal example's `portalRef` usage should be validated against current `@8x8/oxygen-modal` API |
| WARN-002 | Token coverage | "Internal xxx token" placeholders in tokens.md state table are unresolved |
| WARN-003 | Props completeness | `select-pui.md` uses non-canonical marker `<!-- NONE IDENTIFIED -->` instead of `<!-- NO RELEVANT PUI CONTEXT -->` |

---

## What to fix to change verdict to YES

### Step 1 — Resolve CONFLICTs (unblocks doc-rewrite)
| Gap | Action |
|-----|--------|
| GAP-002 | Check `@8x8/oxygen-select` TS exports for `IsAsync` type definition |
| GAP-003 | Confirm whether `React.forwardRef` is used — determines if `ref=` and `forwardedRef=` both work |

### Step 2 — Produce select-figma.md (unblocks figma_alignment + token dimensions)
| Gap | Action |
|-----|--------|
| GAP-001 | Open Desktop Bridge plugin in Figma, run `figma-extract Select` (node 2105:2, file 5YihJ5WuDvnvrlrRMC4sBp) |

### Step 3 — Auto-fixable by doc-rewrite (after conflicts resolved)
| Gap | Fix |
|-----|-----|
| GAP-005 | Add `menuPortalTarget` to props table |
| GAP-006 | Add `menuPlacement` to props table |
| GAP-007 | Add error state example |
| GAP-008 | Add disabled state example |
| GAP-009 | Add async example |
| GAP-010 | Add size variants example |
| GAP-012 | Add `'default'` = Medium mapping note |
| WARN-003 | Fix select-pui.md marker |

### Step 4 — Requires human input
| Gap | Required action |
|-----|----------------|
| GAP-004 | Inspect `@8x8/oxygen-select` for `SelectOption` type definition |
| GAP-011 | Re-run get-theme-tokens with broader terms; inspect component source for token consumption |
| GAP-013 | Inspect rendered DOM to confirm ARIA attributes |
| GAP-014 | Run figma-extract-usage (or request Do/Don't frames from designer) |
| GAP-015 | After figma-extract: map leading visuals frame to `iconLeft` prop |

---

## Suggested next action

1. Resolve GAP-002 and GAP-003 first (quick source checks, unblock everything)
2. Run `figma-extract Select` with Desktop Bridge active
3. Then: `/doc-rewrite Select`

---

_Audit produced by doc-audit skill · Rubric version 1.0 · 2026-04-29_
