---
component: Label
package: "@8x8/oxygen-label"
rubric_version: "1.0"
extracted: 2026-05-01
audited: 2026-05-01
verdict: "NO"
verdict_reason: "2 unresolved CONFLICTs — token names/sizes diverge between MCP and Figma; Figma information boolean mapping to Oxygen infoBox props unverified"

files_found:
  - props.md
  - examples.md
  - tokens.md
  - accessibility.md
  - Label-figma.md
  - label-pui.md

files_missing:
  - label-usage.md   # Desktop Bridge not connected — figma-extract-usage hard-stopped

scores:
  props:         { score: 0.82, coverage: "12/14 props fully sourced", note: "11 prop descriptions heuristically derived; 2 opaque types" }
  examples:      { score: 0.65, coverage: "7 examples present but none sourced from Storybook", note: "MCP returned 0 clean snippets; examples derived from prop shapes" }
  tokens:        { score: 0.50, coverage: "3 tokens documented; CONFLICT on token identity/size vs Figma", note: "label01 (12px MCP) vs typography/body01 (14px Figma)" }
  accessibility: { score: 0.82, coverage: "ARIA, keyboard, WCAG 2.1 AA checklist present", note: "All content inferred from component nature — no MCP or Figma source data" }
  figma:         { score: 0.78, coverage: "Anatomy + tokens + spacing + component properties confirmed via Desktop Bridge", note: "GAP-013/GAP-014 resolved; isDisabled variant still missing from Figma" }
  usage:         { score: 0.00, coverage: "0/1 — file missing", note: "SOURCE_GAP: Desktop Bridge required for figma-extract-usage" }
  pui:           { score: 1.00, coverage: "PASS — NO RELEVANT PUI CONTEXT confirmed", note: "" }

counts:
  doc_gaps: 10
  source_gaps: 4   # GAP-013 and GAP-014 resolved 2026-05-01 via Desktop Bridge
  conflicts: 2
  warnings: 3

