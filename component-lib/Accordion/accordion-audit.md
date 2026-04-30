---
rubric_version: "1.0"
component: Accordion
package: "@8x8/oxygen-accordion"
audit_date: "2026-04-28"
auditor: doc-audit skill

files_found:
  - props.md
  - examples.md
  - tokens.md
  - accessibility.md
  - accordion-figma.md

files_missing:
  - accordion-usage.md
  - accordion-pui.md

verdict: YES
verdict_rationale: >
  All four core files are present and substantive. No deterministic CONFLICTs
  identified. Two major SOURCE_GAPs exist (accordion-usage.md, accordion-pui.md)
  but neither is a blocker per rubric rules — the rewrite can proceed on available
  dimensions while flagging usage-guideline and PUI sections for later fill-in.

scores:
  props_completeness:   0.88
  examples_coverage:    0.72
  token_coverage:       0.75
  accessibility:        0.80
  figma_alignment:      0.74
  usage_guidelines:     0.30
  cross_file_consistency: 0.95
  overall:              0.73

gap_counts:
  doc_gaps: 9
  source_gaps: 7
  conflicts: 0
  warnings: 4

gaps:
  - id: GAP-001
    dimension: usage_guidelines
    severity: major
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: "(absent)"
      location: "Accordion/"
      finding: >
        accordion-usage.md does not exist. figma-extract-usage was attempted but
        halted: Desktop Bridge not running AND the examples page (79430:614) contains
        no frames prefixed with '✅ Do' or '❌ Don't'. Usage content (best-practices,
        when-to-use, when-not-to-use) is partially captured in accordion-figma.md
        from the Oxygen MCP usage field, but no paired Do/Don't visual examples exist.
    fix_action: >
      Designer must add Do/Don't frames to the '↳ Accordion examples' Figma page
      following the figma-draw template convention, then re-run figma-extract-usage.
    blocks:
      - docusaurus usage-guidelines section
      - storybook usage stories
    dependency: []

  - id: GAP-002
    dimension: usage_guidelines
    severity: major
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: "(absent)"
      location: "Accordion/"
      finding: >
        accordion-pui.md does not exist. pui-mcp-extract was not run for this
        component. It is unknown whether Platform UI exposes an Accordion or a
        related wrapper component.
    fix_action: >
      Run the pui-mcp-extract skill for 'Accordion'. If PUI has no equivalent,
      create the file with <!-- NO RELEVANT PUI CONTEXT --> marker.
    blocks:
      - docusaurus PUI integration section
    dependency: []

  - id: GAP-003
    dimension: token_coverage
    severity: major
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: tokens.md
      location: "tokens.md, line 7–9"
      finding: >
        The Oxygen MCP returned 0 theme tokens for the 'accordion' package.
        All token data in tokens.md was sourced from manual Figma design-context
        inspection, not from the authoritative token registry. Token names may
        differ from published names, and any tokens added after the Figma
        extraction date would be missed.
    fix_action: >
      Re-run get-theme-tokens with broader search terms (e.g. 'ui06', 'textcolor',
      'interactive') to confirm token canonical names. Update tokens.md with
      confirmed registry names.
    blocks:
      - token mapping in doc-rewrite
    dependency: []

  - id: GAP-004
    dimension: figma_alignment
    severity: major
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: accordion-figma.md
      location: "accordion-figma.md, lines 77–81 (_header boolean toggles)"
      finding: >
        The Figma '_header' atom has an 'AIBadge?' boolean toggle (default: false)
        that shows a star icon + "AI" label next to the accordion title. No
        corresponding code prop ('aiBadge', 'AIBadge', or similar) exists in
        props.md. It is undocumented whether this feature is: (a) rendered via
        the generic 'contentAfterTitle' slot, (b) a future/unreleased code feature,
        or (c) a Figma-only design preview element.
    fix_action: >
      Confirm with the component owner whether AIBadge is achievable via
      contentAfterTitle. If yes, add an example to examples.md. If it is a
      planned code prop not yet released, note it as 'coming soon' in props.md.
    blocks:
      - props.md completeness
      - examples.md coverage
    dependency: []

  - id: GAP-005
    dimension: figma_alignment
    severity: minor
    type: DOC_GAP
    confidence: heuristic
    auto_fixable: true
    evidence:
      source_file: accordion-figma.md
      location: "accordion-figma.md, lines 62–65 (Accordion boolean toggles)"
      finding: >
        The Figma 'Accordion' component set has a 'divider?' boolean toggle
        (default: true). No corresponding code prop exists in props.md. It is
        not documented whether the divider is always shown in production, always
        hidden, or configurable via CSS only.
    fix_action: >
      Add a note in accordion-figma.md 'Gaps & conflicts' section and props.md
      explaining that the divider is a Figma-only design toggle (always rendered
      in code) OR document a CSS override pattern if applicable.
    blocks: []
    dependency: []

  - id: GAP-006
    dimension: figma_alignment
    severity: minor
    type: DOC_GAP
    confidence: heuristic
    auto_fixable: true
    evidence:
      source_file: accordion-figma.md
      location: "accordion-figma.md, lines 62–65 (Accordion boolean toggles)"
      finding: >
        The Figma 'Accordion' component set has a 'scrollbar?' boolean toggle
        (default: false). No corresponding code prop exists in props.md. The
        docs do not explain how scrolling behaviour is controlled in code (it
        may be automatic when 'isContentScrollable=true' or triggered by
        'forcedHeight').
    fix_action: >
      Clarify in props.md whether scrollbar visibility is automatic when
      isContentScrollable=true, or document that it is Figma-only. Cross-reference
      with isContentScrollable and forcedHeight props.
    blocks: []
    dependency: []

  - id: GAP-007
    dimension: token_coverage
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: accordion-figma.md
      location: "accordion-figma.md, lines 159–184 (Structure & spacing)"
      finding: >
        All spacing values in the Structure & spacing section are listed as raw
        pixel values (16px padding, 12px gap, 4px gap, 48px header height, 20px
        icon size) with no token column populated. It is not documented whether
        these values are hardcoded in the component or bound to spacing tokens.
    fix_action: >
      Inspect component source or ask component owner which spacing values are
      hardcoded vs token-bound. Populate the Token column in the Structure &
      spacing tables in accordion-figma.md and tokens.md.
    blocks:
      - tokens.md completeness
    dependency: [GAP-003]

  - id: GAP-008
    dimension: token_coverage
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: accordion-figma.md
      location: "accordion-figma.md, lines 305–309 (Gaps & conflicts)"
      finding: >
        The Figma Scrollbar_Mac OS component uses a hardcoded #858585 value for
        the scrollbar thumb color in dark mode. No token binding was detected.
        This is flagged in the figma.md gaps section but not resolved.
    fix_action: >
      Confirm with design whether #858585 (dark scrollbar thumb) should be
      bound to a token. If intentionally hardcoded, note the reason. If a token
      exists, add it to tokens.md.
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
        All 8 examples use mode="light" (default). No dark mode example is
        provided. The component has a 'mode' Figma variant (light/dark) but no
        corresponding code prop — however, showing the dark rendering would help
        consumers understand theming expectations.
    fix_action: >
      Add a note in examples.md explaining that dark mode is controlled via CSS
      variables / theming, not a component prop. Link to the Oxygen theming docs.
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
        No example shows the disabled state. The Figma '_header' atom has a
        'state=disabled' variant. If 'disabled' is achievable via a prop or
        attribute, it should be documented.
    fix_action: >
      Confirm whether a 'disabled' prop exists (possibly passed via HTML
      attributes to the button element). Add a disabled example to examples.md.
    blocks: []
    dependency: [GAP-004]

  - id: GAP-011
    dimension: examples_coverage
    severity: minor
    type: DOC_GAP
    confidence: heuristic
    auto_fixable: true
    evidence:
      source_file: examples.md
      location: "examples.md — all examples"
      finding: >
        No example demonstrates 'forcedHeight'. This prop is distinct from
        AccordionGroup.hasFixedHeight but examples.md groups fixed-height
        behaviour only under AccordionGroup. A standalone Accordion with
        forcedHeight would clarify the difference.
    fix_action: >
      Add a forcedHeight example to examples.md showing a single Accordion
      with a pixel height constraint and isContentScrollable=true.
    blocks: []
    dependency: []

  - id: GAP-012
    dimension: accessibility
    severity: minor
    type: SOURCE_GAP
    confidence: heuristic
    auto_fixable: false
    evidence:
      source_file: accessibility.md
      location: "accessibility.md, line 104"
      finding: >
        The WCAG 4.1.2 row notes: 'default label values not confirmed from MCP
        data'. The default values for the 'translations' prop (expand/collapse
        aria-labels) are unknown — the MCP did not return them and they are not
        documented in props.md.
    fix_action: >
      Check component source code or Storybook for default translation strings.
      Add the default values to the 'Translations' type table in props.md and
      confirm whether they are localised or English-only by default.
    blocks:
      - accessibility.md completeness
    dependency: []

  - id: GAP-013
    dimension: accessibility
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: accordion-figma.md
      location: "accordion-figma.md, lines 290–293"
      finding: >
        The Figma file contains no ARIA role, focus order, or keyboard
        interaction annotations on the Accordion component. Accessibility
        guidance in accessibility.md is inferred from WAI-ARIA APG 1.2, not
        confirmed from the design or component source.
    fix_action: >
      Designer should add accessibility annotations to the Figma component.
      Engineering should confirm that the component implements aria-expanded,
      role="region", and aria-labelledby as documented.
    blocks: []
    dependency: []

  - id: GAP-014
    dimension: figma_alignment
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: accordion-figma.md
      location: "accordion-figma.md, lines 221–225 (Component variants table)"
      finding: >
        '_headerCustom' (node 82572:13829) was not separately extracted. The
        figma.md notes it mirrors '_header' with an additional icon button slot,
        but its component properties were not inspected and are not listed.
    fix_action: >
      Run figma_get_component on node 82572:13829 and add its properties to
      accordion-figma.md. Specifically confirm whether the 'contentAfterTitle'
      slot maps to this Figma atom.
    blocks: []
    dependency: []

  - id: GAP-015
    dimension: token_coverage
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: accordion-figma.md
      location: "accordion-figma.md, lines 109–117 (Token coverage)"
      finding: >
        figma_get_component with enrich=true did not return token coverage
        percentage data (REST API limitation without Desktop Bridge). Coverage
        was manually assessed as 'all values tokenised' but this cannot be
        verified programmatically.
    fix_action: >
      Run figma_get_component with enrich=true via Desktop Bridge to obtain
      authoritative token coverage %. Update token coverage section in
      accordion-figma.md.
    blocks: []
    dependency: []

  - id: GAP-016
    dimension: accessibility
    severity: minor
    type: DOC_GAP
    confidence: heuristic
    auto_fixable: true
    evidence:
      source_file: accessibility.md
      location: "accessibility.md, lines 14–23 (ARIA roles table)"
      finding: >
        The ARIA roles table documents aria-labelledby on the content panel
        but does not document aria-controls on the header button. WAI-ARIA
        APG Accordion pattern recommends aria-controls pointing to the panel ID.
        It is unknown whether the component implements this.
    fix_action: >
      Confirm whether the component sets aria-controls on the header button.
      If yes, add a row to the ARIA roles table. If no, note the deviation
      from APG and whether it is intentional.
    blocks: []
    dependency: []

