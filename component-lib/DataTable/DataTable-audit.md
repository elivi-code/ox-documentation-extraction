---
component: DataTable
rubric_version: "1.0"
extracted: 2026-05-06
audited: 2026-05-12
verdict: "NO"
verdict_reason: "2 unresolved CONFLICTs (GAP-001 Pagination, GAP-002 cell type mapping) must be resolved before doc-rewrite can proceed. DataTable-usage.md was authored editorially on 2026-05-12 in derivation-only mode; usage dimension now scored."

files_found:
  - props.md
  - examples.md
  - tokens.md
  - accessibility.md
  - DataTable-figma.md
  - DataTable-usage.md

files_missing:
  - DataTable-pui.md

scores:
  props: 0.70
  examples: 0.85
  tokens: 0.45
  accessibility: 0.80
  figma: 0.60
  usage: 0.80
  pui: null

counts:
  doc_gaps: 5
  source_gaps: 11
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
      source_file: props.md
      location: "## `<Pagination>` section, lines 92–110 and note at line 110"
      finding: >
        MCP-returned Pagination props (canGoBack, canGoNext, numberOfPages, pageNumber,
        rowsPerPage) are mutually exclusive with example-observed props (limit, offset,
        totalResults, loadingData). The two interfaces do not align — props.md documents
        both sets simultaneously without resolving which is the public API.
    fix_action: >
      Determine whether Pagination accepts (limit/offset/totalResults) or
      (pageNumber/rowsPerPage/canGoBack/canGoNext) as its primary API; confirm
      whether usePagination() is a required adapter or an optional helper, then
      update props.md to reflect a single canonical interface.
    blocks:
      - doc-rewrite
      - storybook
    dependency: []

  - id: GAP-002
    dimension: figma
    severity: major
    type: CONFLICT
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: DataTable-figma.md
      location: "## Gaps & conflicts, last row"
      finding: >
        Figma `table cell` component set uses a single component with an 18-value
        `type` variant (default, checkbox, radio, avatar, switch, text input,
        select input, icons, tag, link, action, trend, trend filled, status,
        sentiment, error filled, empty state, skeleton). Oxygen code uses separate
        named components (TextCell, PrimaryTextCell, CheckboxCell, etc.) via
        columnHelper.accessor cell callbacks — no `type` prop on `<Cell>`. The
        design-to-code mapping is undefined.
    fix_action: >
      Create an explicit mapping table: Figma cell type → Oxygen cell component
      (e.g. type=default → TextCell, type=checkbox → CheckboxCell). Confirm with
      the design team whether unmapped types (avatar, switch, tag, link, action,
      trend, sentiment) have corresponding Oxygen components or are custom
      implementations.
    blocks:
      - doc-rewrite
      - storybook
    dependency: []

  - id: GAP-003
    dimension: props
    severity: major
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: examples.md
      location: "All examples — cell callbacks use TextCell, PrimaryTextCell, SecondaryTextCell"
      finding: >
        TextCell, PrimaryTextCell, and SecondaryTextCell are used in every
        example but have no documented props in props.md. They are exported
        from the dataTable package and accept at minimum: primaryText, and
        for TextCell: isInactive. Users cannot configure them without finding
        the source.
    fix_action: >
      Add prop tables for TextCell, PrimaryTextCell, SecondaryTextCell
      (and any other named cell components) to props.md. Run
      get-component-props on each to retrieve MCP data, supplementing
      with example-observed props.
    blocks:
      - doc-rewrite
    dependency: [GAP-002]

  - id: GAP-004
    dimension: props
    severity: minor
    type: DOC_GAP
    confidence: heuristic
    auto_fixable: false
    evidence:
      source_file: props.md
      location: "## `<Table>` section, lines 22–41"
      finding: >
        Table props beyond `children` and `zebra` (loading, tableApi, ariaLabel,
        onRowClick, getRowActions, getRowStatus, enableVirtualization, activeRowId,
        loadingText) are inferred from examples, not returned by the MCP. The MCP
        returned only 2 props. TypeScript types for generic parameters (Table<T>,
        Row<T>) are noted but not expanded.
    fix_action: >
      Flag in props.md that Table prop list is example-inferred; add a note
      that consumers should check @8x8/oxygen-data-table TypeScript types for
      the complete interface. Low priority — the docs are usable as-is.
    blocks: []
    dependency: []

  - id: GAP-005
    dimension: examples
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: true
    evidence:
      source_file: examples.md
      location: "All code blocks — no import statements present"
      finding: >
        No import statements are included in any of the 8 examples. Readers
        cannot determine which symbols to import or from which package entry point.
    fix_action: >
      Add an import block at the top of each example (or a shared imports
      section at the top of examples.md) showing: import { Table, TableContainer,
      TableHeader, HeaderCell, Pagination, useTable, useDataRetrieval,
      columnHelper, ... } from '@8x8/oxygen-data-table'.
    blocks: []
    dependency: []

  - id: GAP-006
    dimension: examples
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: examples.md
      location: "Multiple examples use createPersonColumns() — e.g. paginated example line 109"
      finding: >
        createPersonColumns() is used in paginated, sorted, filtered, and row-actions
        examples but never defined. Readers who copy examples cannot run them.
    fix_action: >
      Add a `createPersonColumns` reference implementation in examples.md
      (or note it is a user-defined helper) so examples are self-contained.
    blocks: []
    dependency: []

  - id: GAP-007
    dimension: tokens
    severity: major
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: true
    evidence:
      source_file: DataTable-figma.md
      location: "## Color & token bindings, lines 266–284"
      finding: >
        Six cell-level color tokens are documented in DataTable-figma.md
        (--ui/ui06, --ui/ui01, --text/textcolor01, --text/textcolor02,
        --error/error01) with light-mode values and two typography tokens
        (typography/body01, typography/label01), but none of these appear
        in tokens.md. tokens.md only contains global active/focus tokens.
    fix_action: >
      Add a "Cell tokens" section to tokens.md cross-referencing the
      tokens from DataTable-figma.md: background (--ui/ui06), border
      (--ui/ui01), primary text (--text/textcolor01), secondary text
      (--text/textcolor02), status bar (--error/error01), and the two
      typography tokens. doc-rewrite can merge these automatically.
    blocks:
      - doc-rewrite
    dependency: []

  - id: GAP-008
    dimension: tokens
    severity: major
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: DataTable-figma.md
      location: "## Color & token bindings — Dark value column shows <!-- NOT FOUND -->"
      finding: >
        Dark mode values for all cell-level tokens are not resolved.
        The Figma Variables API returned empty results; the UI-Foundations
        library (iVY5nI8JAxM05Apnnvozzs) could not be queried via figma_get_variables.
        Only light-mode fallback hex values are available.
    fix_action: >
      Re-run figma-extract after obtaining Figma Enterprise plan access
      or use figma_execute to query the UI-Foundations library variables
      directly via the plugin console. Alternatively, resolve manually
      by inspecting the dark-mode variant of the table cell in Figma.
    blocks:
      - doc-rewrite
      - storybook
    dependency: []

  - id: GAP-009
    dimension: tokens
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: tokens.md
      location: "## Notes section, line 49"
      finding: >
        The zebra prop alternates row backgrounds using an internal token
        not exposed via the Oxygen token API. The token name is unknown
        and cannot be documented without Figma Variables API access or
        source inspection.
    fix_action: >
      Inspect the dataTable package source for the zebra background token
      reference, or query the Figma table cell component in dark/zebra
      mode to identify the variable binding.
    blocks: []
    dependency: [GAP-008]

  - id: GAP-010
    dimension: tokens
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: DataTable-figma.md
      location: "## Gaps & conflicts — compact row height row"
      finding: >
        The isCompact?=yes row height is not documented. The compact cell
        height value was not captured in get_design_context (which only
        returned the default 64px height).
    fix_action: >
      Inspect the Figma table cell component set for isCompact?=yes
      variant dimensions, or query the source code for the compact height value.
    blocks: []
    dependency: []

  - id: GAP-011
    dimension: figma
    severity: major
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: DataTable-figma.md
      location: "## Design decisions & annotations — <!-- NO ANNOTATIONS FOUND -->"
      finding: >
        All 10 Figma component set description fields returned null despite
        the Desktop Bridge plugin being active. No design intent, rationale,
        or usage constraints are captured from Figma.
    fix_action: >
      Request that the design team adds component descriptions in Figma
      (component Properties panel → Description field) for the core
      component sets: table cell, table header, table action header,
      table footer.
    blocks:
      - doc-rewrite
    dependency: []

  - id: GAP-012
    dimension: figma
    severity: major
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: DataTable-figma.md
      location: "## Accessibility (from Figma annotations only) — all <!-- NOT ANNOTATED -->"
      finding: >
        No accessibility annotations exist on any Figma component set:
        ARIA role, focus order, and keyboard interactions are all absent.
    fix_action: >
      Request designer adds accessibility annotations to the Figma component
      sets (at minimum: table cell, table header, table action header).
    blocks:
      - doc-rewrite
    dependency: []

  - id: GAP-013
    dimension: figma
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: DataTable-figma.md
      location: "## Anatomy — table collapsible row slot (55222:11958)"
      finding: >
        The table collapsible row slot component set has only its variant
        axis (mode) documented. Internal anatomy, boolean toggles, and
        spacing were not retrieved.
    fix_action: >
      Run figma_get_component with enrich=true on node 55222:11958
      and append findings to DataTable-figma.md anatomy section.
    blocks: []
    dependency: []

  - id: GAP-014
    dimension: figma
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: DataTable-figma.md
      location: "## Anatomy — table row hover (51615:26100)"
      finding: >
        The table row hover component set has only top-level properties
        documented. Internal anatomy (hover overlay layer structure,
        button positions) was not retrieved.
    fix_action: >
      Run figma_get_component with format=reconstruction on node
      51615:26100 to retrieve internal anatomy.
    blocks: []
    dependency: []

  - id: GAP-015
    dimension: accessibility
    severity: minor
    type: DOC_GAP
    confidence: heuristic
    auto_fixable: false
    evidence:
      source_file: accessibility.md
      location: "## Keyboard interactions — Arrow keys row"
      finding: >
        Virtual scrolling screen reader behavior is undocumented. When
        enableVirtualization=true, only rendered rows exist in the DOM —
        screen readers may not be able to navigate to off-screen rows
        without additional ARIA live region or virtualizer configuration.
    fix_action: >
      Add a "Virtualization and screen readers" section to accessibility.md
      documenting whether the virtualization implementation provides
      aria-rowcount/aria-rowindex on the table element, and whether
      off-screen rows are accessible.
    blocks: []
    dependency: []

  - id: GAP-016
    dimension: accessibility
    severity: minor
    type: DOC_GAP
    confidence: heuristic
    auto_fixable: false
    evidence:
      source_file: accessibility.md
      location: "## WCAG 2.1 AA checklist — 4.1.3 Status Messages row"
      finding: >
        Live region behavior for dynamic data updates (new rows loaded,
        filter results changed, sort applied) is not documented. Tables
        with server-side data fetching typically require aria-live
        announcements for result count changes.
    fix_action: >
      Document whether useDataRetrieval triggers any live region updates
      when data changes, and recommend wrapping totalResultsMessage in
      an aria-live="polite" region if not already present.
    blocks: []
    dependency: []

  - id: GAP-017
    dimension: usage
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    status: "partially mitigated 2026-05-12 — DataTable-usage.md authored editorially in derivation-only mode"
    evidence:
      source_file: DataTable-usage.md
      location: "Frontmatter pipeline_note + HTML comments at top of file"
      finding: >
        The Figma ↳ Table examples page (53919:26449) exists and contains
        Table examples, Table sorting, Table structure, and Notes for future
        work sections, but no ✅ Do / ❌ Don't frames have been created. The
        published Oxygen docs page at /components/table/usage shows an
        "In progress" placeholder (fetched 2026-05-12, last updated
        4/10/2026 on the docs site). DataTable-usage.md was authored on
        2026-05-12 in derivation-only mode from props.md, examples.md,
        tokens.md, accessibility.md, and DataTable-figma.md; it contains 7
        Do/Don't pairs but is not grounded in authoritative design or
        published-docs sources.
    fix_action: >
      Either (a) request the design team populates the ↳ Table examples
      Figma page with Do/Don't usage cards and re-run figma-extract-usage,
      or (b) replace the editorial draft once the published Oxygen Table
      docs page exits its "In progress" state. Both paths supersede the
      current derivation-only draft.
    blocks: []
    dependency: []

  - id: GAP-018
    dimension: pui
    severity: minor
    type: SOURCE_GAP
    confidence: heuristic
    auto_fixable: false
    evidence:
      source_file: "(file absent)"
      location: "component-lib/DataTable/DataTable-pui.md — does not exist"
      finding: >
        DataTable-pui.md has not been produced. DataTable is primarily a
        data-display component; application-layer concerns (navigation,
        notifications, session) are unlikely but not confirmed. The
        useDataRetrieval hook connects to backend APIs which may have
        PUI-level error handling conventions.
    fix_action: >
      Run pui-mcp-extract for DataTable to confirm whether any PUI
      infrastructure context is relevant. If the verdict is "no PUI
      concerns", add <!-- NO RELEVANT PUI CONTEXT --> to close this gap.
    blocks: []
    dependency: []

