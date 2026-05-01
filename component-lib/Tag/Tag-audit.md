---
component: Tag
package: "@8x8/oxygen-tag"
rubric_version: "1.0"
extracted: 2026-05-01
audited: 2026-05-01

files_found:
  - props.md
  - examples.md
  - tokens.md
  - accessibility.md
  - Tag-figma.md
  - figma-screenshot-tag.png  # bonus asset, not a scored file

files_missing:
  - Tag-usage.md  # SOURCE_GAP — figma-extract-usage hard-stopped (no Do/Don't frames on examples page)
  - Tag-pui.md    # N/A — confirmed no Platform UI relevance (PUI MCP search returned only MFE false positives)

scores:
  props: 0.75
  examples: 0.55
  tokens: 0.83
  accessibility: 0.80
  figma: 0.75
  usage: 0.20
  pui: 1.00
  overall: 0.70

counts:
  doc_gaps: 2
  source_gaps: 10
  conflicts: 0
  warnings: 3

verdict: YES
verdict_reason: "Zero CONFLICTs and zero blocker-severity gaps — all four required files (props.md, examples.md, Tag-figma.md, accessibility.md) are present. doc-rewrite can proceed. Major gaps (GAP-003: inferred examples; GAP-011: no usage guidance) will limit doc-rewrite output quality for those dimensions."