gaps:

  - id: GAP-001
    dimension: props
    severity: minor
    type: DOC_GAP
    confidence: heuristic
    auto_fixable: false
    evidence:
      source_file: props.md
      location: "Props table, infoBoxShowOn row"
      finding: "`infoBoxShowOn` type is `keyof typeof showOn` — the `showOn` enum values are not listed. Consumers cannot know the valid string literals."
    fix_action: "Look up the `showOn` enum in `@8x8/oxygen-label` source and document the accepted string values (e.g. `hover`, `click`)."
    blocks: [docusaurus]
    dependency: []

  - id: GAP-002
    dimension: props
    severity: minor
    type: DOC_GAP
    confidence: heuristic
    auto_fixable: false
    evidence:
      source_file: props.md
      location: "Props table, action row"
      finding: "`action` type is `ActionProps['action']` — `ActionProps` is an internal type not expanded or linked. Consumers cannot tell if it is a React event handler, a callback signature, or a URL string."
    fix_action: "Expand the `action` type signature or add a note describing the function signature (e.g. `() => void` or `(event: MouseEvent) => void`)."
    blocks: [docusaurus, storybook]
    dependency: []

  - id: GAP-003
    dimension: props
    severity: minor
    type: DOC_GAP
    confidence: heuristic
    auto_fixable: false
    evidence:
      source_file: props.md
      location: "Props table — 11 rows: value, action, actionLabel, actionTarget, htmlFor, infoBoxText, infoBoxShowOn, infoBoxButtonLabel, shouldWrapText, showTooltipOnOverflow, otherActionProps"
      finding: "MCP returned empty string descriptions for these 11 props. Descriptions in props.md were written by the extractor based on prop names and context, not sourced from MCP or Figma annotations."
    fix_action: "Verify each description against actual component source or Storybook docs. Flag any that are inaccurate."
    blocks: []
    dependency: []

  - id: GAP-004
    dimension: examples
    severity: minor
    type: DOC_GAP
    confidence: heuristic
    auto_fixable: false
    evidence:
      source_file: examples.md
      location: "Footer note: 'MCP returned no clean Storybook snippets… Verify against Storybook before production use.'"
      finding: "All 7 examples were derived from prop shapes, not extracted from actual Storybook stories. The MCP returned 0 clean examples for this component."
    fix_action: "Run `get-component-examples` again after Storybook examples are added upstream, or manually copy verified snippets from the live Storybook."
    blocks: [storybook]
    dependency: []

  - id: GAP-005
    dimension: examples
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: true
    evidence:
      source_file: examples.md
      location: "No example uses the actionTarget prop"
      finding: "`actionTarget` prop (type: `ActionTarget`) is listed in props.md but no example demonstrates it."
    fix_action: "Add an example showing `actionTarget` usage alongside `action` and `actionLabel` (e.g. `actionTarget=\"_blank\"`)."
    blocks: []
    dependency: [GAP-002]

  - id: GAP-006
    dimension: examples
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: examples.md
      location: "No example uses infoBoxShowOn"
      finding: "`infoBoxShowOn` is not demonstrated in any example."
    fix_action: "Add an example showing `infoBoxShowOn` once the accepted values are known (dependency: GAP-001)."
    blocks: []
    dependency: [GAP-001]

  - id: GAP-007
    dimension: examples
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: true
    evidence:
      source_file: examples.md
      location: "No example uses otherActionProps"
      finding: "`otherActionProps` is not demonstrated in any example."
    fix_action: "Add a brief example or note in the action link example showing typical forwarded props (e.g. `data-*` attributes)."
    blocks: []
    dependency: []

  - id: GAP-008
    dimension: tokens
    severity: blocker
    type: CONFLICT
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: tokens.md
      location: "Typography tokens table: label01 (0.75rem / 12px), labelBold01 (0.75rem / 12px)"
      finding: |
        MCP tokens.md records `label01` / `labelBold01` at **0.75rem (12px)** / 1rem line-height.
        Figma design context (Label-figma.md) records `typography/body01` / `typography/bodyBold01` at **14px** / 20px line-height.
        These are different token names AND different sizes. It is unclear whether:
        (a) the Label component uses `label01` tokens (12px) as listed by MCP, or
        (b) the actual rendered text uses `body01` tokens (14px) as seen in Figma.
        This is a direct contradiction between the two authoritative sources.
    fix_action: "Inspect the `@8x8/oxygen-label` component source to determine which token(s) are applied to the label text. Correct tokens.md and Label-figma.md to agree."
    blocks: [docusaurus, storybook, spec]
    dependency: []

  - id: GAP-009
    dimension: tokens
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: true
    evidence:
      source_file: tokens.md
      location: "tokens.md has no entry for error/error01"
      finding: "Label-figma.md documents `error/error01` (light: #cb2233, dark: #f24d5f) as the color for the required asterisk. This token is absent from tokens.md."
    fix_action: "Add `error/error01` to tokens.md with its light/dark values and describe its role (required indicator color)."
    blocks: []
    dependency: []

  - id: GAP-010
    dimension: accessibility
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: Label-figma.md
      location: "Accessibility section: '<!-- NOT ANNOTATED IN FIGMA -->'"
      finding: "No ARIA role, focus order, or keyboard interaction annotations exist in the Figma file for this component."
    fix_action: "Designer must add accessibility annotations to the Figma component (ARIA role, focus order, keyboard interactions)."
    blocks: []
    dependency: []

  - id: GAP-011
    dimension: accessibility
    severity: minor
    type: DOC_GAP
    confidence: heuristic
    auto_fixable: false
    evidence:
      source_file: accessibility.md
      location: "Overview: 'MCP returned no explicit accessibility documentation'"
      finding: "All accessibility content was inferred from component nature and HTML semantics. No MCP or Figma source data confirmed it."
    fix_action: "Verify accessibility guidance against component source / published Oxygen docs. Flag any inferred items that are incorrect."
    blocks: []
    dependency: []

  - id: GAP-012
    dimension: accessibility
    severity: minor
    type: DOC_GAP
    confidence: heuristic
    auto_fixable: false
    evidence:
      source_file: accessibility.md
      location: "Disabled state section"
      finding: "Disabled state visual treatment (e.g. reduced opacity, muted color token) is not documented. The disabled color token is unknown — the MCP did not return it and Figma has no disabled variant."
    fix_action: "Find the disabled color token(s) applied by the component (likely a `textColorDisabled` or similar) and add to both tokens.md and accessibility.md."
    blocks: []
    dependency: [GAP-015]

  - id: GAP-013
    dimension: figma
    severity: major
    type: SOURCE_GAP
    status: RESOLVED
    resolved: 2026-05-01
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: Label-figma.md
      location: "Gaps & conflicts table (updated)"
      finding: "Desktop Bridge connected 2026-05-01. Component properties confirmed via `desktop_bridge_plugin` source: text (TEXT, default 'Label'), information? (BOOLEAN, default true), isRequired? (BOOLEAN, default true), mode (VARIANT, light/dark, default light). description: null, annotations: [] confirmed."
    fix_action: "RESOLVED — no further action needed."
    blocks: []
    dependency: []

  - id: GAP-014
    dimension: figma
    severity: major
    type: SOURCE_GAP
    status: RESOLVED
    resolved: 2026-05-01
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: Label-figma.md
      location: "Gaps & conflicts table (updated)"
      finding: "figma_get_variables returned empty (variables: [], variableCollections: []). This is expected — variables and styles are defined in a linked library file, not in this UI-components file. CSS variable references from design context (e.g. --text/textColor01, --typography/body01) are valid token names from that library."
    fix_action: "RESOLVED — token names from design context are valid. No local variables to verify."
    blocks: []
    dependency: []

  - id: GAP-015
    dimension: figma
    severity: major
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: Label-figma.md
      location: "Gaps & conflicts: 'isDisabled state not present as a Figma variant'"
      finding: "The `isDisabled` prop exists in Oxygen but has no corresponding Figma variant. The visual treatment of the disabled label (color, opacity) is undocumented in Figma."
    fix_action: "Designer must add a `Disabled` variant to the `_base_form_label` Figma component showing the muted/disabled visual state."
    blocks: [spec]
    dependency: []

  - id: GAP-016
    dimension: figma
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: Label-figma.md
      location: "Structure section: 'Text wrapping: not visible in Figma variants (no shouldWrapText variant present)'"
      finding: "`shouldWrapText` and `showTooltipOnOverflow` behaviours have no Figma variant representation. Layout impact is undocumented."
    fix_action: "Designer to add Figma variants showing wrapped text and overflow tooltip states, or document the behaviour expectation in Figma annotations."
    blocks: []
    dependency: []

  - id: GAP-017
    dimension: figma
    severity: blocker
    type: CONFLICT
    confidence: heuristic
    auto_fixable: false
    evidence:
      source_file: Label-figma.md
      location: "Gaps & conflicts: 'Figma information boolean maps to Oxygen infoBoxText / infoBoxButtonLabel props — alignment needs verification'"
      finding: |
        Figma models the info icon as a single boolean `information` (true/false = show/hide).
        Oxygen models it as two separate props: `infoBoxText` (content) and `infoBoxButtonLabel` (a11y label), with an optional `infoBoxShowOn` trigger.
        It is unclear whether:
        (a) the Figma boolean is simply a simplified design representation of the same feature, or
        (b) there is a functional mismatch (e.g. Figma's icon is a different component than Oxygen's info box).
    fix_action: "Verify with the component author whether Figma `information=true` is the direct visual equivalent of `infoBoxText` + `infoBoxButtonLabel` being set. Document the mapping decision in Label-figma.md."
    blocks: [spec]
    dependency: []

  - id: GAP-018
    dimension: usage
    severity: major
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: "(absent)"
      location: "label-usage.md not found in component-lib/Label/"
      finding: "`figma-extract-usage` hard-stopped because the Figma Desktop Bridge plugin was not running. The `↳ Label examples` page (if it exists) has not been read."
    fix_action: "Desktop Bridge is now connected — run `figma-extract-usage` for Label. If the examples page does not exist, flag as SOURCE_GAP pending designer creation."
    blocks: [docusaurus]
    dependency: []

