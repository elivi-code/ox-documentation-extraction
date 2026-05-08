---
rubric_version: "1.0"
component: Modal
package: "@8x8/oxygen-modal"
audit_date: "2026-05-01"
auditor: doc-audit skill

files_found:
  - props.md
  - examples.md
  - tokens.md
  - accessibility.md
  - Modal-figma.md
  - Modal-pui.md

files_missing:
  - Modal-usage.md

verdict: YES
verdict_rationale: >
  All four core OX files are present and substantive. Modal-figma.md and
  Modal-pui.md are present (PUI confirmed no relevant context via engineer
  relevance check). Modal-usage.md is missing (figma-extract-usage not run)
  — this is a major SOURCE_GAP but not a blocker. Zero CONFLICTs detected.
  Zero blocker-severity gaps. Doc-rewrite can proceed on all available
  dimensions and stub the missing usage section.

scores:
  props_completeness:     0.87
  examples_coverage:      0.75
  token_coverage:         0.70
  accessibility:          0.83
  figma_alignment:        0.72
  usage_guidelines:       0.25
  cross_file_consistency: 0.93
  overall:                0.72

gap_counts:
  doc_gaps: 7
  source_gaps: 6
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
      location: "Modal/"
      finding: >
        Modal-usage.md does not exist. figma-extract-usage was not run.
        The Figma page for Modal contains two component sets (Custom Modal,
        Dialog Modal) — it is unknown whether an Examples page with Do/Don't
        frames exists in the same file. No usage/best-practice/when-to-use
        content has been captured from Figma editorial sources.
    fix_action: >
      Run figma-extract-usage for Modal, targeting the UI-components file
      (5YihJ5WuDvnvrlrRMC4sBp). If no Examples page exists, create
      Modal-usage.md with <!-- NO RELEVANT USAGE CONTENT --> marker.
    blocks:
      - docusaurus usage-guidelines section
      - storybook usage stories
    dependency: []

  - id: GAP-002
    dimension: token_coverage
    severity: major
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: tokens.md
      location: "tokens.md, lines 1–9"
      finding: >
        get-theme-tokens returned 0 results for 'Modal'. All 11 token entries
        in tokens.md were extracted from Figma design-context CSS output, not
        from the Oxygen token registry. Token names use Figma CSS variable
        syntax (--ui/ui06, --text/textcolor01, etc.) which may differ from
        the registry's canonical names or @8x8/oxygen-tokens object paths.
    fix_action: >
      Re-run get-theme-tokens with broader search terms ('ui06', 'shadow01',
      'textcolor', 'action09') to confirm canonical token names. Update
      tokens.md with confirmed registry names.
    blocks:
      - token mapping in doc-rewrite
    dependency: []

  - id: GAP-003
    dimension: figma_alignment
    severity: major
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: Modal-figma.md
      location: "Modal-figma.md, lines 240–242 (Gaps & conflicts)"
      finding: >
        figma_get_variables (format=filtered, namePattern=modal|Modal) and
        figma_get_styles both returned empty results. The Desktop Bridge
        plugin was not active during extraction. Token data in Modal-figma.md
        was derived from inline CSS variable references in the Figma design
        context output — this is a secondary source. The token coverage
        percentage was not returned.
    fix_action: >
      Enable the Figma Desktop Bridge plugin and re-run figma_get_variables
      (resolveAliases=true) and figma_get_styles. Update Modal-figma.md with
      authoritative variable bindings and token coverage %.
    blocks:
      - token coverage verification
      - Modal-figma.md completeness
    dependency: []

  - id: GAP-004
    dimension: figma_alignment
    severity: minor
    type: DOC_GAP
    confidence: heuristic
    auto_fixable: false
    evidence:
      source_file: Modal-figma.md
      location: "Modal-figma.md, Structure and spacing — Widths table"
      finding: >
        The Figma component sets show two breakpoint widths (320px mobile,
        664px desktop) but the code API has three named sizes: 'small',
        'medium', 'big'. No mapping between the code size values and Figma
        widths is documented. It is unknown whether 'small', 'medium', 'big'
        correspond to different pixel values than what Figma shows, or
        whether Figma only illustrates one size preset.
    fix_action: >
      Confirm with the component owner what pixel widths 'small', 'medium',
      and 'big' map to in code. Add a sizes → px table to tokens.md and
      Modal-figma.md. Confirm whether Figma breakpoint widths (320px/664px)
      are the mobile/desktop adaptation of 'medium' or a separate concept.
    blocks:
      - tokens.md size table
    dependency: []

  - id: GAP-005
    dimension: props_completeness
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: props.md
      location: "props.md, lines 110–121 (Additional props)"
      finding: >
        The 'modalProps' prop type is truncated in the MCP response:
        `{ 'aria-labelledby'?: string` — the closing brace is missing,
        suggesting additional fields exist. The full type is unknown from
        the MCP data alone. props.md documents only 'aria-labelledby' as a
        known field.
    fix_action: >
      Inspect the component TypeScript source to obtain the complete
      ModalProps type definition. Update the modalProps row in props.md
      with the full type signature.
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
      source_file: props.md
      location: "props.md, lines 110–121 (Additional props)"
      finding: >
        'initialFocus' appears in get-component-info as a ModalPortal-only
        prop, but get-component-props shows it also available on Modal.
        The props.md documents it under ModalPortal only and lists it again
        in the Additional props table. The discrepancy between the two MCP
        sources is not resolved — the prop may be available on both
        components.
    fix_action: >
      Confirm whether 'initialFocus' is available on Modal (not just
      ModalPortal). If yes, add it to the Modal props table in props.md
      and remove it from the Additional props section.
    blocks: []
    dependency: []

  - id: GAP-007
    dimension: token_coverage
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: tokens.md
      location: "tokens.md, lines 60–65 (Size variants)"
      finding: >
        The size variants table shows only Figma breakpoint widths (664px
        desktop, 320px mobile) and notes "No MCP token data was returned
        for sizes". The 'small', 'medium', 'big' code values are listed
        in the props table but their corresponding pixel dimensions are
        unknown.
    fix_action: >
      Resolve GAP-004 first (confirm size → px mapping). Then update
      tokens.md size variants table with the three size presets and their
      pixel values.
    blocks: []
    dependency: [GAP-004]

  - id: GAP-008
    dimension: token_coverage
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: tokens.md
      location: "tokens.md, lines 70–84 (Spacing)"
      finding: >
        All spacing values (16px padding zones, 12px button gap, 8px icon
        gap, 6px corner radius) are listed as raw pixel values with no token
        column populated. It is not documented whether these are hardcoded
        in the component source or bound to spacing tokens.
    fix_action: >
      Inspect component source or ask the component owner which spacing
      values are hardcoded vs token-bound. Populate a token column in the
      Spacing table in tokens.md, and cross-reference with Modal-figma.md
      Structure and spacing section.
    blocks: []
    dependency: [GAP-002]

  - id: GAP-009
    dimension: token_coverage
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: Modal-figma.md
      location: "Modal-figma.md, Hardcoded values flagged (7)"
      finding: >
        Seven values are flagged as hardcoded in Figma: corner radius (6px),
        dark mode footer divider (#666), scrollbar background (#fafafa),
        scrollbar border (#e8e8e8), scrollbar thumb light (#c1c1c1),
        scrollbar thumb dark (#858585), and scrollbar thumb width (8px).
        It is undocumented whether these are intentionally hardcoded in the
        component source or represent tokenisation debt.
    fix_action: >
      Confirm with design whether these values should be tokenised. If
      intentionally hardcoded, add a comment in Modal-figma.md explaining
      the reasoning. If token candidates exist, add them to tokens.md.
    blocks: []
    dependency: []

  - id: GAP-010
    dimension: accessibility
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: Modal-figma.md
      location: "Modal-figma.md, Gaps & conflicts — No ARIA annotations"
      finding: >
        The Figma design file contains no ARIA role, focus order, or
        keyboard interaction annotations. The ARIA documentation in
        accessibility.md (role="dialog", aria-modal, aria-labelledby,
        aria-describedby) is inferred from the WCAG dialog pattern and
        the prop API (modalProps), not confirmed from the design or the
        component source code.
    fix_action: >
      Designer should add accessibility annotations to the Figma Modal
      component. Engineering should confirm the rendered DOM implements
      role="dialog", aria-modal="true", and aria-labelledby as documented.
    blocks: []
    dependency: []

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
        No example demonstrates a confirmation/danger dialog pattern — the
        most common real-world Modal use case (e.g. "Are you sure you want
        to delete?"). The Dialog Modal Figma variant is specifically designed
        for this pattern but no corresponding code example is documented.
    fix_action: >
      Add a "Confirmation dialog" example to examples.md using Modal +
      ModalHeader (title: "Delete item?") + ModalContent (description text)
      + ModalFooter with Cancel and Confirm (danger) buttons.
    blocks: []
    dependency: []

  - id: GAP-012
    dimension: examples_coverage
    severity: minor
    type: DOC_GAP
    confidence: heuristic
    auto_fixable: true
    evidence:
      source_file: examples.md
      location: "examples.md — all examples"
      finding: >
        No example demonstrates aria-describedby wiring, even though
        accessibility.md explicitly recommends using it to point to
        ModalContent when it contains instructions. The existing aria
        example only shows aria-labelledby.
    fix_action: >
      Add an accessibility example to examples.md showing both
      aria-labelledby (via titleProps.id) and aria-describedby (via
      ModalContent id) wired together on the Modal.
    blocks: []
    dependency: []

  - id: GAP-013
    dimension: figma_alignment
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: Modal-figma.md
      location: "Modal-figma.md, Gaps & conflicts — Token coverage %"
      finding: >
        Token coverage percentage was not returned by the enriched
        figma_get_component call (REST API fallback used; Desktop Bridge
        plugin not active). The coverage assessment in Modal-figma.md
        is based on manual inspection rather than the Figma API metric.
    fix_action: >
      Run figma_get_component with enrich=true via Desktop Bridge.
      Update Modal-figma.md with the authoritative token coverage %.
    blocks: []
    dependency: [GAP-003]

warnings:
  - id: WARN-001
    dimension: examples_coverage
    confidence: heuristic
    finding: >
      The MCP returned only 1 Storybook example (the documentation wrapper
      story), which is not a clean usage snippet. All 8 examples in
      examples.md are derived from the prop definitions and the Storybook
      story structure — they have not been run against the component.
      The 'useModalState' hook import path and API are assumed from the
      story pattern but not confirmed from the package's public exports.
    recommendation: >
      Validate examples against the Storybook or a local dev environment
      before publishing. Specifically verify that 'useModalState' is a
      public export of '@8x8/oxygen-modal'.

  - id: WARN-002
    dimension: accessibility
    confidence: heuristic
    finding: >
      accessibility.md documents role="dialog" and aria-modal="true" as
      the correct rendered markup. This is based on the WCAG dialog pattern
      and the presence of the 'modalProps' pass-through prop — it has not
      been confirmed by inspecting the component's rendered DOM or source.
      The component may use a different element type or ARIA implementation.
    recommendation: >
      Inspect the rendered DOM of the Modal in a browser or check the
      component source to confirm role="dialog" and aria-modal="true"
      are set on the dialog container element.

  - id: WARN-003
    dimension: token_coverage
    confidence: heuristic
    finding: >
      All token names in tokens.md use Figma CSS variable syntax
      (--ui/ui06, --text/textcolor01, --actions/action09, etc.) derived
      from the design-context output. These may differ from the Oxygen
      token registry's canonical names or the @8x8/oxygen-tokens JavaScript
      paths used in production.
    recommendation: >
      Cross-reference token names against @8x8/oxygen-tokens or the
      published Oxygen token registry before using in implementation.
      Resolve GAP-002 to obtain authoritative names.

  - id: WARN-004
    dimension: props_completeness
    confidence: heuristic
    finding: >
      ModalFooter and ModalContent have "No documented props beyond
      standard HTML attributes" in props.md. This accurately reflects
      what the MCP returned (0 props for both). However, these components
      likely accept className, style, and forwarded HTML attributes —
      the absence of documented props may mislead consumers into thinking
      these components cannot be customised.
    recommendation: >
      Add a note to the ModalFooter and ModalContent sections confirming
      they accept standard React HTML attributes (className, style, etc.)
      as a pass-through.
# --- navigation (added by component-map) ---
role: audit
pipeline_stage: spec_ready
pipeline_note: "Audit verdict YES/PARTIAL — doc-rewrite can run"
siblings:
  - "[[Modal/props]]"
  - "[[Modal/examples]]"
  - "[[Modal/tokens]]"
  - "[[Modal/accessibility]]"
  - "[[Modal/Modal-figma]]"
  - "[[Modal/Modal-pui]]"
tags:
  - oxygen
  - component/Modal
  - role/audit
  - stage/spec_ready
---

# Modal — Audit Report

> **Verdict: YES — ready for doc-rewrite**
>
> All 4 core source files are present and substantive. Modal-pui.md is
> present (engineer confirmed no relevant PUI context). No CONFLICTs.
> No blocker-severity gaps. One major SOURCE_GAP (Modal-usage.md missing)
> and two major SOURCE_GAPs (MCP tokens empty, Desktop Bridge offline) —
> none are blockers. Doc-rewrite can proceed on all available dimensions.

**Audit date:** 2026-05-01 | **Rubric version:** 1.0

---

## File inventory

| File | Status | Lines | Produced by |
|------|--------|-------|-------------|
| `props.md` | ✅ Present | 123 | oxygen-mcp-extract |
| `examples.md` | ✅ Present | 235 | oxygen-mcp-extract |
| `tokens.md` | ✅ Present | 103 | oxygen-mcp-extract |
| `accessibility.md` | ✅ Present | 147 | oxygen-mcp-extract |
| `Modal-figma.md` | ✅ Present | 245 | figma-extract |
| `Modal-pui.md` | ✅ Present (no context) | 23 | pui-mcp-extract |
| `Modal-usage.md` | ❌ Missing | — | figma-extract-usage |

---

## Dimension scores

| Dimension | Score | Coverage | Status |
|-----------|-------|----------|--------|
| Props completeness | 0.87 | 13/15 checks | ⚠️ Minor gaps |
| Examples coverage | 0.75 | 8/11 scenarios | ⚠️ Minor gaps |
| Token coverage | 0.70 | 8/12 checks | ⚠️ Source gap (MCP returned 0) |
| Accessibility | 0.83 | 9/11 checks | ⚠️ Inferred, not confirmed from source |
| Figma alignment | 0.72 | 7/10 checks | ⚠️ Variables empty; size→px mapping missing |
| Usage guidelines | 0.25 | 0/2 files | ❌ Major source gap |
| Cross-file consistency | 0.93 | 19/20 checks | ✅ Strong |
| **Overall** | **0.72** | | |

---

## Gaps

### Blockers
_None._

### Major gaps

| ID | Type | Dimension | Finding |
|----|------|-----------|---------|
| GAP-001 | SOURCE_GAP | Usage guidelines | `Modal-usage.md` missing — figma-extract-usage not run |
| GAP-002 | SOURCE_GAP | Token coverage | MCP returned 0 tokens; all token data from Figma context output only |
| GAP-003 | SOURCE_GAP | Figma alignment | `figma_get_variables` + `figma_get_styles` empty; Desktop Bridge offline during extraction |

### Minor gaps

| ID | Type | Dimension | Finding |
|----|------|-----------|---------|
| GAP-004 | DOC_GAP | Figma alignment | `size` prop values (`small`/`medium`/`big`) have no px mapping in Figma; breakpoint widths (320px/664px) not mapped to size presets |
| GAP-005 | SOURCE_GAP | Props completeness | `modalProps` type truncated in MCP — full type signature unknown |
| GAP-006 | DOC_GAP | Props completeness | `initialFocus` discrepancy — MCP sources disagree on whether it's Modal-only or ModalPortal-only |
| GAP-007 | DOC_GAP | Token coverage | `size` variants table incomplete — `small`/`medium`/`big` → px values unknown |
| GAP-008 | DOC_GAP | Token coverage | Spacing values (16px, 12px, 8px, 6px) not mapped to tokens |
| GAP-009 | DOC_GAP | Token coverage | 7 hardcoded Figma values (scrollbar colors, divider, radius) — intent not confirmed |
| GAP-010 | SOURCE_GAP | Accessibility | No ARIA annotations in Figma; a11y guidance inferred from WCAG APG, not confirmed from source |
| GAP-011 | DOC_GAP | Examples coverage | No confirmation/danger dialog example (Dialog Modal variant not illustrated in code) |
| GAP-012 | DOC_GAP | Examples coverage | No `aria-describedby` example (recommended in accessibility.md but absent from examples) |
| GAP-013 | SOURCE_GAP | Figma alignment | Token coverage % unavailable — Desktop Bridge required |

---

## Conflicts
_None identified._

---

## Warnings (heuristic — advisory only)

| ID | Dimension | Finding |
|----|-----------|---------|
| WARN-001 | Examples | All examples derived from prop API + 1 Storybook story — `useModalState` export path unverified |
| WARN-002 | Accessibility | `role="dialog"` and `aria-modal="true"` inferred from WCAG pattern, not confirmed from rendered DOM |
| WARN-003 | Token coverage | Token names from Figma CSS variable syntax — may differ from `@8x8/oxygen-tokens` canonical paths |
| WARN-004 | Props completeness | ModalFooter/ModalContent "no props" note may mislead — standard HTML attributes not explicitly listed |

---

## What doc-rewrite can fix automatically

| Gap | Auto-fixable |
|-----|:---:|
| GAP-006 — clarify `initialFocus` availability on Modal vs ModalPortal | ✅ |
| GAP-011 — add confirmation dialog example to examples.md | ✅ |
| GAP-012 — add `aria-describedby` wiring example to examples.md | ✅ |
| WARN-004 — add HTML attributes pass-through note to ModalFooter/ModalContent | ✅ |

## What requires human input before doc-rewrite

| Gap | Required action |
|-----|----------------|
| GAP-001 | Run figma-extract-usage for Modal |
| GAP-002 | Confirm token canonical names against OX token registry |
| GAP-003 | Enable Desktop Bridge and re-run figma_get_variables / figma_get_styles |
| GAP-004 | Component owner confirms size → px mapping for `small`/`medium`/`big` |
| GAP-005 | Inspect TS source for full `modalProps` type definition |
| GAP-007 | Resolve GAP-004 first, then populate size table in tokens.md |
| GAP-008 | Component owner confirms spacing token bindings vs hardcoded |
| GAP-009 | Design confirms scrollbar/divider/radius hardcoded intent or token candidates |
| GAP-010 | Designer adds ARIA annotations to Figma; engineering confirms DOM implementation |
| GAP-013 | Enable Desktop Bridge for authoritative token coverage % |

---

## Suggested next action

```
/doc-rewrite Modal
```

The rewrite can address the 4 auto-fixable gaps and stub the missing
usage section with an explicit placeholder. GAP-004 (size→px mapping)
is the most impactful human-input gap — resolving it unblocks the tokens
and figma-alignment dimensions.

---

_Audit produced by doc-audit skill · Rubric version 1.0 · 2026-05-01_