warnings:
  - id: WARN-001
    dimension: examples_coverage
    confidence: heuristic
    finding: >
      All 8 examples in examples.md are derived/inferred — the MCP returned
      0 clean Storybook examples. The examples are plausible based on prop
      definitions but have not been verified against a running component.
      They may contain import paths that don't exist (e.g. '@8x8/oxygen-icons'
      VideoIcon, '@8x8/oxygen-icon-button' IconButton).
    recommendation: >
      Validate examples against the actual Storybook before publishing to
      Docusaurus. Consider running the component in isolation to confirm
      import paths.

  - id: WARN-002
    dimension: accessibility
    confidence: heuristic
    finding: >
      accessibility.md states the header "is rendered as a native button
      element" and that aria-expanded is set. This is inferred from WAI-ARIA
      best practice, not confirmed from component source. The component may
      use a div with role="button" or a custom implementation.
    recommendation: >
      Inspect component source or rendered DOM to confirm the element type
      and ARIA attribute implementation before publishing.

  - id: WARN-003
    dimension: figma_alignment
    confidence: heuristic
    finding: >
      Figma 'isOpen?' maps to code 'isExpanded'. The naming difference is
      expected (Figma property names rarely match code prop names exactly)
      but is not explicitly called out in the docs. This could confuse
      contributors cross-referencing Figma and code.
    recommendation: >
      Add a mapping note in accordion-figma.md: "Figma 'isOpen?' corresponds
      to code prop 'isExpanded'."

  - id: WARN-004
    dimension: token_coverage
    confidence: heuristic
    finding: >
      tokens.md is sourced entirely from Figma inspection rather than the
      Oxygen token registry. Token names use Figma CSS variable syntax
      (--ui/ui06, --text/textcolor01) which may differ from the registry's
      canonical names or JavaScript token object paths.
    recommendation: >
      Cross-reference token names against the Oxygen token registry or the
      published @8x8/oxygen-tokens package before using in implementation.