gaps:
  - id: GAP-001
    dimension: props
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: props.md
      location: "## Tag > Gap note at bottom — '## Variant matching: code vs Figma'"
      finding: "The leading icon delivery mechanism is unconfirmed. props.md notes 'verify how an icon is supplied in code — it may be the first React element in children'. The Figma `icon?` boolean controls an instance-swap slot, but the React API equivalent (children-first-element vs a dedicated icon prop) is not verified from package source."
    fix_action: "Inspect @8x8/oxygen-tag source to confirm whether the leading icon is passed via children (first ReactElement) or a dedicated icon prop. Update props.md with the confirmed mechanism and add a verified example."
    blocks: [docusaurus, examples.md]
    dependency: []

  - id: GAP-002
    dimension: props
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: props.md
      location: "### variant values > Note paragraph"
      finding: "The `Variant` TypeScript type alias is opaque in the Oxygen MCP response. The seven variant values (default, blue, grey, red, yellow, green, yellow-emphasis) are sourced from the Figma `color` axis, not from the TypeScript type definition."
    fix_action: "Check @8x8/oxygen-tag TypeScript types for the Variant union. Confirm all 7 values are present and correctly named. Update props.md if any differ."
    blocks: []
    dependency: []

  - id: GAP-003
    dimension: examples
    severity: major
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: examples.md
      location: "File header data gap notice"
      finding: "Oxygen MCP get-component-examples returned 0 clean Storybook examples for @8x8/oxygen-tag — only a TagDocumentation Storybook wrapper was found. All examples in examples.md are constructed from observed props and Figma examples page content, not from package source or official documentation."
    fix_action: "Source verified code snippets from the internal Storybook (https://oxygen.8x8.dev/packages/release/latest/?path=/story/components-tag--guidelines) or the package README. Replace inferred examples with confirmed ones once available."
    blocks: [storybook]
    dependency: []

  - id: GAP-004
    dimension: examples
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: examples.md
      location: "## Standard Tag with leading icon > comment"
      finding: "The leading icon example includes a caveat — 'verify with the package source if a dedicated icon prop is required'. The example may be incorrect if the icon is not passed via children."
    fix_action: "Once GAP-001 is resolved, update the leading icon example with the confirmed prop usage pattern and remove the verification caveat."
    blocks: []
    dependency: [GAP-001]

  - id: GAP-005
    dimension: tokens
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: tokens.md + Tag-figma.md
      location: "tokens.md has no close-button section; Tag-figma.md > 'Sub-component sizing'"
      finding: "The close button (×) is a sub-component (CloseButton.tsx in packages/tag/src/components/CloseButton.tsx). Its icon color token and any hover/pressed state tokens are not captured in tokens.md. The extraction only covered container-level tokens."
    fix_action: "Inspect CloseButton.tsx source or run get-theme-tokens with relevant search terms to identify the × icon color token. Add a 'Close button tokens' section to tokens.md."
    blocks: []
    dependency: []

  - id: GAP-006
    dimension: tokens
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: Tag-figma.md
      location: "## Token coverage — 'Token coverage % not returned'"
      finding: "Figma Variables API was unavailable during extraction (Desktop Bridge not connected; Enterprise plan required for Variables API). All token names were inferred from CSS variable fallback paths in the design context code (e.g. var(--ui/ui01, #ebeae1)). Actual variable collection structure and binding assignments are unconfirmed."
    fix_action: "Re-run figma-extract with the Desktop Bridge plugin active and Figma Variables API available to confirm token bindings and collection structure."
    blocks: []
    dependency: []

  - id: GAP-007
    dimension: figma
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: Tag-figma.md
      location: "## Design decisions & annotations > 'Standard Tag description (Figma)'"
      finding: "The Standard Tag Figma component description links to https://oxygen.8x8.com/docs/Contribution/intro (the contribution guide), not the Tag component documentation. This is a Figma authoring error — the URL is a placeholder."
    fix_action: "Request designer or component owner to update the Figma component description URL to the correct Tag usage page (likely https://oxygen.8x8.com/components/tag/usage or equivalent)."
    blocks: []
    dependency: []

  - id: GAP-008
    dimension: figma
    severity: minor
    type: SOURCE_GAP
    confidence: heuristic
    auto_fixable: false
    evidence:
      source_file: Tag-figma.md
      location: "## Avatar Tag — Variant axes > Note"
      finding: "Avatar Tag omits the yellow and green color variants present in Standard Tag (Avatar Tag has 5 colors vs Standard Tag's 7). No Figma annotation explains the exclusion. The omission may be intentional (status tags with avatar faces are less common) or an oversight."
    fix_action: "Confirm with component owner whether yellow/green exclusion from Avatar Tag is intentional. If intentional, add a design rationale note to Tag-figma.md and the variant table in props.md. If an oversight, request the designer to add the missing variants."
    blocks: []
    dependency: []

  - id: GAP-009
    dimension: figma
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: Tag-figma.md
      location: "## Interaction states > 'No hover or active/pressed states'"
      finding: "Neither the Standard Tag nor the Avatar Tag component set includes hover or pressed/active state variants in Figma. The close button likely has hover/active styling in code but these states are not modelled at the design layer."
    fix_action: "Request designer to add hover and pressed states to the Figma component sets. Alternatively, verify these states in CloseButton.tsx implementation and document them in accessibility.md and Tag-figma.md."
    blocks: []
    dependency: []

  - id: GAP-010
    dimension: figma
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: Tag-figma.md
      location: "## Text styles > Effect styles comment — 'NO EFFECT STYLES FOUND IN FIGMA RESPONSE'"
      finding: "figma_get_styles returned 0 styles. Named text and effect styles (e.g. typography style names like 'Label/Label01') are not captured in Tag-figma.md."
    fix_action: "Re-run figma_get_styles with the Desktop Bridge plugin active to retrieve named text and effect styles. Confirm that label01 is the correct style name."
    blocks: []
    dependency: []

  - id: GAP-011
    dimension: usage
    severity: major
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: "(Tag-usage.md — not written)"
      location: "figma-extract-usage run result"
      finding: "figma-extract-usage hard-stopped on both conditions: (1) Desktop Bridge was not connected; (2) the Figma examples page (node 52829:11107) contains anatomy/type documentation sections, not ✅ Do / ❌ Don't card frames. No usage guidance pairs were found. Tag-usage.md was not written."
    fix_action: "Request designer to create ✅ Do / ❌ Don't card frames in the Figma examples page following the standard template. Re-run figma-extract-usage once frames are in place."
    blocks: [docusaurus]
    dependency: []

  - id: GAP-012
    dimension: accessibility
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: accessibility.md
      location: "File header — 'Note: Oxygen MCP returned no explicit accessibility data for Tag'"
      finding: "All accessibility content in accessibility.md is inferred from the component's dual-mode nature (display-only vs interactive with action) and WCAG 2.1 AA requirements. No official accessibility documentation was returned by the Oxygen MCP, and Figma carries no accessibility annotations on the Tag component."
    fix_action: "Cross-reference accessibility.md against the official Oxygen Storybook (https://oxygen.8x8.dev/packages/release/latest/?path=/story/components-tag--guidelines) for any official a11y notes. Update any inferences that conflict with official guidance."
    blocks: []
    dependency: []

