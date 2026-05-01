---
component: Link
package: "@8x8/oxygen-link"
rubric_version: "1.0"
extracted: 2026-05-01
audited: 2026-05-01

files_found:
  - props.md
  - examples.md
  - tokens.md
  - accessibility.md
  - Link-figma.md
  - Link-usage.md

files_missing:
  - Link-pui.md  # N/A — confirmed no Platform UI package for Link

scores:
  props: 0.56
  examples: 0.50
  tokens: 0.50
  accessibility: 0.86
  figma: 0.78
  usage: 0.50
  pui: 1.00
  overall: 0.67

counts:
  doc_gaps: 9
  source_gaps: 9
  conflicts: 2
  warnings: 4

verdict: NO
verdict_reason: "2 CONFLICTs must be resolved before doc-rewrite can run (GAP-003: standalone/size type mismatch between MCP and Figma; GAP-012: hover token identity conflict between MCP search and Figma design context)."

gaps:
  - id: GAP-001
    dimension: props
    severity: major
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: true
    evidence:
      source_file: props.md
      location: "## Props table"
      finding: "`href` is the primary anchor attribute for Link but is not listed in the props table. props.md notes 'accepts all standard HTML anchor attributes via prop spread' but does not call out href explicitly."
    fix_action: "Add `href` prop row to the props table (type: string, required: false for flexibility, description: 'URL the link navigates to — passed to the underlying <a> element')."
    blocks: [docusaurus, storybook]
    dependency: []

  - id: GAP-002
    dimension: props
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: true
    evidence:
      source_file: props.md
      location: "## Props table — icon row"
      finding: "The `icon` prop has an empty description in the MCP response and props.md."
    fix_action: "Add description to `icon` prop: 'ReactNode displayed alongside the link label; typically an external-link or directional icon.'"
    blocks: []
    dependency: []

  - id: GAP-003
    dimension: props
    severity: major
    type: CONFLICT
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: props.md + Link-figma.md
      location: "props.md: standalone row (type: false, size: never) vs Link-figma.md: Variant axes (size: Small | Large)"
      finding: "The Oxygen MCP surfaces `standalone: false` and `size: never` — indicating the inline variant only. The Figma component set is named 'Standalone Link' and exposes `size: Small | Large`. This implies a discriminated union in the TypeScript API where standalone and inline are separate prop shapes. The full API is not reflected in the MCP response."
    fix_action: "Inspect @8x8/oxygen-link source to find full LinkProps type. Document both shapes: InlineLinkProps (standalone: false, inherits size) and StandaloneLinkProps (standalone: true, size: Small | Large). Update props.md with the complete union."
    blocks: [docusaurus, storybook, examples.md]
    dependency: []

  - id: GAP-004
    dimension: props
    severity: major
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: Link-figma.md
      location: "## API — Variant axes: isInverted: true | false"
      finding: "`isInverted` is a first-class variant axis in Figma (all 32 variants include it) but is absent from the Oxygen MCP props response. It is either a React prop not surfaced by MCP, or handled via CSS custom property / theme context."
    fix_action: "Check @8x8/oxygen-link source for an `isInverted` prop. If it exists, add to props.md. If it is CSS-only, document as a theming consideration in tokens.md and props.md."
    blocks: [docusaurus]
    dependency: []

  - id: GAP-005
    dimension: props
    severity: minor
    type: SOURCE_GAP
    confidence: heuristic
    auto_fixable: false
    evidence:
      source_file: Link-figma.md
      location: "## API — Boolean toggles: hasIcon"
      finding: "`hasIcon` is a Figma boolean toggle but is absent from the MCP React props. The React API uses an `icon` ReactNode prop instead, which implies `hasIcon` is a Figma-only presentation control."
    fix_action: "Confirm hasIcon is Figma-only. If so, add a note to Link-figma.md clarifying that hasIcon has no React prop equivalent — the icon slot is controlled by passing/omitting the `icon` prop."
    blocks: []
    dependency: []

  - id: GAP-006
    dimension: examples
    severity: major
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: examples.md
      location: "Data gap notice at file top"
      finding: "Oxygen MCP returned 0 clean code examples (get-component-examples with cleanExamples: true returned total: 0). All examples in examples.md are manually inferred, not sourced from MCP or Storybook."
    fix_action: "Source verified code snippets from the internal Storybook or the package README at https://oxygen.8x8.com/docs/components/textlink/usage. Replace inferred examples in examples.md with confirmed ones."
    blocks: [storybook]
    dependency: []

  - id: GAP-007
    dimension: examples
    severity: major
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: examples.md
      location: "Missing section"
      finding: "No standalone variant code example exists in examples.md. The standalone variant is structurally distinct from inline (different size prop, different typography)."
    fix_action: "Add standalone Link example once GAP-003 is resolved and the correct prop shape is confirmed."
    blocks: [docusaurus, storybook]
    dependency: [GAP-003]

  - id: GAP-008
    dimension: tokens
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: true
    evidence:
      source_file: tokens.md
      location: "## Chat surface — action05 row"
      finding: "`$action05` value is listed as '—' in tokens.md. The MCP token search for 'link' did not return this token."
    fix_action: "Run get-theme-tokens with search: 'action05' and populate the light/dark values in the chat surface table."
    blocks: []
    dependency: []

  - id: GAP-009
    dimension: tokens
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: true
    evidence:
      source_file: tokens.md
      location: "## Typography tokens — body02 row"
      finding: "`$body02` typography token is referenced but its size/weight/line-height values were not fetched."
    fix_action: "Run get-theme-tokens with search: 'body02' and add size, weight, and line-height values to the typography token table."
    blocks: []
    dependency: []

  - id: GAP-010
    dimension: tokens
    severity: major
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: true
    evidence:
      source_file: tokens.md + Link-figma.md
      location: "tokens.md: no focus token section; Link-figma.md: Focus ring — Default/Inverted surface tables"
      finding: "Four focus ring tokens are fully documented in Link-figma.md (`focus01`, `focus02`, `ui06`, `ui07` with light/dark hex values) but are entirely absent from tokens.md."
    fix_action: "Add a '## Focus ring tokens' section to tokens.md with `$focus01`, `$focus02`, `$ui06`, `$ui07` rows using values from Link-figma.md."
    blocks: [docusaurus]
    dependency: []

  - id: GAP-011
    dimension: tokens
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: true
    evidence:
      source_file: tokens.md + Link-figma.md
      location: "tokens.md: no active14 row; Link-figma.md: Text label color tables — active14 for default surface"
      finding: "`$active14` is used for the default-surface active state (light: #003486, dark: #ccddf9) in Link-figma.md but is not listed in tokens.md. Only `$active17` (inverted surface) is present."
    fix_action: "Add `$active14` row to the Default surface section in tokens.md with light (#003486) and dark (#ccddf9) values."
    blocks: []
    dependency: []

  - id: GAP-012
    dimension: tokens
    severity: major
    type: CONFLICT
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: tokens.md + Link-figma.md + Link-usage.md
      location: "tokens.md: '$hover07 — Hover background color for links — Light: #246FE5' vs Link-figma.md: '--interactive/hover15 — #0045b3 (Light hover)' vs Link-usage.md: '$hover15'"
      finding: "The MCP token search returned `$hover07` (#246FE5) tagged as 'Hover background color for links'. The Figma design context code and Link-usage.md both use `$hover15` (#0045b3) for the text colour on hover. These are different tokens with different hex values. Possible explanation: $hover07 is a background hover token (not text), while $hover15 is the correct text-colour hover token for links — but this must be confirmed."
    fix_action: "Verify which token is the correct link text hover colour. Cross-reference the Oxygen token dictionary or source CSS. If $hover07 is a background token and $hover15 is the text token, remove $hover07 from tokens.md 'Default surface' and replace with $hover15. Update description accordingly."
    blocks: [docusaurus, tokens.md correctness]
    dependency: []

  - id: GAP-013
    dimension: figma
    severity: major
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: Link-figma.md
      location: "## Anatomy — no inline variant"
      finding: "The Figma component set at node 58315:113 covers only the Standalone variant. The Inline Link variant (which inherits surrounding typography) is not represented as a named component in the scanned Figma canvas. Its anatomy, states, and spacing are undocumented from Figma."
    fix_action: "Locate the Inline Link Figma frame (possibly within a separate page or usage examples canvas) and run figma-extract on that node. If no dedicated Inline component exists, document this explicitly in Link-figma.md."
    blocks: [docusaurus]
    dependency: []

  - id: GAP-014
    dimension: figma
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: Link-figma.md
      location: "## Token coverage — NO COVERAGE DATA comment"
      finding: "figma_get_component with enrich=true failed to return token coverage % because the Desktop Bridge plugin was not running."
    fix_action: "Re-run figma-extract with the Desktop Bridge plugin active to get token coverage percentage."
    blocks: []
    dependency: []

  - id: GAP-015
    dimension: figma
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: Link-figma.md
      location: "## Text styles — NO EFFECT STYLES comment"
      finding: "figma_get_styles returned 0 styles. Text style names (e.g. 'Body/Body02 Semi Bold') are not captured in Link-figma.md."
    fix_action: "Re-run figma_get_styles with Desktop Bridge plugin active to retrieve named text and effect styles."
    blocks: []
    dependency: []

  - id: GAP-016
    dimension: figma
    severity: minor
    type: SOURCE_GAP
    confidence: heuristic
    auto_fixable: false
    evidence:
      source_file: Link-figma.md
      location: "## Gaps & conflicts — Missing variant row"
      finding: "No `isDisabled` state exists in Figma or the MCP API. Intentionality is unconfirmed — could be design decision, oversight, or handled via CSS pointer-events."
    fix_action: "Confirm with component owner. If intentionally unsupported, add a note to props.md. If handled via CSS, document the recommended implementation pattern."
    blocks: []
    dependency: []

  - id: GAP-017
    dimension: usage
    severity: major
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: Link-usage.md
      location: "File header: PAIRS: 0"
      finding: "The Figma page at node 58394:123 uses a narrative documentation format instead of the ✅ Do / ❌ Don't card template. figma-extract-usage encountered two hard stops: Desktop Bridge not running + no Do/Don't frames found."
    fix_action: "Request designer to create ✅ Do / ❌ Don't card frames in the Figma examples page following the standard template. Re-run figma-extract-usage once cards are in place."
    blocks: [docusaurus]
    dependency: []

  - id: GAP-018
    dimension: usage
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: Link-usage.md
      location: "## Accessible external links section"
      finding: "A ✅/❌ pattern was visible in the Figma screenshot for the 'Accessible external link' section, but text was too small to read accurately. Desktop Bridge was not running to access the text nodes directly."
    fix_action: "Extract verbatim text from the accessible external link guidance using Desktop Bridge or by requesting content from the designer."
    blocks: []
    dependency: []

  - id: GAP-019
    dimension: accessibility
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: accessibility.md
      location: "File header data gap notice"
      finding: "Oxygen MCP returned no explicit accessibility documentation for Link. All a11y content in accessibility.md is inferred from the component's nature (wraps <a>) and WCAG 2.1 AA requirements, not sourced from official documentation."
    fix_action: "Cross-reference accessibility.md against the official Oxygen docs at https://oxygen.8x8.com/docs/components/textlink/usage for any official a11y guidance. Update any inferences that conflict with official statements."
    blocks: []
    dependency: []

  - id: GAP-020
    dimension: accessibility
    severity: minor
    type: DOC_GAP
    confidence: heuristic
    auto_fixable: false
    evidence:
      source_file: accessibility.md
      location: "## Color and contrast table"
      finding: "Contrast ratios are stated as '≥ 4.5:1' for action08 on white but no actual computed ratios are provided. Hover (#246FE5 or #0045b3) and visited (#73348C) states are flagged 'Check against surface' without values."
    fix_action: "Compute actual contrast ratios for all token×surface combinations (at minimum: action08 on ui01, hover15 on ui01, textColor08 on ui01) and add to the contrast table."
    blocks: []
    dependency: [GAP-012]