warnings:
  - id: WARN-001
    dimension: props
    confidence: heuristic
    finding: >
      Table props sourced from example code rather than MCP may be incomplete.
      The MCP returned only 2 props (children, zebra) while 9 additional props
      are inferred from Storybook example code. If the component has additional
      props not present in the 31 Storybook stories, they will be absent from docs.
    advisory: >
      Consider cross-referencing with the package TypeScript types
      (@8x8/oxygen-data-table) to validate completeness.

  - id: WARN-002
    dimension: tokens
    confidence: heuristic
    finding: >
      tokens.md documents 4 global semantic tokens (active08, active10, focus01,
      focus02) while DataTable-figma.md surfaces 5 additional component-specific
      tokens. The disconnect suggests tokens.md was not updated after figma-extract
      completed.
    advisory: >
      After GAP-007 is resolved (merging cell tokens into tokens.md),
      verify that all tokens are referenced by the correct component
      element in the merged spec.
# --- navigation (added by component-map) ---
role: audit
pipeline_stage: blocked
pipeline_note: "Audit verdict NO — resolve CONFLICTs before rewrite"
siblings:
  - "[[DataTable/props]]"
  - "[[DataTable/examples]]"
  - "[[DataTable/tokens]]"
  - "[[DataTable/accessibility]]"
  - "[[DataTable/DataTable-figma]]"
