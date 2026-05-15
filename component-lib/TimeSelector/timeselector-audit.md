---
component: TimeSelector
package: "@8x8/oxygen-time-selector"
audit_date: 2026-05-15
rubric_version: "1.0"
verdict: "NO"
verdict_reason: "2 unresolved CONFLICTs about the Size=Large variant and default size mismatch between Figma and code API — requires human resolution before doc-rewrite can proceed. (Re-audit 2026-05-15: GAP-011 resolved — editorial timeselector-usage.md authored from the published Oxygen docs page via Claude_in_Chrome.)"

files_found:
  - props.md
  - examples.md
  - tokens.md
  - accessibility.md
  - timeselector-figma.md
  - timeselector-usage.md   # added 2026-05-15 — editorial, docs-mirrored (figma-extract-usage skipped)
  - figma-screenshot-timeselector.png

files_missing:
  - timeselector-pui.md     # N/A — PUI MCP search returned 0 results; no platform-layer concerns

scores:
  props:         { coverage: "8/11", score: 0.73 }
  examples:      { coverage: "6/8",  score: 0.75 }
  tokens:        { coverage: "8/9",  score: 0.89 }
  accessibility: { coverage: "5/9",  score: 0.56 }
  figma:         { coverage: "8/10", score: 0.80 }
  usage:         { coverage: "1/1",  score: 1.00 }
  pui:           { coverage: "N/A",  score: null  }

summary:
  doc_gaps: 4
  source_gaps: 5
  conflicts: 2
  warnings: 2

