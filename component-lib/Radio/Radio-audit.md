---
rubric_version: "1.0"
component: Radio
package: "@8x8/oxygen-radio"
audit_date: "2026-05-15"
auditor: doc-audit skill
updated: "2026-05-15"

file_inventory:
  present:
    - props.md
    - examples.md
    - tokens.md
    - accessibility.md
    - Radio-usage.md          # editorial — see WARN-001
    - Radio-usage.html        # HTML render of Radio-usage.md
  missing:
    - Radio-figma.md
    - Radio-pui.md

dimension_scores:
  props_completeness:   { score: 0.85, coverage: "9/9 Radio props + 5/5 RadioGroup props listed with types, defaults, required flags, and descriptions; `value` union type detailed separately; deterministic from MCP source" }
  examples_quality:     { score: 0.85, coverage: "8 examples covering basic vertical group, horizontal, disabled options, info-tooltip, full Storybook documentation story, form-field Slot pattern, no-label Radio Button Input, and overflow/multiline labels; both Radio and RadioGroup compositions shown" }
  token_coverage:       { score: 0.45, coverage: "Only `$spacing(2)` (8px gap between items) documented from Figma node 50606:93474; no per-state colour/border/shadow token bindings — Radio has 8 listed states (Rest/Hover/Focused/Disabled × IsChecked) but tokens.md lists no state-to-token mapping. Resolution blocked by GAP-001 (Figma not extracted)" }
  accessibility:        { score: 0.90, coverage: "Complete ARIA table (radiogroup/radio roles, aria-labelledby, aria-checked, aria-disabled, info-button aria-label), full keyboard interactions including arrow navigation, screen-reader guidance, focus-ring scope from Figma, font-scaling and zoom behaviour, multiline alignment, 8-row WCAG 2.1 AA checklist — deterministic from MCP + Figma source" }
  figma_fidelity:       { score: 0.0,  coverage: "Radio-figma.md absent. figma-extract has not been run. Figma nodes are known (UI-components 51776:2800, 50606:93474 — referenced from examples.md, tokens.md, accessibility.md), so this is recoverable by running figma-extract Radio" }
  pui_integration:      { score: 0.50, coverage: "Radio-pui.md absent. No `<!-- NO RELEVANT PUI CONTEXT -->` marker has been written to formally confirm the PUI dimension. Radio is a pure form input — Platform UI integration is unlikely but should be confirmed" }
  usage_guidelines:     { score: 0.70, coverage: "Radio-usage.md present (editorial — see WARN-001); 6 grounded Do/Don't pairs derived from the published Oxygen docs page (https://oxygen.8x8.com/components/radiobutton/usage, fetched 2026-05-14) cross-validated against props.md / examples.md / tokens.md / accessibility.md; HTML render also present; missing Figma-sourced verification" }

overall_score: 0.61

counts:
  doc_gaps: 0
  source_gaps: 3
  conflicts: 0
  warnings: 1

verdict: PARTIAL
verdict_reason: >
  GAP-001 is a blocker SOURCE_GAP: Radio-figma.md is absent because
  figma-extract has not yet been run. Unlike SlideOut, this is recoverable
  — Figma nodes are known (UI-components 51776:2800 and 50606:93474, referenced
  from multiple extracted files) and figma-extract Radio can produce the
  file directly. Zero CONFLICTs exist. doc-rewrite can proceed on six
  dimensions (props, examples, tokens, accessibility, usage, pui) with the
  caveats that token_coverage is light without Figma state bindings and
  pui_integration needs a formal N/A marker. Run figma-extract Radio to
  promote this verdict to YES.