warnings:
  - id: WARN-001
    dimension: props
    finding: "The Figma `mode` property (light/dark) has no React prop equivalent — it is handled by the theme CSS context, not a direct prop. This is standard Oxygen pattern but is not explicitly documented in props.md."
    action: "Add a theming note to props.md clarifying that light/dark mode is controlled by the parent theme provider, not a Tag prop."

  - id: WARN-002
    dimension: accessibility
    finding: "Contrast ratios in the WCAG table in accessibility.md are computed from token hex values resolved via the Oxygen MCP (get-theme-tokens). They have not been validated against a browser-based contrast checker tool or in an actual rendered environment."
    action: "Run the 7-variant × 2-mode contrast pairs through a WCAG contrast checker (e.g. WebAIM) against realistic surface backgrounds. Update ratios if any discrepancies are found."

  - id: WARN-003
    dimension: figma
    finding: "The Figma examples page uses 'Amber' as the display name for the yellow variant in the RAG pattern (Red/Amber/Green). In the React API the prop value is variant='yellow'. If the spec or usage guidance ever refers to 'Amber', it should cross-reference variant='yellow' to prevent confusion."
    action: "When writing Tag-spec.md, ensure that RAG guidance maps 'Amber' to variant='yellow' explicitly."
---

# Tag — Documentation Audit

> **Verdict: YES** — No conflicts; no blocker gaps. `doc-rewrite` can proceed.
>
> Major caveats: all examples are inferred (GAP-003) and no usage Do/Don't guidance exists (GAP-011). The spec will be solid on props, tokens, and accessibility but weak on curated examples and editorial usage guidance until those source gaps are resolved.

**Audited:** 2026-05-01 · **Rubric:** v1.0

---

## File inventory

| File | Status | Notes |
|------|--------|-------|
| `props.md` | ✅ Present | 8 props; variant values from Figma (type alias opaque in MCP) |
| `examples.md` | ✅ Present | 14 examples — all inferred; MCP returned 0 clean snippets |
| `tokens.md` | ✅ Present | 13 tokens; strong coverage; close button × token missing |
| `accessibility.md` | ✅ Present | Full WCAG checklist; all content inferred — no official source |
| `Tag-figma.md` | ✅ Present | Two component sets; full token tables; hardcoded spacings noted |
| `figma-screenshot-tag.png` | ✅ Present | Canvas screenshot (Standard + Avatar sets) |
| `Tag-usage.md` | ❌ Missing | SOURCE_GAP — no Do/Don't frames on Figma examples page |
| `Tag-pui.md` | ➖ N/A | Confirmed no Platform UI relevance |

---

## Dimension scores

