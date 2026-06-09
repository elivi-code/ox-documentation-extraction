---
rubric_version: 1.0
component: List
package: "@8x8/oxygen-list"
extracted: 2026-05-08
audited: 2026-06-08
verdict: "YES"
verdict_reason: "Zero CONFLICTs (GAP-001 resolved 2026-06-08 — ui01 confirmed as active/pressed state by designer), zero blocker-severity gaps. Remaining gaps are major/minor SOURCE_GAPs requiring upstream work."

files:
  present:
    - props.md
    - examples.md
    - tokens.md
    - accessibility.md
    - List-figma.md
    - List-pui.md
    - figma-screenshot-List.png
  absent:
    - List-usage.md  # SOURCE_GAP: no List-specific Figma examples page found

dimensions:
  props:
    score: 0.92
    coverage: "11/11 props present; all descriptions filled; all boolean defaults documented; package version placeholder added; variant composition patterns (8 Figma types) unconfirmed as code patterns (SOURCE_GAP)"
  examples:
    score: 0.68
    coverage: "7 examples present; shouldWrapText and theme examples added; no examples for secondary text, leading icon/avatar, badge, or Figma variant patterns (Destructive, Checkbox, Radio, Collapsible, etc.) — blocked on variant composition SOURCE_GAP"
  tokens:
    score: 0.78
    coverage: "CONFLICT on ui01 resolved (active/pressed state confirmed); sidebar tokens (active12, hover12, hover13) correctly attributed to SidebarMenu; Figma-confirmed tokens ui06/textColor01/textColor02/icon01 not promoted to tokens.md; dark mode hex for text/icon tokens still unresolved; spacing values hardcoded"
  accessibility:
    score: 0.50
    coverage: "Full structure present (ARIA, keyboard, disabled, screen reader, WCAG checklist) but entirely inferred; 0 MCP-sourced or Figma-annotated a11y data; isActive/isDisabled ARIA emission unverified"
  figma:
    score: 0.85
    coverage: "Screenshot present; all 8 variant types documented; anatomy + boolean toggles + token bindings confirmed via Desktop Bridge; dark text/icon hex values not resolved; padding/gap hardcoded; no ARIA annotations in Figma"
  usage:
    score: 0.0
    coverage: "File absent — no List-specific examples page found in Figma; no Do/Don't frames available"
  pui:
    score: 1.0
    coverage: "N/A confirmed — no application-layer concerns"

summary:
  doc_gaps: 1
  source_gaps: 6
  conflicts: 0
  warnings: 3