warnings:
  - id: WARN-001
    dimension: tokens
    note: "tokens.md records `label01` / `labelBold01` as component-specific typography tokens, but these appear to be global theme tokens matched by name search — not tokens scoped to the Label component. Confirm whether the component actually consumes `label01` or a different token."
    confidence: heuristic

  - id: WARN-002
    dimension: figma
    note: "The Figma node `33680:62952` is a documentation showcase frame ('Group 3'), not the component itself. The actual component is `_base_form_label` (22230:37448). Future re-extractions should target 22230:37448 directly for cleaner data."
    confidence: deterministic

  - id: WARN-003
    dimension: examples
    note: "examples.md imports `Input` from `@8x8/oxygen-input` in examples. This import is not declared in props.md. Verify the package name is correct before publishing to Docusaurus."
    confidence: heuristic
---

# Label — Documentation Audit

> **Verdict: NO** — 2 unresolved CONFLICTs block the rewrite phase. Resolve GAP-008 (token conflict) and GAP-017 (Figma `information` vs Oxygen `infoBoxText` mapping) before running `doc-rewrite`.

## File inventory

| File | Status |
|------|--------|
| `props.md` | ✅ Present |
| `examples.md` | ✅ Present |
| `tokens.md` | ✅ Present |
| `accessibility.md` | ✅ Present |
| `Label-figma.md` | ✅ Present |
| `label-usage.md` | ❌ Missing — Desktop Bridge required |
| `label-pui.md` | ✅ Present (NO RELEVANT PUI CONTEXT = PASS) |

