---
rubric_version: "1.0"
component: Modal
package: "@8x8/oxygen-modal"
audit_date: "2026-05-13"
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

notes:
  - >
    Modal-usage-draft.md is present (created 2026-05-13 by usage-advisor skill)
    with 7 approved Do/Don't pairs. This is an intermediate artifact, not the
    canonical figma-extract-usage output. GAP-001 (Modal-usage.md missing) is
    downgraded to reflect draft progress — see updated fix_action.

verdict: "YES"
verdict_rationale: >
  All four core OX files are present and substantive. Modal-figma.md and
  Modal-pui.md are present (PUI confirmed no relevant context via engineer
  relevance check). Modal-usage.md is missing but a usage-advisor draft with
  7 approved Do/Don't pairs exists (Modal-usage-draft.md). Zero CONFLICTs
  detected. Zero blocker-severity gaps. Doc-rewrite can proceed on all available
  dimensions and stub the missing usage section with the draft as input.

scores:
  props_completeness:     0.87
  examples_coverage:      0.75
  token_coverage:         0.70
  accessibility:          0.83
  figma_alignment:        0.72
  usage_guidelines:       0.40
  cross_file_consistency: 0.93
  overall:                0.74

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
        Modal-usage.md does not exist — figma-extract-usage has not been run.
        A usage-advisor draft (Modal-usage-draft.md) was produced on 2026-05-13
        with 7 approved Do/Don't pairs, all grounded in props.md, accessibility.md,
        Modal-figma.md, and internal precedent from AlertBanner and Button.
        The draft is ready to use as doc-rewrite input or to seed a Figma
        examples page so figma-extract-usage can run.
    fix_action: >
      Option A — Figma path (canonical): Push the 7 pairs from Modal-usage-draft.md
      into Figma via figma-draw to create the '↳ Modal examples' page. Drop in
      real Modal component instances, finalise wording, then run figma-extract-usage
      to produce the canonical Modal-usage.md.
      Option B — Direct path: Reference Modal-usage-draft.md in doc-rewrite as
      the usage-guidelines source. The spec will note this as a draft until a
      Figma-extracted canonical file replaces it.
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
      location: "tokens.md, lines 29–33"
      finding: >
        get-theme-tokens returned 0 results for 'Modal'. All token entries in
        tokens.md were extracted from Figma design-context CSS output, not from
        the Oxygen token registry. Token names use Figma CSS variable syntax
        (--ui/ui06, --text/textcolor01, etc.) which may differ from the
        registry's canonical names or @8x8/oxygen-tokens object paths.
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
      location: "Modal-figma.md, lines 260–266 (Gaps & conflicts)"
      finding: >
        figma_get_variables and figma_get_styles both returned empty results —
        the Desktop Bridge plugin was not active during extraction. Token data
        in Modal-figma.md was derived from inline CSS variable references in
        the Figma design context output (secondary source only). Token coverage
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
      location: "Modal-figma.md, Structure and spacing — Widths table (lines 197–200)"
      finding: >
        The Figma component sets show two breakpoint widths (320px mobile,
        664px desktop) but the code API has three named sizes: 'small',
        'medium', 'big'. No mapping between the code size values and Figma
        widths is documented. It is unknown whether 'small', 'medium', 'big'
        correspond to different pixel values than what Figma shows, or whether
        Figma only illustrates one size preset.
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
      location: "props.md, lines 148–153 (Additional props)"
      finding: >
        The 'modalProps' prop type is documented as `{ 'aria-labelledby'?: string }`
        — derived from the MCP response which truncated the type definition.
        The closing brace of the type object is absent in the source, suggesting
        additional fields may exist beyond aria-labelledby.
    fix_action: >
      Inspect the component TypeScript source to obtain the complete ModalProps
      type definition. Update the modalProps row in props.md with the full
      type signature.
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
      location: "props.md, lines 107 and 149"
      finding: >
        'initialFocus' appears in both the ModalPortal props table (line 107)
        and the Additional props table (line 149). The Additional props note
        says it is "Available on Modal (in addition to ModalPortal)" —
        contradicting the earlier ModalPortal-only placement. The discrepancy
        between the two MCP sources is not resolved.
    fix_action: >
      Confirm whether 'initialFocus' is available on Modal (not just
      ModalPortal). If yes, add it to the Modal props table and remove the
      duplicate from the Additional props section.
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
      location: "tokens.md, lines 83–90 (Size variants)"
      finding: >
        The size variants table shows only Figma breakpoint widths (664px
        desktop, 320px mobile) and notes "No MCP token data was returned for
        sizes". The 'small', 'medium', 'big' code values from props.md are not
        mapped to pixel dimensions.
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
      location: "tokens.md, lines 96–108 (Spacing)"
      finding: >
        All spacing values (16px padding zones, 12px button gap, 8px icon gap,
        6px corner radius) are listed as raw pixel values with no token column.
        It is not documented whether these are hardcoded in the component source
        or bound to spacing tokens.
    fix_action: >
      Inspect component source or ask the component owner which spacing values
      are hardcoded vs token-bound. Populate a token column in the Spacing
      table in tokens.md.
    blocks: []
    dependency: [GAP-002]

  - id: GAP-009
    dimension: token_coverage
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: tokens.md
      location: "tokens.md, lines 112–124 (Hardcoded values flagged)"
      finding: >
        Six values are flagged as hardcoded in Figma: corner radius (6px),
        dark mode footer divider (#666), scrollbar background (#fafafa),
        scrollbar border (#e8e8e8), scrollbar thumb light (#c1c1c1), scrollbar
        thumb dark (#858585). It is undocumented whether these are intentionally
        hardcoded in the component source or represent tokenisation debt.
    fix_action: >
      Confirm with design whether these values should be tokenised. If
      intentionally hardcoded, add a reasoning note in Modal-figma.md.
      If token candidates exist, add them to tokens.md.
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
      location: "Modal-figma.md, Gaps & conflicts — No ARIA annotations (line 260)"
      finding: >
        The Figma design file contains no ARIA role, focus order, or keyboard
        interaction annotations. The ARIA documentation in accessibility.md
        (role="dialog", aria-modal, aria-labelledby, aria-describedby) is
        inferred from the WCAG dialog pattern and the prop API (modalProps),
        not confirmed from the design file or the component source code.
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
        No example demonstrates a confirmation/danger dialog pattern — the most
        common real-world Modal use case. The Dialog Modal Figma variant is
        specifically designed for this (Modal-figma.md:74-80) but no corresponding
        code example exists. examples.md has 8 examples covering open/close,
        sizes, close behaviour, portal, headless variant, and ModalHeader — but
        not the destructive confirmation pattern.
    fix_action: >
      Add a "Confirmation dialog" example to examples.md using Modal +
      ModalHeader (title: "Delete item?") + ModalContent (description text) +
      ModalFooter with Cancel and Delete (isDestructive) buttons. Wire
      focusAfterCloseItemRef and set initial focus on Cancel.
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
      location: "examples.md — ModalHeader variants section (lines 234–242)"
      finding: >
        The existing aria example demonstrates aria-labelledby wiring (via
        titleProps.id and modalProps) but aria-describedby is absent.
        accessibility.md explicitly recommends using aria-describedby to
        point to ModalContent when it contains instructions (line 151).
    fix_action: >
      Extend the accessibility example in examples.md to show both
      aria-labelledby (via titleProps.id) and aria-describedby (via a
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
      location: "Modal-figma.md, Gaps & conflicts — Token coverage % (line 265)"
      finding: >
        Token coverage percentage was not returned by the enriched
        figma_get_component call (REST API fallback used; Desktop Bridge
        plugin not active). Coverage assessment in Modal-figma.md is based
        on manual inspection rather than the Figma API metric.
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
      story). All 8 examples in examples.md are derived from the prop
      definitions and the Storybook story structure — they have not been run
      against the component. The 'useModalState' hook import path and API are
      assumed from the story pattern but not confirmed from the package's
      public exports.
    recommendation: >
      Validate examples against the Storybook or a local dev environment
      before publishing. Verify that 'useModalState' is a public export
      of '@8x8/oxygen-modal'.

  - id: WARN-002
    dimension: accessibility
    confidence: heuristic
    finding: >
      accessibility.md documents role="dialog" and aria-modal="true" as the
      correct rendered markup. This is based on the WCAG dialog pattern and
      the presence of the 'modalProps' pass-through prop — it has not been
      confirmed by inspecting the component's rendered DOM or source.
    recommendation: >
      Inspect the rendered DOM of the Modal in a browser or check the component
      source to confirm role="dialog" and aria-modal="true" are set on the
      dialog container element.

  - id: WARN-003
    dimension: token_coverage
    confidence: heuristic
    finding: >
      All token names in tokens.md use Figma CSS variable syntax
      (--ui/ui06, --text/textcolor01, --actions/action09, etc.). These may
      differ from the Oxygen token registry's canonical names or the
      @8x8/oxygen-tokens JavaScript paths used in production.
    recommendation: >
      Cross-reference token names against @8x8/oxygen-tokens or the published
      Oxygen token registry before using in implementation. Resolve GAP-002
      to obtain authoritative names.

  - id: WARN-004
    dimension: props_completeness
    confidence: heuristic
    finding: >
      ModalFooter and ModalContent have "No documented props beyond standard
      HTML attributes" in props.md. This accurately reflects what the MCP
      returned (0 props for both) but may mislead consumers — these components
      likely accept className, style, and other standard React HTML attributes.
    recommendation: >
      Add a note to the ModalFooter and ModalContent sections confirming they
      accept standard React HTML attributes (className, style, etc.) as
      pass-through.

# --- navigation ---
role: audit
pipeline_stage: spec_ready
pipeline_note: "Audit verdict YES — doc-rewrite can run"
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
> present (engineer confirmed no relevant PUI context). No CONFLICTs. No
> blocker-severity gaps. One major SOURCE_GAP (Modal-usage.md missing) —
> partially addressed by Modal-usage-draft.md (7 approved Do/Don't pairs,
> 2026-05-13). Doc-rewrite can proceed on all available dimensions.

**Audit date:** 2026-05-13 | **Rubric version:** 1.0 | **Prior audit:** 2026-05-01

---

## File inventory

| File | Status | Lines | Produced by |
|------|--------|-------|-------------|
| `props.md` | ✅ Present | 154 | oxygen-mcp-extract |
| `examples.md` | ✅ Present | 258 | oxygen-mcp-extract |
| `tokens.md` | ✅ Present | 126 | oxygen-mcp-extract |
| `accessibility.md` | ✅ Present | 170 | oxygen-mcp-extract |
| `Modal-figma.md` | ✅ Present | 268 | figma-extract |
| `Modal-pui.md` | ✅ Present (no context) | 46 | pui-mcp-extract |
| `Modal-usage.md` | ❌ Missing | — | figma-extract-usage |
| `Modal-usage-draft.md` | ⚠️ Draft present | — | usage-advisor (2026-05-13) |

---

## Dimension scores

| Dimension | Score | Coverage | Change | Status |
|-----------|-------|----------|--------|--------|
| Props completeness | 0.87 | 13/15 checks | — | ⚠️ Minor gaps |
| Examples coverage | 0.75 | 8/11 scenarios | — | ⚠️ Minor gaps |
| Token coverage | 0.70 | 8/12 checks | — | ⚠️ Source gap (MCP returned 0) |
| Accessibility | 0.83 | 9/11 checks | — | ⚠️ Inferred, not confirmed from source |
| Figma alignment | 0.72 | 7/10 checks | — | ⚠️ Variables empty; size→px mapping missing |
| Usage guidelines | 0.40 | draft only | ↑ 0.15 | ⚠️ Draft present; canonical file missing |
| Cross-file consistency | 0.93 | 19/20 checks | — | ✅ Strong |
| **Overall** | **0.74** | | **↑ 0.02** | |

---

## Gaps

### Blockers
_None._

### Major gaps

| ID | Type | Dimension | Finding |
|----|------|-----------|---------|
| GAP-001 | SOURCE_GAP | Usage guidelines | `Modal-usage.md` missing; draft with 7 approved pairs available in `Modal-usage-draft.md` |
| GAP-002 | SOURCE_GAP | Token coverage | MCP returned 0 tokens; all token data from Figma context output only |
| GAP-003 | SOURCE_GAP | Figma alignment | `figma_get_variables` + `figma_get_styles` empty; Desktop Bridge offline during extraction |

### Minor gaps

| ID | Type | Dimension | Finding |
|----|------|-----------|---------|
| GAP-004 | DOC_GAP | Figma alignment | `size` prop values (`small`/`medium`/`big`) have no px mapping; Figma breakpoint widths (320px/664px) not mapped to size presets |
| GAP-005 | SOURCE_GAP | Props completeness | `modalProps` type truncated in MCP — full type signature unknown |
| GAP-006 | DOC_GAP | Props completeness | `initialFocus` listed in both ModalPortal table and Additional props — discrepancy unresolved |
| GAP-007 | DOC_GAP | Token coverage | Size variants table incomplete — `small`/`medium`/`big` → px values unknown |
| GAP-008 | DOC_GAP | Token coverage | Spacing values (16px, 12px, 8px, 6px) not mapped to tokens |
| GAP-009 | DOC_GAP | Token coverage | 6 hardcoded Figma values (scrollbar colors, divider, radius) — tokenisation intent unconfirmed |
| GAP-010 | SOURCE_GAP | Accessibility | No ARIA annotations in Figma; a11y guidance inferred from WCAG APG, not confirmed from source |
| GAP-011 | DOC_GAP | Examples coverage | No confirmation/danger dialog example (Dialog Modal variant not illustrated in code) |
| GAP-012 | DOC_GAP | Examples coverage | `aria-describedby` example missing (recommended in accessibility.md but absent from examples) |
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
| WARN-004 | Props completeness | ModalFooter/ModalContent "no props" note may mislead — standard HTML attributes not explicitly documented |

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
| GAP-001 | Push `Modal-usage-draft.md` pairs to Figma and run figma-extract-usage **or** reference draft directly in doc-rewrite |
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

The rewrite can address the 4 auto-fixable gaps. For the usage section,
pass `Modal-usage-draft.md` as input — it contains 7 grounded Do/Don't pairs
ready for the spec. GAP-004 (size→px mapping) remains the highest-impact
human-input gap.

---

_Audit produced by doc-audit skill · Rubric version 1.0 · 2026-05-13_