---

# Accordion — Audit Report

> **Verdict: YES — ready for doc-rewrite**
>
> All 4 core source files are present and substantive. No deterministic conflicts.
> Two major SOURCE_GAPs exist (accordion-usage.md, accordion-pui.md) but these
> are not blockers — doc-rewrite can proceed on available dimensions and stub
> the missing sections.

**Audit date:** 2026-04-28 | **Rubric version:** 1.0

---

## File inventory

| File | Status | Lines | Produced by |
|------|--------|-------|-------------|
| `props.md` | ✅ Present | 82 | oxygen-mcp-extract |
| `examples.md` | ✅ Present | 184 | oxygen-mcp-extract |
| `tokens.md` | ✅ Present | 95 | oxygen-mcp-extract |
| `accessibility.md` | ✅ Present | 109 | oxygen-mcp-extract |
| `accordion-figma.md` | ✅ Present | 314 | figma-extract |
| `accordion-usage.md` | ❌ Missing | — | figma-extract-usage |
| `accordion-pui.md` | ❌ Missing | — | pui-mcp-extract |

---

## Dimension scores

| Dimension | Score | Coverage | Status |
|-----------|-------|----------|--------|
| Props completeness | 0.88 | 14/16 checks | ⚠️ Minor gaps |
| Examples coverage | 0.72 | 8/11 scenarios | ⚠️ Minor gaps |
| Token coverage | 0.75 | 9/12 checks | ⚠️ Source gap (MCP returned 0) |
| Accessibility | 0.80 | 8/10 checks | ⚠️ Inferred, not confirmed |
| Figma alignment | 0.74 | 7/9 checks | ⚠️ 3 Figma props unresolved in code |
| Usage guidelines | 0.30 | 0/2 files | ❌ Major source gap |
| Cross-file consistency | 0.95 | 19/20 checks | ✅ Strong |
| **Overall** | **0.73** | | |