tags:
  - oxygen
  - component/DataTable
  - role/audit
  - stage/blocked
---

# DataTable — Audit Report

> **Verdict: NO** — 2 unresolved CONFLICTs must be resolved before `doc-rewrite` can proceed.
>
> See also: [props.md](./props.md) · [examples.md](./examples.md) · [tokens.md](./tokens.md) · [accessibility.md](./accessibility.md) · [DataTable-figma.md](./DataTable-figma.md)

---

## File inventory

| File | Status | Severity if absent |
|------|--------|--------------------|
| `props.md` | ✅ Present | blocker |
| `examples.md` | ✅ Present | blocker |
| `tokens.md` | ✅ Present | major |
| `accessibility.md` | ✅ Present | blocker |
| `DataTable-figma.md` | ✅ Present | blocker |
| `DataTable-usage.md` | ✅ Present (editorial, 2026-05-12) | major |
| `DataTable-pui.md` | ❌ Missing | minor |

---

## Dimension scores

| Dimension | Score | Gaps |
|-----------|-------|------|
| props | 0.70 | GAP-001 (CONFLICT), GAP-003 (major), GAP-004 (minor) |
| examples | 0.85 | GAP-005 (minor), GAP-006 (minor) |
| tokens | 0.45 | GAP-007 (major DOC_GAP), GAP-008 (major SOURCE_GAP), GAP-009 (minor), GAP-010 (minor) |
| accessibility | 0.80 | GAP-015 (minor), GAP-016 (minor) |
| figma | 0.60 | GAP-002 (CONFLICT), GAP-011 (major), GAP-012 (major), GAP-013 (minor), GAP-014 (minor) |
| usage | 0.80 | GAP-017 (minor SOURCE_GAP — editorial derivation; upstream Figma cards + published docs still absent) |
| pui | — | GAP-018 (minor SOURCE_GAP — needs assessment) |