gaps:

  # ─── SOURCE GAPS (upstream Figma / MCP work needed) ────────────────────────

  - id: GAP-001
    dimension: usage
    severity: major
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: List-usage.md
      location: "File absent"
      finding: >
        No List-specific Figma examples page exists. The provided URL
        (node-id=49969:10533) resolves to "↳ Popover examples" which contains
        no frames with `✅ Do —` or `❌ Don't —` prefixes. List-usage.md was
        not written.
    fix_action: "Ask designer to create a dedicated '↳ List examples' Figma page and author Do/Don't card frames; re-run figma-extract-usage after cards are added"
    blocks: [docusaurus]
    dependency: []

  - id: GAP-002
    dimension: accessibility
    severity: major
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: accessibility.md
      location: "Lines 14, 47 — inferred notes"
      finding: >
        All accessibility content is inferred from HTML list semantics.
        The Oxygen MCP returned no a11y data; Figma has no ARIA annotations.
        Critical implementation questions remain unverified: Does `isActive`
        automatically emit `aria-current` or `aria-selected`? Does `isDisabled`
        emit `aria-disabled`? Is the focus ring implemented in the component or
        left to the browser default?
    fix_action: "Verify DOM output via Storybook or running application: inspect ARIA attributes emitted by isActive and isDisabled props, and confirm focus ring implementation; update accessibility.md with verified findings"
    blocks: [docusaurus]
    dependency: []

  - id: GAP-003
    dimension: props
    severity: major
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: List-figma.md
      location: "ListItem variant groups table, lines 30–38"
      finding: >
        Figma contains 8 distinct ListItem variant types: Single Action or Select,
        Destructive, Checkbox, Radio, Add Item, Sub Menu, Collapsible, Remove Item.
        The Oxygen MCP exposes a single generic `ListItem` with no variant-specific
        props. It is unknown whether these visual patterns are achieved through
        child composition (e.g. `<ListItem><Checkbox/></ListItem>`) or whether
        additional exports/props exist but are not registered in the MCP.
        Consumers cannot implement Destructive, Checkbox, Radio, or Collapsible
        patterns from current docs alone.
    fix_action: "Inspect @8x8/oxygen-list package exports and Storybook stories to confirm whether variant patterns (Destructive, Checkbox, Radio, Collapsible) are achieved via child composition or undocumented props/exports; document the pattern in examples.md and List.composition.md"
    blocks: [docusaurus, storybook]
    dependency: []

  - id: GAP-004
    dimension: tokens
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: List-figma.md
      location: "Color & token bindings / Text and icon table, lines 130–135"
      finding: >
        Dark mode hex values for `text/textColor01`, `text/textColor02`, and
        `icon/icon01` were not resolved — variable alias chain was not followed
        beyond one level for the dark mode path. Light values are confirmed
        (#26252A, #6C6862).
    fix_action: "Run figma_execute with getVariableByIdAsync on the dark-mode alias IDs for textColor01/textColor02/icon01 to obtain dark hex values; update List-figma.md and List.tokens.md"
    blocks: []
    dependency: []

  - id: GAP-005
    dimension: figma
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: List-figma.md
      location: "Structure & spacing table, lines 161–164"
      finding: >
        Container padding (12 px left/right, 8 px top/bottom) and inter-child
        gap (8 px) are hardcoded in Figma with no variable binding. Desktop
        Bridge confirmed no `boundVariables` on padding properties.
    fix_action: "Flag to Oxygen design team to tokenise spacing values; document in tokens.md once spacing tokens exist"
    blocks: []
    dependency: []

  - id: GAP-006
    dimension: figma
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: List-figma.md
      location: "Accessibility section, line 222"
      finding: "Figma contains no ARIA role, focus order, or keyboard interaction annotations on any ListItem variant node (Desktop Bridge confirmed no annotation objects)."
    fix_action: "Ask designer to add a11y annotations to at least the Single Action or Select variant Figma frame"
    blocks: []
    dependency: []

  # ─── DOC GAPS (requires upstream resolution before auto-fix is possible) ────

  - id: GAP-007
    dimension: examples
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: examples.md
      location: "All examples — no variant pattern examples present"
      finding: "No examples demonstrate secondary text slot (secondaryText?), leading icon/avatar composition, badge, or any of the 8 Figma visual variant patterns (Destructive, Checkbox, Radio, Collapsible, Add Item, Sub Menu, Remove Item). Requires GAP-003 resolution to document correctly."
    fix_action: "Add examples for secondary text and leading icon patterns once GAP-003 (variant composition pattern) is resolved; defer Checkbox/Radio/Collapsible patterns until confirmed"
    blocks: []
    dependency: [GAP-003]

# ─── WARNINGS (heuristic — advisory only) ──────────────────────────────────
warnings:

  - id: WARN-001
    dimension: accessibility
    confidence: heuristic
    finding: >
      `ListItem isActive` conveys selection/active state visually but it is
      unknown whether the component emits any ARIA attribute (aria-current,
      aria-selected, aria-pressed) automatically. accessibility.md advises
      adding these via a custom wrapper — but if the component already handles
      them, that guidance would be incorrect.
    advisory: "Verify via DOM inspection whether isActive emits aria-current, aria-selected, or nothing; update accessibility.md accordingly (dependent on GAP-002)"

  - id: WARN-002
    dimension: accessibility
    confidence: heuristic
    finding: >
      `ListItem isDisabled` — it is unknown whether the rendered `<li>` receives
      `aria-disabled="true"` or simply a visual CSS class. If only a CSS class is
      applied, screen readers will still announce the item as interactive.
    advisory: "Verify via DOM inspection whether isDisabled emits aria-disabled; if not, add guidance in accessibility.md to wrap with aria-disabled or use pointer-events:none"

  - id: WARN-003
    dimension: figma
    confidence: heuristic
    finding: >
      The Figma `focus` state uses `ui/ui06` (same background as rest) with a note
      "focus ring expected — not confirmed from node data". The focus ring may be
      browser default or a custom outline defined in CSS outside the component's
      fill/stroke bindings.
    advisory: "Inspect focus ring implementation; document whether it is browser default, a custom outline token, or a box-shadow effect applied in CSS"

# --- navigation (added by component-map) ---
role: audit
pipeline_stage: rewrite_done
pipeline_note: "Audit verdict YES — doc-rewrite complete; remaining gaps are SOURCE_GAPs requiring upstream work"
audit_verdict: "YES"
siblings:
  - "[[List/props]]"
  - "[[List/examples]]"
  - "[[List/tokens]]"
  - "[[List/accessibility]]"
  - "[[List/List-figma]]"
  - "[[List/List-pui]]"
tags:
  - oxygen
  - component/List
  - role/audit
  - stage/rewrite_done
  - category/data_display

---

# List — Audit Report

> **Verdict: YES** — zero CONFLICTs, zero blocker-severity gaps. `doc-rewrite` has run; hub + 7 spokes produced.
>
> Remaining open items are SOURCE_GAPs requiring upstream work (designer, Storybook inspection).

**Audited:** 2026-06-08 · **Rubric:** v1.0 · **Package:** `@8x8/oxygen-list`

---

## File inventory

| File | Status | Notes |
|------|--------|-------|
| `props.md` | ✅ Present | List (5 props) + ListItem (6 props); all descriptions filled |
| `examples.md` | ✅ Present | 7 examples; shouldWrapText + theme added; variant patterns still missing |
| `tokens.md` | ✅ Present | ui01 conflict resolved; sidebar tokens separated; dark hex still missing |
| `accessibility.md` | ✅ Present | Full structure; entirely inferred |
| `List-figma.md` | ✅ Present | Desktop Bridge; anatomy + tokens + spacing confirmed; screenshot present |
| `List-pui.md` | ✅ Present | `<!-- NO RELEVANT PUI CONTEXT -->` confirmed |
| `List-usage.md` | ⬜ Absent | **SOURCE_GAP** — no List-specific examples page in Figma |

---

## Dimension scores

| Dimension | Score | Coverage summary |
|-----------|-------|-----------------|
| Props | 0.92 | 11/11 props; all descriptions + defaults filled; variant composition unconfirmed |
| Examples | 0.68 | 7 examples; shouldWrapText + theme added; variant patterns blocked on GAP-003 |
| Tokens | 0.78 | Conflict resolved; sidebar tokens labelled; dark mode hex + spacing still gaps |
| Accessibility | 0.50 | Full structure; entirely inferred; ARIA emission unverified |
| Figma | 0.85 | Desktop Bridge; all 8 variants; token coverage confirmed; dark text hex + no annotations |
| Usage | 0.0 | File absent — no examples page found |
| PUI | N/A | Confirmed no application-layer concerns |

---

## Resolved since previous audit (2026-05-08)

| ID | What changed |
|----|-------------|
| ~~GAP-001~~ | CONFLICT resolved — `ui01` confirmed as active/pressed state background by designer (2026-06-08) |
| ~~GAP-008~~ | `ListItem.title` description added |
| ~~GAP-009~~ | `ListItem.shouldWrapText` description added |
| ~~GAP-010~~ | `isDisabled` and `isActive` defaults set to `false` |
| ~~GAP-011~~ | Sidebar tokens (active12, hover12, hover13) separated and correctly attributed |
| ~~GAP-013~~ | `shouldWrapText` and `theme` examples added |
| ~~GAP-014~~ | Package version placeholder added to install command |

---

## Open source gaps — upstream work needed

| ID | Dimension | Severity | Finding |
|----|-----------|----------|---------|
| GAP-001 | Usage | major | No List-specific Figma examples page; no Do/Don't frames |
| GAP-002 | Accessibility | major | All a11y content inferred; isActive/isDisabled ARIA behaviour unverified |
| GAP-003 | Props | major | 8 Figma ListItem visual variants not documented as code patterns |
| GAP-004 | Tokens | minor | Dark mode hex for text/icon tokens not resolved |
| GAP-005 | Figma | minor | Padding/gap values hardcoded — not tokenised |
| GAP-006 | Figma | minor | No a11y annotations in Figma on any ListItem variant |

---

## Open doc gap — blocked on upstream

| ID | Dimension | Finding |
|----|-----------|---------|
| GAP-007 | Examples | No examples for secondary text, leading icon, badge, or variant patterns — blocked on GAP-003 |

---

## Warnings (advisory)

**WARN-001 · Accessibility:** `isActive` ARIA emission unknown — verify whether it emits `aria-current`/`aria-selected` automatically or requires a wrapper.

**WARN-002 · Accessibility:** `isDisabled` ARIA emission unknown — verify whether it emits `aria-disabled` or only applies visual CSS.

**WARN-003 · Figma:** Focus ring implementation unconfirmed — browser default, token-bound outline, or CSS box-shadow?

---

## Suggested next actions

1. **GAP-003** (highest value) — inspect `@8x8/oxygen-list` package exports to confirm variant composition patterns; unblocks GAP-007 (examples)
2. **GAP-002** — verify `isActive`/`isDisabled` ARIA attributes via DOM inspection in Storybook
3. **GAP-001** — ask designer to create `↳ List examples` Figma page with Do/Don't frames

---

_Source: doc-audit skill v1.0 · Audited 2026-06-08_
