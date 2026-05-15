---
rubric_version: 1.0
component: List
package: "@8x8/oxygen-list"
extracted: 2026-05-08
audited: 2026-05-08
verdict: "NO"
verdict_reason: "1 CONFLICT requires human resolution — token ui01 described as 'selected state' in tokens.md but Figma Desktop Bridge confirms it is the active/pressed state; no background change occurs for selected state"

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
    - List-usage.md  # SOURCE_GAP: ↳ Popover examples page has no Do/Don't card frames; no List-specific examples page found

dimensions:
  props:
    score: 0.82
    coverage: "11/11 props present; 2 props (ListItem.title, ListItem.shouldWrapText) have no descriptions; isDisabled and isActive have no default values documented"
  examples:
    score: 0.55
    coverage: "5 examples present but all derived from 1 documentation story; 0 clean MCP-sourced snippets; no examples for secondary text, leading icon, badge, Figma visual variant patterns"
  tokens:
    score: 0.60
    coverage: "6 tokens from Oxygen MCP; Figma-confirmed bindings (ui/ui06, ui/ui02, ui/ui01, text/textColor01, text/textColor02, icon/icon01) richer than MCP tokens; 1 semantic conflict on ui01 description"
  accessibility:
    score: 0.50
    coverage: "Full structure present (ARIA, keyboard, disabled, screen reader, WCAG checklist) but entirely inferred; 0 MCP-sourced or Figma-annotated a11y data"
  figma:
    score: 0.85
    coverage: "Screenshot present; all 8 variant types documented; anatomy + boolean toggles + instance swap + token bindings + spacing confirmed via Desktop Bridge; dark text/icon hex values not fully resolved"
  usage:
    score: 0.0
    coverage: "File absent — no List-specific examples page found in Figma; Popover examples page has no Do/Don't frames"
  pui:
    score: 1.0
    coverage: "N/A confirmed — no PUI context (single false-positive candidate rejected)"

summary:
  doc_gaps: 7
  source_gaps: 6
  conflicts: 1
  warnings: 3