---

## Conflicts (must resolve before rewrite)

### GAP-001 — Pagination API discrepancy · CONFLICT · props

**Evidence:** `props.md` documents two incompatible Pagination interfaces simultaneously:
- MCP-returned props: `canGoBack`, `canGoNext`, `numberOfPages`, `pageNumber`, `rowsPerPage`
- Example-observed props: `limit`, `offset`, `totalResults`, `loadingData`

**Fix:** Determine the canonical public API and whether `usePagination()` is a required adapter or an optional convenience. Update props.md to a single interface.

---

### GAP-002 — Figma cell types vs. Oxygen cell components · CONFLICT · figma

**Evidence:** `DataTable-figma.md` documents a single `table cell` component set with 18 `type` variants. Oxygen code uses separate named components (`TextCell`, `PrimaryTextCell`, `CheckboxCell`, etc.) — no `type` prop exists on `<Cell>`.

**Fix:** Create an explicit Figma type → Oxygen component mapping table. Confirm with design whether all 18 Figma types have code counterparts.

---

## Major gaps

| ID | Dimension | Type | Description |
|----|-----------|------|-------------|
| GAP-003 | props | DOC_GAP | TextCell, PrimaryTextCell, SecondaryTextCell props undocumented |
| GAP-007 | tokens | DOC_GAP | Cell-level tokens from figma.md not in tokens.md |
| GAP-008 | tokens | SOURCE_GAP | Dark mode token values not resolved (Variables API unavailable) |
| GAP-011 | figma | SOURCE_GAP | All Figma component set descriptions null |
| GAP-012 | figma | SOURCE_GAP | No accessibility annotations in Figma |