gaps:
  - id: GAP-001
    dimension: figma_fidelity
    severity: blocker
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: "(file absent)"
      location: "Radio-figma.md — not present in directory"
      finding: >
        No Radio-figma.md exists. figma-extract has not been run for Radio.
        The Figma nodes are referenced from `examples.md:198`, `tokens.md:69`,
        and `accessibility.md:101` as UI-components nodes 51776:2800 and
        50606:93474, so this is straightforward to resolve by running
        figma-extract — unlike SlideOut, no upstream design work is needed.
    fix_action: "Run `/figma-extract Radio` against UI-components nodes 51776:2800 and 50606:93474. This will produce `Radio-figma.md` and a screenshot. After it lands, re-run `/doc-audit Radio` to promote the verdict from PARTIAL to YES."
    blocks: [doc-rewrite-figma-dimension, token_coverage-state-bindings]
    dependency: []

  - id: GAP-002
    dimension: pui_integration
    severity: major
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: "(file absent)"
      location: "Radio-pui.md — not present in directory"
      finding: >
        No Radio-pui.md exists. Radio is a pure form input — Platform UI
        integration is unlikely (no navigation, notification, session, or
        event-bus concerns) — but no explicit N/A marker has been written
        to formally confirm this determination in the file inventory.
    fix_action: "Run `/pui-mcp-extract Radio` to confirm there are no PUI concerns. If confirmed, write a minimal `Radio-pui.md` containing only the `<!-- NO RELEVANT PUI CONTEXT -->` marker to formally close this dimension."
    blocks: []
    dependency: []

  - id: GAP-003
    dimension: token_coverage
    severity: major
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: tokens.md
      location: "tokens.md:25-36 — only `$spacing(2)` (8px gap) is documented"
      finding: >
        tokens.md declares only one Radio-specific binding (`$spacing(2)` →
        8px gap between RadioGroup items, confirmed from Figma node
        50606:93474). The component exposes 8 states (Rest, Hover, Focused,
        Disabled, IsChecked variants) — see tokens.md:50-59 — but no
        state-to-colour, state-to-border, or state-to-shadow token bindings
        are present. The MCP token search returned no dedicated Radio
        tokens. This dimension cannot be completed without inspecting the
        Figma variants (blocked by GAP-001) or the component's CSS source.
    fix_action: "Run `/figma-extract Radio` to capture per-state token bindings from the variants on nodes 51776:2800 / 50606:93474; or inspect the `@8x8/oxygen-radio` component source to identify which design tokens are consumed for each state. Update tokens.md with a state × token table."
    blocks: [doc-rewrite]
    dependency: [GAP-001]

warnings:
  - id: WARN-001
    dimension: usage_guidelines
    confidence: heuristic
    added: "2026-05-15"
    finding: >
      Radio-usage.md is editorial — drafted on 2026-05-14 from the published
      Oxygen docs page (https://oxygen.8x8.com/components/radiobutton/usage,
      fetched via the Claude_in_Chrome MCP) cross-validated against the
      extracted MCP artifacts. The 6 Do/Don't pairs are not from a Figma
      `↳ Radio examples` page with card frames (no such page exists). The
      pairs are well-grounded with file:line citations into props.md /
      examples.md / tokens.md / accessibility.md and verbatim quotes from
      the public docs page, but they have not been validated against a
      Figma source-of-truth or designer review.
    advisory: "Treat the usage doc as canonical for now (mirrors the published Oxygen docs). If a Figma `↳ Radio examples` page is ever authored with `✅ Do —` / `❌ Don't —` card frames, run figma-extract-usage to overwrite Radio-usage.md and confirm whether each editorial pair survives. The published docs URL is the current canonical authority."

# --- navigation (added by component-map) ---
role: audit
pipeline_stage: spec_ready
pipeline_note: "Audit verdict PARTIAL — doc-rewrite can run on 6 of 7 dimensions; usage is editorial (WARN-001); figma_fidelity recoverable by running figma-extract Radio."
siblings:
  - "[[Radio/props]]"
  - "[[Radio/examples]]"
  - "[[Radio/tokens]]"
  - "[[Radio/accessibility]]"
  - "[[Radio/Radio-usage]]"
tags:
  - oxygen
  - component/Radio
  - role/audit
  - stage/spec_ready