---

## Gaps

### Blockers
_None._

### Major gaps

| ID | Type | Dimension | Finding |
|----|------|-----------|---------|
| GAP-001 | SOURCE_GAP | Usage guidelines | `accordion-usage.md` missing — no Do/Don't frames in Figma; Desktop Bridge offline |
| GAP-002 | SOURCE_GAP | Usage guidelines | `accordion-pui.md` missing — pui-mcp-extract not run |
| GAP-003 | SOURCE_GAP | Token coverage | MCP returned 0 tokens; all token data from Figma inspection only |
| GAP-004 | DOC_GAP | Figma alignment | `AIBadge?` Figma toggle has no documented code prop equivalent |

### Minor gaps

| ID | Type | Dimension | Finding |
|----|------|-----------|---------|
| GAP-005 | DOC_GAP | Figma alignment | `divider?` Figma toggle — no documented code mapping or "always shown" explanation |
| GAP-006 | DOC_GAP | Figma alignment | `scrollbar?` Figma toggle — no documented code mapping |
| GAP-007 | DOC_GAP | Token coverage | Spacing values (16px, 12px, 48px, 20px) not mapped to tokens |
| GAP-008 | DOC_GAP | Token coverage | Scrollbar thumb `#858585` (dark) hardcoded — no token detected |
| GAP-009 | DOC_GAP | Examples coverage | No dark mode example or theming guidance |
| GAP-010 | DOC_GAP | Examples coverage | No disabled state example |
| GAP-011 | DOC_GAP | Examples coverage | No `forcedHeight` standalone example (different from `hasFixedHeight`) |
| GAP-012 | SOURCE_GAP | Accessibility | Default `translations` values not confirmed from MCP or source |
| GAP-013 | SOURCE_GAP | Accessibility | No ARIA annotations in Figma file |
| GAP-014 | SOURCE_GAP | Figma alignment | `_headerCustom` (82572:13829) properties not extracted |
| GAP-015 | SOURCE_GAP | Token coverage | Token coverage % unavailable (Desktop Bridge required) |
| GAP-016 | DOC_GAP | Accessibility | `aria-controls` relationship not documented (WAI-ARIA APG recommends it) |