---

## Minor gaps

| ID | Dimension | Type | Description |
|----|-----------|------|-------------|
| GAP-004 | props | DOC_GAP | Table props beyond children/zebra are example-inferred, not MCP-confirmed |
| GAP-005 | examples | DOC_GAP | No import statements in any example |
| GAP-006 | examples | DOC_GAP | createPersonColumns() helper undefined |
| GAP-009 | tokens | SOURCE_GAP | Zebra stripe token unknown |
| GAP-010 | tokens | SOURCE_GAP | isCompact row height not captured |
| GAP-013 | figma | SOURCE_GAP | table collapsible row slot anatomy incomplete |
| GAP-014 | figma | SOURCE_GAP | table row hover internal anatomy incomplete |
| GAP-015 | accessibility | DOC_GAP | Virtual scrolling screen reader behavior undocumented |
| GAP-016 | accessibility | DOC_GAP | Live region behavior for data updates undocumented |
| GAP-017 | usage | SOURCE_GAP | Usage doc is editorial derivation (2026-05-12); upstream Figma Do/Don't cards + published Oxygen docs page still absent |
| GAP-018 | pui | SOURCE_GAP | PUI relevance unconfirmed |

---

## Warnings (heuristic — advisory only)

**WARN-001 (props):** Table prop list may be incomplete — only 2 props confirmed by MCP, 9 inferred from examples. Cross-reference with TypeScript types.

**WARN-002 (tokens):** tokens.md and DataTable-figma.md token sets are not aligned. After GAP-007 is resolved, verify cross-references in the merged spec.

---

## Recommended resolution order

1. **Resolve GAP-001** (Pagination API) — confirm with engineering
2. **Resolve GAP-002** (cell type mapping) — confirm with design
3. **Fix GAP-003** (TextCell/PrimaryTextCell/SecondaryTextCell props) — re-run MCP extract for these components
4. **Fix GAP-007** (merge figma cell tokens into tokens.md) — doc-rewrite can do this automatically once conflicts are resolved
5. **Fix GAP-008** (dark mode tokens) — requires Figma Variables API access or manual inspection
6. **Request GAP-011/GAP-012** (Figma descriptions + a11y annotations) — designer action
7. **GAP-017** — partially mitigated 2026-05-12 by editorial `DataTable-usage.md`. Replace once a Figma `↳ DataTable examples` page is populated with Do/Don't cards OR the published Oxygen Table docs page exits "In progress".
8. Remaining minor gaps can be addressed during doc-rewrite

---

_Initial audit: 2026-05-06 · Updated: 2026-05-12 (usage dimension scored after editorial DataTable-usage.md) · Rubric version 1.0_