---

# Radio — Audit Report

> **Verdict: PARTIAL** — GAP-001 is a recoverable blocker SOURCE_GAP: `Radio-figma.md` is absent because figma-extract has not been run yet. Figma nodes are known (UI-components 51776:2800, 50606:93474), so `/figma-extract Radio` will resolve this directly. Zero CONFLICTs. `doc-rewrite` can proceed on 6 of 7 dimensions (props, examples, tokens, accessibility, usage, pui) — token_coverage is light without state bindings; pui needs a formal N/A marker.
>
> Rubric version: 1.0 · Audit date: 2026-05-15

## Summary

| Dimension | Score | Status |
|-----------|-------|--------|
| Props completeness | 0.85 | 9 Radio + 5 RadioGroup props; types / defaults / descriptions all present; deterministic |
| Examples quality | 0.85 | 8 examples — basic, horizontal, disabled, info-tooltip, full Storybook story, form Slot pattern, no-label, multiline |
| Token coverage | 0.45 | Only `$spacing(2)` documented; state-to-token bindings unresolved (blocked by GAP-001) |
| Accessibility | 0.90 | Full ARIA, keyboard, screen-reader, focus, font-scaling, zoom, multiline; 8-row WCAG checklist |
| Figma fidelity | 0.00 | `Radio-figma.md` absent — figma-extract not yet run (GAP-001) |
| PUI integration | 0.50 | `Radio-pui.md` absent; no N/A marker written |
| Usage guidelines | 0.70 | ✅ Editorial; 6 pairs mirrored from published Oxygen docs page (WARN-001); +HTML render |
| **Overall** | **0.61** | |

## Gap register

| ID | Dimension | Severity | Type | Summary |
|----|-----------|----------|------|---------|
| GAP-001 | figma_fidelity | blocker | SOURCE_GAP | `Radio-figma.md` absent — figma-extract not run. **Recoverable** (Figma nodes known: 51776:2800, 50606:93474) |
| GAP-002 | pui_integration | major | SOURCE_GAP | `Radio-pui.md` absent; no `<!-- NO RELEVANT PUI CONTEXT -->` marker written |
| GAP-003 | token_coverage | major | SOURCE_GAP | Only `$spacing(2)` documented; per-state colour/border/shadow token bindings missing; blocked by GAP-001 |

## Warnings

| ID | Dimension | Advisory |
|----|-----------|---------|
| WARN-001 | usage_guidelines | `Radio-usage.md` is editorial — mirrors `oxygen.8x8.com/components/radiobutton/usage` (fetched 2026-05-14). Replace with `figma-extract-usage` output if a Figma `↳ Radio examples` page is ever authored |

## Resolution path

The fastest path from PARTIAL → YES:

1. **GAP-001 + GAP-003 (Figma + tokens):** Run `/figma-extract Radio` against UI-components nodes 51776:2800 and 50606:93474. This produces `Radio-figma.md` with anatomy, variant axes, and per-state token bindings — closing GAP-001 directly and giving GAP-003 the data it needs.
2. **GAP-002 (PUI):** Run `/pui-mcp-extract Radio`. Likely confirms no PUI concerns; write a minimal `Radio-pui.md` with the `<!-- NO RELEVANT PUI CONTEXT -->` marker to formally close.
3. **Re-audit:** Run `/doc-audit Radio` again — verdict should promote to YES.

All three closure paths are deterministic and require no human decisions. WARN-001 is advisory and does not block rewrite.

## Notes on the editorial usage doc

`Radio-usage.md` was drafted via the docs-mirrored mode on 2026-05-14 with explicit verbatim quotes from `oxygen.8x8.com/components/radiobutton/usage` plus file:line citations into the extracted artifacts. It is currently the canonical authority on Radio usage because no Figma examples page exists. This is a stronger editorial provenance than SlideOut's (which had no public docs page to mirror) and is reflected in the higher usage_guidelines score (0.70 vs 0.55).