---

## Conflicts
_None identified._

---

## Warnings (heuristic — advisory only)

| ID | Dimension | Finding |
|----|-----------|---------|
| WARN-001 | Examples | All examples derived/inferred — 0 Storybook examples from MCP; import paths unverified |
| WARN-002 | Accessibility | ARIA implementation (button element, aria-expanded) inferred from APG, not confirmed from source |
| WARN-003 | Figma alignment | `isOpen?` (Figma) → `isExpanded` (code) naming difference not called out in docs |
| WARN-004 | Token coverage | Token names sourced from Figma CSS variable syntax — may differ from registry canonical names |

---

## What doc-rewrite can fix automatically

| Gap | Auto-fixable |
|-----|:---:|
| GAP-005 — add divider? explanation to props.md | ✅ |
| GAP-006 — add scrollbar? / isContentScrollable clarification | ✅ |
| GAP-009 — add dark mode / theming note to examples.md | ✅ |
| GAP-011 — add forcedHeight example | ✅ |
| GAP-016 — add aria-controls note to accessibility.md | ✅ |
| WARN-003 — add isOpen? → isExpanded mapping note in accordion-figma.md | ✅ |

## What requires human input before doc-rewrite

| Gap | Required action |
|-----|----------------|
| GAP-001 | Designer adds Do/Don't frames to Figma |
| GAP-002 | Run pui-mcp-extract |
| GAP-003 | Confirm token canonical names against registry |
| GAP-004 | Component owner confirms AIBadge code behaviour |
| GAP-007 | Component owner confirms spacing token bindings |
| GAP-008 | Design confirms scrollbar thumb token or hardcoded intent |
| GAP-010 | Confirm disabled prop/attribute existence |
| GAP-012 | Check component source for default translations |
| GAP-013 | Designer adds ARIA annotations to Figma |
| GAP-014 | Run figma_get_component on 82572:13829 |
| GAP-015 | Run Desktop Bridge for token coverage % |

---

## Suggested next action

```
/doc-rewrite Accordion
```

The rewrite can address all 6 auto-fixable gaps and stub the 2 missing
source files with explicit placeholders. Resolve human-input gaps in parallel
(GAP-004 is the most impactful — clarifying AIBadge unlocks props.md and
examples.md completeness).

---

_Audit produced by doc-audit skill · Rubric version 1.0 · 2026-04-28_