warnings:
  - id: WARN-001
    dimension: props
    finding: "The `mode` Figma property (Light/Dark) has no documented React equivalent. It is likely handled by CSS theme context, not a prop — but this is unconfirmed."
    action: "Verify with source code. If CSS-only, add a theming note to props.md."

  - id: WARN-002
    dimension: examples
    finding: "The chat surface example uses `isChat` but the token it activates ($action05 vs $action07) depends on the parent surface — this logic is not explained in examples.md."
    action: "Add inline comment or note to the chat example clarifying which token is applied and when."

  - id: WARN-003
    dimension: figma
    finding: "The `items-start` alignment on the container auto-layout may cause visual misalignment when combining multi-line text with an icon. The figma-extract did not capture whether this is the correct alignment for all use cases."
    action: "Verify intended alignment for icon + multi-line label. If items-center is also valid, document both patterns."

  - id: WARN-004
    dimension: accessibility
    finding: "accessibility.md documents WCAG 1.4.1 (Use of Color) requiring a non-color link indicator, but only the hover/focus/active states show underlines. The rest state has no underline. This may conflict with 1.4.1 for inline links."
    action: "Confirm whether rest-state underline is required for inline links. If not, document the design decision and contrast-based justification."
---

# Link — Documentation Audit

> **Verdict: NO** — 2 conflicts must be resolved before `doc-rewrite` can run.
>
> Resolve GAP-003 (standalone/size prop type conflict) and GAP-012 (hover token conflict) first.