gaps:
  - id: GAP-001
    dimension: props
    severity: major
    type: CONFLICT
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: timeselector-figma.md
      location: "API — Variant axes table; Gaps & conflicts section"
      finding: >
        Figma component set exposes Size=Large (with distinct dimensions: 48px
        height, 120px width, 16px H / 12px V padding, $body02 typography).
        The TimeSelectorSize enum in the code API only has "small" | "default".
        "default" maps to Figma Medium. Large is entirely absent from the API.
    fix_action: >
      Human decision required: (a) add size="large" to TimeSelectorSize and
      document its dimensions, OR (b) confirm Large is intentionally excluded
      and strike it from timeselector-figma.md as a design-only variant.
    blocks: [timeselector-spec.md]
    dependency: []

  - id: GAP-002
    dimension: props
    severity: major
    type: CONFLICT
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: timeselector-figma.md
      location: "API — Variant axes table; Figma default for Size = Large"
      finding: >
        Figma default size is Large (confirmed via Desktop Bridge
        componentPropertyDefinitions). Code default for `size` prop is
        "default" (≡ Medium). The rendered output when no size is specified
        differs between Figma and code.
    fix_action: >
      Human decision required: confirm which size is the intended default and
      align either the code default or the Figma default accordingly.
    blocks: [timeselector-spec.md]
    dependency: [GAP-001]

  - id: GAP-003
    dimension: props
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: props.md
      location: "Data gaps section"
      finding: >
        onChange, onOpen, onClose callbacks appear in the Storybook
        documentation story but are absent from the OX MCP props list.
        Descriptions in props.md are inferred from usage patterns.
    fix_action: >
      Verify callback signatures against the live component source or package
      type declarations; add official descriptions to props.md once confirmed.
    blocks: []
    dependency: []

  - id: GAP-004
    dimension: props
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: props.md
      location: "Props table — hasError, timeDisplayFormat rows"
      finding: >
        hasError has no description in the OX MCP response.
        timeDisplayFormat has no description and the accepted format strings
        (e.g. whether it follows moment.js, date-fns, or a custom syntax) are
        entirely undocumented.
    fix_action: >
      Retrieve prop descriptions from package source or changelog;
      document accepted timeDisplayFormat pattern strings with examples.
    blocks: []
    dependency: []

  - id: GAP-005
    dimension: examples
    severity: minor
    type: DOC_GAP
    confidence: heuristic
    auto_fixable: false
    evidence:
      source_file: examples.md
      location: "Data note at end of file"
      finding: >
        OX MCP returned 0 clean code examples. All 8 examples in examples.md
        were reconstructed from the Storybook documentation story and Figma
        design context — they are not verbatim from the component package.
        Correctness cannot be guaranteed without live verification.
    fix_action: >
      Run figma-extract-usage or verify examples against the live Storybook
      at oxygen.8x8.com/docs/components/timeselector/usage; correct any
      divergent prop names or import paths.
    blocks: []
    dependency: []

  - id: GAP-006
    dimension: examples
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: true
    evidence:
      source_file: examples.md
      location: "No example present for timeDisplayFormat"
      finding: >
        props.md documents `timeDisplayFormat` as a string prop affecting how
        the time is displayed, but examples.md has no usage example for it.
    fix_action: >
      Add an example showing timeDisplayFormat with at least one format string
      once the accepted format syntax is confirmed (see GAP-004).
    blocks: []
    dependency: [GAP-004]

  - id: GAP-007
    dimension: tokens
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: tokens.md
      location: "Data source note; all token names"
      finding: >
        OX MCP token search returned 0 results for "timeSelector". All tokens
        are sourced from the UI-Foundations Figma library via CSS custom
        property names in design context output. Token names in tokens.md use
        Figma variable casing (e.g. --text/textColor01) which may differ from
        the OX design-token package identifiers.
    fix_action: >
      Cross-reference token names against the @8x8/oxygen-tokens package or
      the design-token catalog to confirm exact CSS custom property names used
      at runtime.
    blocks: []
    dependency: []

  - id: GAP-008
    dimension: accessibility
    severity: major
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: accessibility.md
      location: "ARIA role section; Keyboard interactions section"
      finding: >
        The OX MCP returned no accessibility documentation for TimeSelector.
        Figma annotations contain no ARIA role, keyboard interaction, or focus
        order notes. All content in accessibility.md is inferred from
        time-picker conventions and must be verified against the rendered DOM
        and component source.
    fix_action: >
      Audit the live component's rendered HTML for actual ARIA roles and
      attributes; confirm keyboard behaviour in browser; update
      accessibility.md with verified data.
    blocks: [timeselector-spec.md]
    dependency: []

  - id: GAP-009
    dimension: figma
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: timeselector-figma.md
      location: "Accessibility section — NOT ANNOTATED IN FIGMA markers"
      finding: >
        No ARIA role, focus order, or keyboard interaction annotations exist
        in the Figma component. These must be added by the designer to make
        the Figma file the authoritative a11y source.
    fix_action: >
      Request designer to add accessibility annotations to the Figma component
      for ARIA role, keyboard interactions, and focus order.
    blocks: []
    dependency: []

  - id: GAP-010
    dimension: figma
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: timeselector-figma.md
      location: "Token coverage section"
      finding: >
        Token coverage % could not be computed: the UI-components Figma file
        has 0 local variables — all design tokens are consumed from the
        external UI-Foundations library which cannot be queried via Desktop
        Bridge when UI-components is the active file.
    fix_action: >
      Token coverage % must be derived manually by comparing the hardcoded
      values list against the total number of design properties in the
      component. Current hardcoded properties: border-radius (6px) on input
      and icon button; all spacing/padding values.
    blocks: []
    dependency: []

  # GAP-011 RESOLVED 2026-05-15 — timeselector-usage.md authored editorially
  # from the published Oxygen docs page (https://oxygen.8x8.com/components/timeselector/usage,
  # fetched via Claude_in_Chrome MCP) cross-validated against props.md, examples.md,
  # tokens.md, accessibility.md, and timeselector-figma.md. figma-extract-usage was
  # skipped per direction — no Figma "↳ TimeSelector examples" page located.
  # Replace with figma-extract-usage output if a Figma examples page is ever created.