| Dimension | Score | Coverage | Key issues |
|-----------|-------|----------|------------|
| Props | 0.75 | 6/8 | GAP-001 (icon mechanism), GAP-002 (Variant type opaque) |
| Examples | 0.55 | 4/7 | GAP-003 (0 MCP examples — all inferred), GAP-004 (icon example unverified) |
| Tokens | 0.83 | 9/11 | GAP-005 (close button × token), GAP-006 (variable bindings unconfirmed) |
| Accessibility | 0.80 | 6/7 | GAP-012 (all content inferred, not officially sourced) |
| Figma | 0.75 | 7/9 | GAP-008 (Avatar Tag yellow/green unconfirmed), GAP-009 (no hover states) |
| Usage | 0.20 | 0/1 | GAP-011 (no file — no Do/Don't frames in Figma) |
| PUI | 1.00 | N/A | Confirmed not applicable |
| **Overall** | **0.70** | | |

---

## Gaps by dimension

### Props (GAP-001 – GAP-002)

| ID | Severity | Type | Summary |
|----|----------|------|---------|
| GAP-001 | minor | SOURCE_GAP | Leading icon delivery mechanism unconfirmed (children vs dedicated prop) |
| GAP-002 | minor | SOURCE_GAP | `Variant` type alias opaque in MCP — values sourced from Figma only |

### Examples (GAP-003 – GAP-004)

| ID | Severity | Type | Summary |
|----|----------|------|---------|
| GAP-003 | major | SOURCE_GAP | Oxygen MCP returned 0 clean examples — all are inferred |
| GAP-004 | minor | DOC_GAP | Leading icon example marked as unverified; depends on GAP-001 |

### Tokens (GAP-005 – GAP-006)

| ID | Severity | Type | Summary |
|----|----------|------|---------|
| GAP-005 | minor | SOURCE_GAP | Close button (×) icon color token not captured |
| GAP-006 | minor | SOURCE_GAP | Token names inferred from CSS fallbacks; Figma Variables API unavailable |

### Figma (GAP-007 – GAP-010)

| ID | Severity | Type | Summary |
|----|----------|------|---------|
| GAP-007 | minor | DOC_GAP | Standard Tag Figma description links to contribution guide (incorrect URL) |
| GAP-008 | minor | SOURCE_GAP | Avatar Tag yellow/green exclusion — intentionality unconfirmed |
| GAP-009 | minor | SOURCE_GAP | No hover/pressed states in Figma component sets |
| GAP-010 | minor | SOURCE_GAP | Effect/text styles unavailable (figma_get_styles returned 0) |

### Usage (GAP-011)

| ID | Severity | Type | Summary |
|----|----------|------|---------|
| GAP-011 | major | SOURCE_GAP | Tag-usage.md not written — no Do/Don't frames on Figma examples page |

### Accessibility (GAP-012)

| ID | Severity | Type | Summary |
|----|----------|------|---------|
| GAP-012 | minor | SOURCE_GAP | All a11y content inferred — no official Oxygen accessibility source |

---

## Warnings (heuristic — advisory only)

| ID | Dimension | Finding |
|----|-----------|---------|
| WARN-001 | Props | `mode` Figma property has no React equivalent — handled by CSS theme context; undocumented in props.md |
| WARN-002 | Accessibility | Contrast ratios computed from token hex values, not validated in a browser contrast tool |
| WARN-003 | Figma | RAG pattern calls yellow variant "Amber" — spec should explicitly cross-reference `variant='yellow'` |

---

## Suggested next actions

1. **Run `doc-rewrite`** — verdict is YES; proceed with Tag-spec.md
2. **Resolve GAP-001** — inspect `@8x8/oxygen-tag` source for leading icon prop mechanism; update props.md and examples.md
3. **Resolve GAP-003** — source verified Storybook examples once the Oxygen team adds them (scheduled check: 2026-05-08)
4. **Resolve GAP-011** — request designer to add Do/Don't card frames to the Figma examples page; re-run `figma-extract-usage`
5. **Confirm GAP-008** — ask component owner whether Avatar Tag yellow/green omission is intentional

_Source: doc-audit skill v1.0 · Extracted files in component-lib/Tag/ · Audited 2026-05-01_