gaps:

  # ─── CONFLICTS (human decision required) ───────────────────────────────────

  - id: GAP-001
    dimension: tokens
    severity: major
    type: CONFLICT
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: tokens.md
      location: "Color tokens table, ui01 row, line 16"
      finding: >
        tokens.md describes `ui01` as "selected state background color for list items"
        (sourced from Oxygen MCP token registry description). List-figma.md (Desktop
        Bridge confirmed) shows `ui/ui01` is applied to the `active` (pointer-down)
        state, not the selected state. The selected state (`selected?=true`) uses
        `ui/ui06` (white/dark-purple) — identical to the rest state — because
        selection is communicated by trailing icon visibility alone, not background
        colour. The two sources directly contradict each other on what state ui01
        represents.
    fix_action: "Confirm with designer whether 'selected state background' in the token description refers to the pressed/active state (not selection state); update tokens.md description to match Figma intent — either 'active/pressed state background' or document that selection is icon-only"
    blocks: [docusaurus]
    dependency: []

  # ─── SOURCE GAPS (upstream Figma / MCP work needed) ────────────────────────

  - id: GAP-002
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

  - id: GAP-003
    dimension: accessibility
    severity: major
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: accessibility.md
      location: "Lines 14, 47 — inferred notes"
      finding: >
        All accessibility content is inferred from the component's HTML list
        semantics. The Oxygen MCP returned no a11y data; Figma has no ARIA
        annotations. Critical implementation questions are unverified: Does
        `isActive` automatically emit `aria-current` or `aria-selected`? Does
        `isDisabled` emit `aria-disabled`? Is the focus ring implemented in
        the component or left to the browser default?
    fix_action: "Verify DOM output via Storybook or running application: inspect aria attributes emitted by isActive and isDisabled props, and confirm focus ring implementation"
    blocks: [docusaurus]
    dependency: []

  - id: GAP-004
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
        additional exports/props exist but are not registered in the MCP. Consumers
        cannot implement Destructive, Checkbox, Radio, or Collapsible patterns from
        current docs alone.
    fix_action: "Inspect @8x8/oxygen-list package exports and Storybook stories to confirm whether variant patterns (Destructive, Checkbox, Radio, Collapsible) are achieved via child composition or undocumented props/exports; document the pattern in examples.md"
    blocks: [docusaurus, storybook]
    dependency: []

  - id: GAP-005
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
    fix_action: "Run figma_execute with getVariableByIdAsync on the dark-mode alias IDs for textColor01/textColor02/icon01 to obtain dark hex values; update List-figma.md"
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
      location: "Structure & spacing table, lines 161–164"
      finding: >
        Container padding (12 px left/right, 8 px top/bottom) and inter-child
        gap (8 px) are hardcoded in Figma with no variable binding. Desktop
        Bridge confirmed no `boundVariables` on padding properties.
    fix_action: "Flag to Oxygen design team to tokenise spacing values; document in tokens.md once spacing tokens exist"
    blocks: []
    dependency: []

  - id: GAP-007
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

  # ─── DOC GAPS (auto-fixable by doc-rewrite) ─────────────────────────────────

  - id: GAP-008
    dimension: props
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: true
    evidence:
      source_file: props.md
      location: "ListItem props table, title row, line 41"
      finding: "`ListItem.title` prop has no description — the MCP source returned an empty string."
    fix_action: "Add description: 'HTML title attribute applied to the <li> element; appears as browser tooltip on hover; useful when item text is truncated'"
    blocks: []
    dependency: []

  - id: GAP-009
    dimension: props
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: true
    evidence:
      source_file: props.md
      location: "ListItem props table, shouldWrapText row, line 45"
      finding: "`ListItem.shouldWrapText` prop has no description — the MCP source returned an empty string."
    fix_action: "Add description: 'When false, item text is clipped to a single line; when true (or unset), text wraps to multiple lines'"
    blocks: []
    dependency: []

  - id: GAP-010
    dimension: props
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: true
    evidence:
      source_file: props.md
      location: "ListItem props table, isDisabled and isActive rows, lines 43–44"
      finding: "`ListItem.isDisabled` and `ListItem.isActive` have no default values documented (MCP returned no defaults for these boolean props)."
    fix_action: "Add default: false for both isDisabled and isActive (standard boolean prop convention)"
    blocks: []
    dependency: []

  - id: GAP-011
    dimension: tokens
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: true
    evidence:
      source_file: tokens.md
      location: "Color tokens table, lines 13–15"
      finding: >
        `active12`, `hover12`, and `hover13` are listed in tokens.md because the
        Oxygen MCP token search for "list" returned them. Their descriptions
        reference "sidebar menu list items" and "floating menu list items" —
        they are sidebar-context tokens, not tokens used by @8x8/oxygen-list.
        Including them without qualification creates false attribution.
    fix_action: "Add a note to each row clarifying these tokens apply to SidebarMenu list items, not to the List/ListItem component; or move them to a separate 'Related sidebar tokens' subsection"
    blocks: []
    dependency: [GAP-001]

  - id: GAP-012
    dimension: examples
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: examples.md
      location: "All 5 examples — footer note, line 60"
      finding: >
        No examples demonstrate: secondary text slot (secondaryText?), leading
        icon/avatar composition, badge, or any of the 8 Figma visual variant
        patterns (Destructive, Checkbox, Radio, Collapsible, Add Item, Sub Menu,
        Remove Item). These require GAP-004 resolution to document correctly.
    fix_action: "Add examples for secondary text and leading icon patterns once GAP-004 (variant composition pattern) is resolved; defer Checkbox/Radio/Collapsible patterns until confirmed"
    blocks: []
    dependency: [GAP-004]

  - id: GAP-013
    dimension: examples
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: true
    evidence:
      source_file: examples.md
      location: "All 5 examples"
      finding: "`theme` prop is not demonstrated in any example. `shouldWrapText` is also not demonstrated."
    fix_action: "Add a brief example or note for shouldWrapText={false} (single-line truncation); theme prop usage can be noted as 'provided by Oxygen theme provider — override only when using outside standard setup'"
    blocks: []
    dependency: []

  - id: GAP-014
    dimension: props
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: true
    evidence:
      source_file: props.md
      location: "Installation section, line 9"
      finding: "Package version is absent from the install command."
    fix_action: "Add package version to install command once confirmed from Artifactory registry (e.g. @8x8/oxygen-list@<version>)"
    blocks: []
    dependency: []

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
    advisory: "Verify via DOM inspection whether isActive emits aria-current, aria-selected, or nothing; update accessibility.md accordingly (dependent on GAP-003)"

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
      fill/stroke bindings. If it relies on browser default, it may not meet WCAG
      2.4.11 (Focus Appearance) in all browsers.
    advisory: "Inspect focus ring implementation; document whether it is browser default, a custom outline token, or a box-shadow effect applied in CSS"
# --- navigation (added by component-map) ---
role: audit
pipeline_stage: blocked
pipeline_note: "Audit verdict NO — CONFLICTs must be resolved first"
audit_verdict: "NO"
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
  - stage/blocked
  - category/data_display

---

# List — Audit Report

> **Verdict: NO** — 1 conflict requires human resolution before `doc-rewrite` can run.
>
> Resolve GAP-001 (token ui01 semantic description), then re-run this audit.

**Audited:** 2026-05-08 · **Rubric:** v1.0 · **Package:** `@8x8/oxygen-list`

---

## File inventory