warnings:
  - id: WARN-001
    dimension: accessibility
    confidence: heuristic
    finding: >
      WCAG 1.4.3 contrast for disabled state
      (--interactive/disabled04 #8D8B7E on --interactive/disabled01 #C8C8BD)
      has not been verified. Ratio may fall below 4.5:1 for normal text.
      Decorative exemption may apply if disabled text is purely presentational.
    advisory: "Verify contrast ratio before shipping."

  - id: WARN-002
    dimension: examples
    confidence: heuristic
    finding: >
      The ClockIcon import in the "With a left icon" example uses
      "@8x8/oxygen-icons" — this package name has not been verified against
      the actual Oxygen icon package identifier.
    advisory: "Confirm icon package name before publishing the example."
# --- navigation (added by component-map) ---
role: audit
pipeline_stage: blocked
pipeline_note: "Audit verdict NO — CONFLICTs must be resolved first"
audit_verdict: "NO"
siblings:
  - "[[TimeSelector/props]]"
  - "[[TimeSelector/examples]]"
  - "[[TimeSelector/tokens]]"
  - "[[TimeSelector/accessibility]]"
  - "[[TimeSelector/timeselector-figma]]"
  - "[[TimeSelector/timeselector-usage]]"
tags:
  - oxygen
  - component/TimeSelector
  - role/audit
  - stage/blocked
  - category/date_time

---

# TimeSelector — Audit Report

**Verdict: NO** — 2 unresolved CONFLICTs must be resolved before doc-rewrite can run.

**Audit date:** 2026-05-07 · **Rubric:** v1.0

---

## File inventory

| File | Status |
|------|--------|
| `props.md` | ✅ Present |
| `examples.md` | ✅ Present |
| `tokens.md` | ✅ Present |
| `accessibility.md` | ✅ Present |
| `timeselector-figma.md` | ✅ Present |
| `timeselector-usage.md` | ✅ Present (editorial, docs-mirrored — added 2026-05-15) |
| `timeselector-pui.md` | — N/A (PUI MCP returned 0 results; no platform-layer concerns) |

---

## Dimension scores

| Dimension | Coverage | Score | Blocker? |
|-----------|----------|-------|----------|
| Props | 8/11 | 0.73 | — |
| Examples | 6/8 | 0.75 | — |
| Tokens | 8/9 | 0.89 | — |
| Accessibility | 5/9 | 0.56 | ⚠️ Major source gaps |
| Figma | 8/10 | 0.80 | — |
| Usage | 1/1 | 1.00 | — *(editorial, docs-mirrored — see pipeline note in [timeselector-usage.md](timeselector-usage.md))* |
| PUI | N/A | — | — |

---

## Conflicts (must resolve before rewrite)

### GAP-001 · CONFLICT · Props + Figma · major

**Figma exposes Size=Large; code API does not.**

Figma has a fully specced Large variant (48px input height, 120px width, 16px H / 12px V padding, `$body02` typography). `TimeSelectorSize` only accepts `"small" | "default"`. The Large size is not accessible via code.

**Fix:** Human decision — add `size="large"` to the API, or confirm Large is intentionally design-only and document accordingly.

### GAP-002 · CONFLICT · Props + Figma · major *(depends on GAP-001)*

**Figma default size is Large; code default is "default" (Medium).**

Confirmed via Desktop Bridge `componentPropertyDefinitions`. A consumer rendering `<TimeSelector />` without a size prop gets Medium in code but Large in Figma. These must be aligned.

**Fix:** Align defaults once GAP-001 is resolved.

---

## Source gaps

| ID | Dimension | Severity | Finding |
|----|-----------|----------|---------|
| GAP-003 | Props | minor | onChange/onOpen/onClose callbacks inferred from story, not in official props list |
| GAP-004 | Props | minor | hasError and timeDisplayFormat have no official descriptions; format strings undocumented |
| GAP-007 | Tokens | minor | Token names are Figma variable names — may differ from OX design-token package identifiers |
| GAP-008 | Accessibility | major | All a11y content inferred from conventions — not sourced from OX MCP or Figma annotations |
| GAP-009 | Figma | minor | No ARIA/keyboard/focus annotations in Figma source |
| GAP-010 | Figma | minor | Token coverage % not computable (external library limitation) |
| ~~GAP-011~~ | ~~Usage~~ | ~~major~~ | **Resolved 2026-05-15** — editorial `timeselector-usage.md` authored from published Oxygen docs page (via Claude_in_Chrome). Replace with `figma-extract-usage` output if a Figma examples page is ever created. |

---

## Doc gaps

| ID | Dimension | Severity | Auto-fixable | Finding |
|----|-----------|----------|-------------|---------|
| GAP-005 | Examples | minor | No | All examples reconstructed from story/Figma — not from clean MCP output |
| GAP-006 | Examples | minor | Yes (after GAP-004) | No example for timeDisplayFormat |

---

## Warnings

| ID | Dimension | Advisory |
|----|-----------|---------|
| WARN-001 | Accessibility | Disabled state contrast ratio unverified — may not meet WCAG 1.4.3 |
| WARN-002 | Examples | ClockIcon import package name unverified |

---

## Suggested next actions

1. **Resolve GAP-001 + GAP-002** — decide whether `size="large"` is added to the code API and align Figma defaults. This unblocks the rewrite verdict.
2. **Verify accessibility** (GAP-008) — inspect rendered DOM for actual ARIA roles and keyboard behaviour.
3. **Verify `timeDisplayFormat` syntax** (GAP-004) — confirm whether it follows moment / date-fns / a custom syntax; update `props.md` + replace the placeholder caveat in `timeselector-usage.md`.
4. **Optional — run `figma-extract-usage` later.** The current `timeselector-usage.md` is an editorial mirror of the published Oxygen docs page (resolves GAP-011). If a Figma `↳ TimeSelector examples` page is ever created with Do/Don't card frames, re-run `figma-extract-usage` and replace the editorial pairs.
5. Re-run audit after conflicts are resolved → expect verdict to upgrade to **PARTIAL** or **YES**.

_Audit produced by doc-audit skill · Updated 2026-05-15_