## Dimension scores

| Dimension | Score | Coverage |
|-----------|-------|----------|
| props | 0.82 | 12/14 fully sourced |
| examples | 0.65 | 7 examples; none from Storybook |
| tokens | 0.50 | CONFLICT on token identity/size |
| accessibility | 0.82 | Full checklist; all inferred |
| figma | 0.78 | Anatomy + component properties confirmed via Desktop Bridge |
| usage | 0.00 | File missing |
| pui | 1.00 | PASS — no relevant context |

**Overall: 0.65** *(updated 2026-05-01 — GAP-013/014 resolved)*

## Gap counts

| Type | Count |
|------|-------|
| CONFLICTs | **2** |
| Blocker source gaps | 1 (GAP-015) |
| Major source gaps | 1 (GAP-018) — GAP-013 and GAP-014 resolved 2026-05-01 |
| Minor gaps | 12 |
| Warnings | 3 |

## CONFLICTs — must resolve before rewrite

### GAP-008 — Token name and size conflict (tokens × figma) `BLOCKER`

| Source | Token name | Font size | Line height |
|--------|-----------|-----------|-------------|
| MCP (`tokens.md`) | `label01` / `labelBold01` | 0.75rem (12px) | 1rem |
| Figma (`Label-figma.md`) | `typography/body01` / `typography/bodyBold01` | 14px | 20px |

**Decision needed:** Which tokens does `@8x8/oxygen-label` actually apply? Inspect component source.

### GAP-017 — Figma `information` boolean vs Oxygen `infoBoxText` / `infoBoxButtonLabel` `BLOCKER`

Figma uses a single `information: true/false` boolean. Oxygen uses two props (`infoBoxText`, `infoBoxButtonLabel`) plus optional `infoBoxShowOn`. The relationship is unverified.

**Decision needed:** Is Figma's `information` boolean a 1:1 design representation of the Oxygen info box props, or is there a structural mismatch?

## Major source gaps

| ID | Gap | Fix |
|----|-----|-----|
| ~~GAP-013~~ | ~~figma-console Desktop Bridge not connected~~ | ✅ Resolved 2026-05-01 |
| ~~GAP-014~~ | ~~Variables API unavailable~~ | ✅ Resolved — variables are in linked library; CSS var names are valid |
| GAP-015 | `isDisabled` Figma variant missing — disabled visual treatment unknown | Designer must add disabled variant |
| GAP-018 | `label-usage.md` missing | Desktop Bridge now connected — run `figma-extract-usage` |

## Notable minor gaps

- **GAP-001:** `infoBoxShowOn` enum values undocumented (`keyof typeof showOn` is opaque)
- **GAP-002:** `action` type signature (`ActionProps['action']`) not expanded
- **GAP-009:** `error/error01` token (required asterisk color) absent from `tokens.md`
- **GAP-012:** Disabled state color token undocumented

## Warnings

- **WARN-001:** `label01` / `labelBold01` may be global theme tokens, not Label-specific — confirm token usage
- **WARN-002:** Extract targeted showcase frame `33680:62952` rather than the component itself (`22230:37448`) — future re-extractions should use the inner node
- **WARN-003:** Examples import `@8x8/oxygen-input` — verify package name before publishing

## Suggested next actions

1. **Resolve GAP-008:** Check `@8x8/oxygen-label` component source for which typography token it uses. Update `tokens.md` and `Label-figma.md` to agree.
2. **Resolve GAP-017:** Confirm with component author whether Figma `information` maps to `infoBoxText`/`infoBoxButtonLabel`. Document the decision.
3. **Run `figma-extract-usage`** — Desktop Bridge is now connected; run it to fill GAP-018.
4. **Designer action:** Add `isDisabled` Figma variant (GAP-015).
5. Once CONFLICTs are resolved → run `doc-rewrite`.

_Audited: 2026-05-01 · Rubric v1.0_