**Audited:** 2026-05-01 · **Rubric:** v1.0

---

## File inventory

| File | Status | Notes |
|------|--------|-------|
| `props.md` | ✅ Present | 6 props documented; type anomalies on `standalone` and `size` |
| `examples.md` | ✅ Present | 4 examples but all manually inferred; MCP returned 0 clean examples |
| `tokens.md` | ✅ Present | Partial — missing focus, active14, body02; hover token conflict |
| `accessibility.md` | ✅ Present | Strong; content inferred, not officially sourced |
| `Link-figma.md` | ✅ Present | 32 variants documented; inline variant missing |
| `Link-usage.md` | ✅ Present | Narrative format; no Do/Don't cards |
| `Link-pui.md` | ➖ N/A | No Platform UI package for Link (confirmed) |

---

## Dimension scores

| Dimension | Score | Coverage | Key issues |
|-----------|-------|----------|------------|
| Props | 0.56 | 5/9 | GAP-003 (CONFLICT), GAP-004, missing href, icon desc |
| Examples | 0.50 | 3/6 | GAP-006 (0 MCP examples), GAP-007 (no standalone example) |
| Tokens | 0.50 | 4/8 | GAP-012 (CONFLICT), GAP-010 (focus tokens missing) |
| Accessibility | 0.86 | 6/7 | GAP-019 (inferred, not sourced) |
| Figma | 0.78 | 7/9 | GAP-013 (inline variant absent), GAP-016 (isDisabled unknown) |
| Usage | 0.50 | 3/6 | GAP-017 (no Do/Don't cards) |
| PUI | 1.00 | N/A | Confirmed not applicable |
| **Overall** | **0.67** | | |

---

## Conflicts — must resolve before rewrite

### GAP-003 · Props · CONFLICT · major

**Finding:** `standalone` prop type is `false` and `size` is `never` in the MCP API (inline-variant shape only). The Figma component set is named "Standalone Link" and exposes `size: Small | Large`. A discriminated union likely exists in `LinkProps` but the full shape is not reflected in MCP data.

**Fix:** Inspect `@8x8/oxygen-link` TypeScript source. Document both `InlineLinkProps` and `StandaloneLinkProps` shapes in `props.md`.

---

### GAP-012 · Tokens · CONFLICT · major

**Finding:** MCP token search returned `$hover07` (#246FE5) described as "Hover background color for links". Figma design context and usage.md both use `$hover15` (#0045b3) as the link text colour on hover. These are different tokens with different hex values and different roles.

**Fix:** Verify intent — `$hover07` may be a background hover, not a text hover token. Correct `tokens.md` to use `$hover15` if that is the actual link text hover colour. Remove or reclassify `$hover07`.

---

## Gaps by dimension

### Props (GAP-001 – GAP-005)

| ID | Severity | Type | Summary |
|----|----------|------|---------|
| GAP-001 | major | DOC_GAP | `href` not listed in props table |
| GAP-002 | minor | DOC_GAP | `icon` prop has no description |
| GAP-003 | major | CONFLICT | standalone/size prop type mismatch between MCP and Figma |
| GAP-004 | major | SOURCE_GAP | `isInverted` in Figma but absent from React API |
| GAP-005 | minor | SOURCE_GAP | `hasIcon` is Figma-only; React uses `icon` prop instead |

### Examples (GAP-006 – GAP-007)

| ID | Severity | Type | Summary |
|----|----------|------|---------|
| GAP-006 | major | SOURCE_GAP | MCP returned 0 clean examples; all are inferred |
| GAP-007 | major | DOC_GAP | No standalone variant code example |

### Tokens (GAP-008 – GAP-012)

| ID | Severity | Type | Summary |
|----|----------|------|---------|
| GAP-008 | minor | DOC_GAP | `$action05` value missing |
| GAP-009 | minor | DOC_GAP | `$body02` typography token values not fetched |
| GAP-010 | major | DOC_GAP | Focus ring tokens absent from tokens.md |
| GAP-011 | minor | DOC_GAP | `$active14` (default surface active) missing from tokens.md |
| GAP-012 | major | CONFLICT | `$hover07` (MCP) vs `$hover15` (Figma) — different tokens |

### Figma (GAP-013 – GAP-016)

| ID | Severity | Type | Summary |
|----|----------|------|---------|
| GAP-013 | major | SOURCE_GAP | Inline Link variant not in Figma component set |
| GAP-014 | minor | SOURCE_GAP | Token coverage % unavailable (Desktop Bridge offline) |
| GAP-015 | minor | SOURCE_GAP | Figma style names unavailable (figma_get_styles returned 0) |
| GAP-016 | minor | SOURCE_GAP | `isDisabled` intentionality unconfirmed |

### Usage (GAP-017 – GAP-018)

| ID | Severity | Type | Summary |
|----|----------|------|---------|
| GAP-017 | major | SOURCE_GAP | No Do/Don't cards — Figma page uses narrative format |
| GAP-018 | minor | SOURCE_GAP | "Accessible external link" section text not extracted |

### Accessibility (GAP-019 – GAP-020)

| ID | Severity | Type | Summary |
|----|----------|------|---------|
| GAP-019 | minor | SOURCE_GAP | A11y content inferred from component type, not official source |
| GAP-020 | minor | DOC_GAP | Contrast ratios not computed; stated as approximate |

---

## Warnings (heuristic — advisory only)

| ID | Dimension | Finding |
|----|-----------|---------|
| WARN-001 | Props | `mode` Figma property has no confirmed React equivalent |
| WARN-002 | Examples | Chat surface example doesn't explain $action05 vs $action07 token selection logic |
| WARN-003 | Figma | `items-start` alignment may misalign icon with multi-line text |
| WARN-004 | Accessibility | Rest-state has no underline — may conflict with WCAG 1.4.1 for inline links |

---

## Suggested next actions

1. **Resolve GAP-003** — inspect `@8x8/oxygen-link` source for full `LinkProps` discriminated union
2. **Resolve GAP-012** — verify `$hover07` vs `$hover15` in the Oxygen token dictionary
3. **Fix GAP-001, GAP-002, GAP-010, GAP-011** — doc-rewrite can handle these once conflicts are clear
4. **Enable Desktop Bridge** and re-run `figma-extract` to close GAP-013, GAP-014, GAP-015
5. **Request designer** to add Do/Don't card frames (GAP-017)

_Source: doc-audit skill v1.0 · Extracted files in component-lib/Link/ · Audited 2026-05-01_