| File | Status | Notes |
|------|--------|-------|
| `props.md` | ✅ Present | List (5 props) + ListItem (6 props) |
| `examples.md` | ✅ Present | 5 examples; 0 MCP-clean; all derived from documentation story |
| `tokens.md` | ✅ Present | 6 tokens from MCP; 1 semantic conflict with Figma data |
| `accessibility.md` | ✅ Present | Full structure; entirely inferred |
| `List-figma.md` | ✅ Present | Desktop Bridge; anatomy + tokens + spacing confirmed; screenshot present |
| `List-pui.md` | ✅ Present | `<!-- NO RELEVANT PUI CONTEXT -->` confirmed |
| `List-usage.md` | ⬜ Absent | **SOURCE_GAP** — no List-specific examples page in Figma |

---

## Dimension scores

| Dimension | Score | Coverage summary |
|-----------|-------|-----------------|
| Props | 0.82 | 11/11 props present; 2 missing descriptions; 2 missing defaults |
| Examples | 0.55 | 5 examples; 0 MCP-clean; missing variant patterns |
| Tokens | 0.60 | 6 MCP tokens; 1 semantic conflict; Figma bindings richer but not promoted |
| Accessibility | 0.50 | Full structure; entirely inferred; 0 verified data |
| Figma | 0.85 | Desktop Bridge; all 8 variants; 100% color token coverage; minor dark-text gap |
| Usage | 0.0 | File absent — no examples page found |
| PUI | N/A | Confirmed no application-layer concerns |

---

## Conflicts — must resolve before rewrite

### GAP-001 · CONFLICT · Tokens · major

**Finding:** `tokens.md` describes `ui01` as **"selected state background color for list items"** (Oxygen MCP token registry). `List-figma.md` (Desktop Bridge confirmed) shows `ui/ui01` is applied to the **active/pressed** state (`state=active`). The **selected** state (`selected?=true`) uses `ui/ui06` (white in light mode) — same background as rest — because selection is communicated through trailing icon visibility only.

These two sources directly contradict each other on what state `ui01` represents.

**Fix:** Confirm with designer whether "selected state" in the token description refers to the pressed/active interaction state (not a persistent selection state). Update `tokens.md` description: either "active/pressed state background for list items" or document that selection is icon-only and `ui01` is the pressed colour.

---

## Source gaps — upstream work needed

| ID | Dimension | Severity | Finding |
|----|-----------|----------|---------|
| GAP-002 | Usage | major | No List-specific Figma examples page; Popover examples page has no Do/Don't frames |
| GAP-003 | Accessibility | major | All a11y content inferred; isActive/isDisabled ARIA behaviour unverified |
| GAP-004 | Props | major | 8 Figma ListItem visual variants not documented as code patterns; composition approach unconfirmed |
| GAP-005 | Tokens | minor | Dark mode hex for text/icon tokens not resolved |
| GAP-006 | Figma | minor | Padding/gap values hardcoded (12px, 8px) — not tokenised in Figma |
| GAP-007 | Figma | minor | No a11y annotations in Figma on any ListItem variant |

---

## Doc gaps — auto-fixable by doc-rewrite

| ID | Dimension | Finding |
|----|-----------|---------|
| GAP-008 | Props | `ListItem.title` has no description |
| GAP-009 | Props | `ListItem.shouldWrapText` has no description |
| GAP-010 | Props | `ListItem.isDisabled` and `isActive` have no default values |
| GAP-011 | Tokens | `active12`, `hover12`, `hover13` attributed to this component but are sidebar tokens |
| GAP-012 | Examples | No examples for secondary text, leading icon, badge, or Figma variant patterns (blocks on GAP-004) |
| GAP-013 | Examples | `theme` and `shouldWrapText` props not demonstrated |
| GAP-014 | Props | Package version absent from install command |

---

## Warnings (advisory)

**WARN-001 · Accessibility:** `isActive` ARIA emission unknown — verify whether it emits `aria-current`/`aria-selected` automatically or requires a wrapper.

**WARN-002 · Accessibility:** `isDisabled` ARIA emission unknown — verify whether it emits `aria-disabled` or only applies visual CSS.

**WARN-003 · Figma:** Focus ring implementation unconfirmed — browser default, token-bound outline, or CSS box-shadow? May affect WCAG 2.4.11 compliance.

---

## Suggested next actions

1. **Resolve GAP-001** — clarify with designer whether `ui01` = active/pressed state (not selection state); update `tokens.md` description
2. Once conflict is resolved, **re-run doc-audit** — verdict should flip to **PARTIAL** (1 major source gap: GAP-004)
3. **Resolve GAP-004** — inspect `@8x8/oxygen-list` package exports to confirm composition patterns for Destructive/Checkbox/Radio/Collapsible
4. Once GAP-004 resolved, run **doc-rewrite** — it can auto-fix GAP-008 through GAP-014

---

_Source: doc-audit skill v1.0 · Audited 2026-05-08_
