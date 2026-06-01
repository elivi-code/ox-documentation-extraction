# Accordion doc-rewrite Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Apply all 6 auto-fixable gaps to their source files and assemble `accordion-spec.md` — the canonical merged spec for the Accordion component.

**Architecture:** Pure file I/O — no MCP connections required. Audit verdict is YES with zero CONFLICTs. All source files are present (props, examples, tokens, accessibility, figma, usage). PUI file is absent and will be stubbed.

**Tech Stack:** Markdown file I/O only. Input: `component-lib/Accordion/{source}.md`. Output: `component-lib/Accordion/accordion-spec.md`.

---

## Gap partition

```
Rewrite plan for Accordion:
  Apply (auto-fixable DOC_GAPs):  6 changes across 4 source files
  Stub  (SOURCE_GAPs):            7 gaps stubbed in spec
  Skip  (manual DOC_GAPs):        4 gaps require human input

Proceeding with Apply + Stub. Manual gaps listed at end.
```

### Apply bucket — source file edits

| Gap | File | Change |
|-----|------|--------|
| GAP-005 | `props.md` | Add `divider?` Figma-only note |
| GAP-006 | `props.md` | Add `scrollbar?` / `isContentScrollable` clarification |
| GAP-009 | `examples.md` | Add dark mode / theming note |
| GAP-011 | `examples.md` | Add `forcedHeight` standalone example |
| GAP-016 | `accessibility.md` | Add `aria-controls` note to ARIA table |
| WARN-003 | `accordion-figma.md` | Add `isOpen?` → `isExpanded` mapping note |

### Stub bucket — SOURCE_GAPs in spec only

| Gap | Spec section | Stub marker |
|-----|-------------|-------------|
| GAP-001 | Usage guidelines | Editorial provenance note (file exists post-audit) |
| GAP-002 | Platform UI integration | `<!-- STUB:GAP-002 ... -->` |
| GAP-003 | Design tokens | Canonical names unverified note |
| GAP-012 | Accessibility | `translations` defaults unconfirmed |
| GAP-013 | Design decisions | No Figma ARIA annotations |
| GAP-014 | Design decisions | `_headerCustom` not extracted |
| GAP-015 | Design tokens | Token coverage % unavailable |

### Skip/manual bucket — human input required

| Gap | Reason |
|-----|--------|
| GAP-004 | `AIBadge?` code prop behavior unknown — needs component owner confirmation |
| GAP-007 | Spacing values (16px, 48px…) not known to be token-bound or hardcoded |
| GAP-008 | Scrollbar thumb `#858585` dark — design must confirm token or hardcoded intent |
| GAP-010 | Disabled example depends on GAP-004 (unresolved) — cannot derive safely |

---

## File structure

| File | Action | Gaps addressed |
|------|--------|----------------|
| `component-lib/Accordion/props.md` | Modify | GAP-005, GAP-006 |
| `component-lib/Accordion/examples.md` | Modify | GAP-009, GAP-011 |
| `component-lib/Accordion/accessibility.md` | Modify | GAP-016 |
| `component-lib/Accordion/accordion-figma.md` | Modify | WARN-003 |
| `component-lib/Accordion/accordion-spec.md` | Create | Assembled from all source files |

---

## Task 1 — Apply GAP-005 + GAP-006 to props.md

**Files:**
- Modify: `component-lib/Accordion/props.md`

- [ ] **Step 1: Read props.md**

  Read current content. Confirm the `Accordion` props table ends at line ~82 and includes `isExpanded`, `forcedHeight`, `isContentScrollable`.

- [ ] **Step 2: Apply GAP-005 — add divider? Figma-only note**

  After the `Accordion` props table (after the `shouldCloseOnActiveClick` row, before the `---` separator that precedes `AccordionGroup`), insert:

  ```markdown
  > **Figma-only:** The Figma component exposes a `divider?` boolean toggle (default: `true`) that shows a 1px separator below the accordion row. There is no corresponding code prop — the divider is always rendered in the DOM. Use CSS overrides to suppress it if needed.
  ```

  Location: after line 82 (`| shouldCloseOnActiveClick | ... |`) and before the `---` that opens the AccordionGroup section.

- [ ] **Step 3: Apply GAP-006 — add scrollbar? / isContentScrollable clarification**

  After the `isContentScrollable` row in the Accordion props table, insert a blockquote note. The `isContentScrollable` row is at approximately line 78. Insert _after_ that row:

  ```markdown
  > **Figma vs code:** The Figma component has a `scrollbar?` boolean toggle (default: `false`) that renders a Mac OS–style scrollbar overlay. In code, scroll behaviour is governed by `isContentScrollable` and `forcedHeight` — there is no separate scrollbar prop. The browser's native scrollbar renders automatically when content overflows a fixed height.
  ```

  Location: inside the table the note will look odd — instead insert it as a standalone blockquote immediately after the props table and before the GAP-005 divider note. So the order after the Accordion table is:
  1. GAP-005 divider? note
  2. GAP-006 scrollbar? note
  3. `---` separator before AccordionGroup

- [ ] **Step 4: Write the updated props.md**

  Confirm the file has more lines than the original (additions only, no deletions). Write it back.

---

## Task 2 — Apply GAP-009 + GAP-011 to examples.md

**Files:**
- Modify: `component-lib/Accordion/examples.md`

- [ ] **Step 1: Read examples.md**

  Read current content. Confirm it has 8 examples, ending at the `Blocking navigation` example (~line 205). The `_Source` line is the last line.

- [ ] **Step 2: Apply GAP-009 — add dark mode / theming note**

  Insert a new section before the `_Source` line:

  ```markdown
  ## Dark mode and theming

  Dark mode is controlled via CSS custom properties, not a component prop. The Accordion component reads design tokens (`--ui/ui06`, `--text/textcolor01`, etc.) that automatically resolve to dark values when the `.oxygen-dark` class (or equivalent Oxygen theme class) is applied to a parent element.

  There is no `mode` or `theme` prop on `Accordion` or `AccordionGroup`. Apply theming at the application level.

  > For token resolved values in light and dark modes see [tokens.md](./tokens.md) and [accordion-figma.md](./accordion-figma.md#color--token-bindings).
  ```

- [ ] **Step 3: Apply GAP-011 — add forcedHeight standalone example**

  Insert a new section immediately after the `Fixed-height group` example and before `Nested accordion`:

  ```markdown
  ## Forced height on a standalone accordion

  `forcedHeight` constrains a single `Accordion`'s content to a fixed pixel height, independently of `AccordionGroup.hasFixedHeight`. Combine with `isContentScrollable={true}` to allow the user to scroll the clamped content.

  ```tsx
  <Accordion
    title="Long content section"
    forcedHeight={200}
    isContentScrollable={true}
  >
    <p>Line 1</p>
    <p>Line 2</p>
    {/* … many lines … */}
    <p>Line N</p>
  </Accordion>
  ```

  > **Difference from `AccordionGroup hasFixedHeight`:** `hasFixedHeight` makes the group fill its parent container and limits the group to one open accordion at a time. `forcedHeight` on a standalone `Accordion` sets an absolute pixel cap on that accordion's content area only — multiple accordions in the same group can be open simultaneously.
  ```

- [ ] **Step 4: Write the updated examples.md**

  Confirm line count is higher than original. Write it back.

---

## Task 3 — Apply GAP-016 to accessibility.md

**Files:**
- Modify: `component-lib/Accordion/accessibility.md`

- [ ] **Step 1: Read accessibility.md**

  Read current content. Confirm the ARIA roles table is at lines ~38–46. It ends with `| Disabled accordion | aria-disabled="true" | ... |`.

- [ ] **Step 2: Apply GAP-016 — add aria-controls note**

  Add a new row at the end of the ARIA roles and attributes table:

  ```markdown
  | Accordion header | `aria-controls` | WAI-ARIA APG Accordion pattern recommends `aria-controls` pointing to the panel ID. Implementation not confirmed from component source — verify before publishing. |
  ```

  The updated table will look like:

  ```markdown
  | Element | Role / Attribute | Notes |
  |---------|-----------------|-------|
  | Accordion header | `<button>` | The header is rendered as a native button element |
  | Collapsed state | `aria-expanded="false"` | Set on the header button |
  | Expanded state | `aria-expanded="true"` | Set on the header button |
  | Content panel | `role="region"` | The expanded content area |
  | Content panel | `aria-labelledby` | Should reference the header button's ID |
  | Disabled accordion | `aria-disabled="true"` | Matches the Figma `disabled` state |
  | Accordion header | `aria-controls` | WAI-ARIA APG Accordion pattern recommends `aria-controls` pointing to the panel ID. Implementation not confirmed from component source — verify before publishing. |
  ```

- [ ] **Step 3: Write the updated accessibility.md**

  Confirm no lines were removed. Write it back.

---

## Task 4 — Apply WARN-003 to accordion-figma.md

**Files:**
- Modify: `component-lib/Accordion/accordion-figma.md`

- [ ] **Step 1: Read accordion-figma.md**

  Read current content. Confirm the Accordion variant axes table is at lines ~78–81 with properties `mode` and `isOpen?`.

- [ ] **Step 2: Apply WARN-003 — add isOpen? → isExpanded mapping note**

  Immediately after the `### Accordion variant axes` table (after the `| isOpen? | true, false | false |` row), insert:

  ```markdown
  > **Code mapping:** Figma `isOpen?` corresponds to the code prop `isExpanded` on `<Accordion>`. Figma property names rarely match code prop names exactly; this is the only renamed axis on this component.
  ```

- [ ] **Step 3: Write the updated accordion-figma.md**

  Confirm no lines were removed. Write it back.

---

## Task 5 — Assemble accordion-spec.md

**Files:**
- Read: all `component-lib/Accordion/` files (post-fix versions)
- Create: `component-lib/Accordion/accordion-spec.md`

- [ ] **Step 1: Compose YAML frontmatter**

  ```yaml
  ---
  component: Accordion
  package: "@8x8/oxygen-accordion"
  category: layout_overlay
  role: spec
  role_description: "Canonical component spec — merged output of doc-rewrite; source of truth for docusaurus + storybook"
  pipeline_stage: spec_complete
  pipeline_note: "Canonical spec written — pipeline complete"
  audit_verdict: YES
  rubric_version: "1.0"
  spec_produced: "2026-05-19"
  siblings:
    - "[[Accordion/props]]"
    - "[[Accordion/examples]]"
    - "[[Accordion/tokens]]"
    - "[[Accordion/accessibility]]"
    - "[[Accordion/accordion-figma]]"
    - "[[Accordion/accordion-audit]]"
  tags:
    - oxygen
    - component/Accordion
    - role/spec
    - stage/spec_complete
    - category/layout_overlay
  ---
  ```

- [ ] **Step 2: Write the Overview section**

  Source: `props.md` intro + `accordion-figma.md` description + `accordion-usage.md` overview.

  ```markdown
  # Accordion — Component Spec

  > **Status:** Under review
  > **Package:** `@8x8/oxygen-accordion`
  > **Category:** Layout overlay
  > **Figma file:** `5YihJ5WuDvnvrlrRMC4sBp` ([UI components](https://www.figma.com/design/5YihJ5WuDvnvrlrRMC4sBp/UI-components)) · node `44417:100356`
  > **Extracted:** 2026-04-28
  > **Spec produced by:** doc-rewrite · Rubric v1.0 · 2026-05-19

  ---

  ## Overview

  An Accordion is a vertically stacked set of panels. Each panel has a header that toggles the visibility of its content area. Use accordions to reduce clutter when content is long or when users need to see only one section at a time.

  Key behaviours:
  - The entire header row (default) or only the chevron icon (`expandTrigger="arrow"`) triggers expand/collapse
  - Accordions can be grouped via `AccordionGroup` for shared state management
  - `AccordionGroup hasFixedHeight` enables single-open mode with the active panel filling the remaining container height
  - Maximum nesting depth is **two levels**

  ### Installation

  ```sh
  # yarn
  yarn add @8x8/oxygen-accordion

  # npm
  npm install @8x8/oxygen-accordion
  ```

  **Registry configuration required (8x8 VPN):**

  ```ini
  # .npmrc
  @8x8:registry=https://artifactory.es.8x8.com/artifactory/api/npm/npm-repository/
  ```

  ```yaml
  # .yarnrc.yml
  npmScopes:
    8x8:
      npmRegistryServer: "https://artifactory.es.8x8.com/artifactory/api/npm/npm-repository/"
  nodeLinker: node-modules
  ```
  ```

- [ ] **Step 3: Write the Props section**

  Source: post-fix `props.md`. Merge verbatim: the `Accordion` props table, the GAP-005 divider note, the GAP-006 scrollbar note, the `AccordionGroup` props table, and the `Translations` type table.

  Add a manual-gap HTML comment after the `contentAfterTitle` prop row:

  ```markdown
  <!-- GAP-004 (manual): The Figma _header atom has an `AIBadge?` boolean (default: false) that renders a star icon + "AI" label after the title. No code prop is documented. Awaiting component owner confirmation of whether this is achievable via `contentAfterTitle` or is a planned prop. -->
  ```

- [ ] **Step 4: Write the Design Tokens section**

  Source: `tokens.md` (full content verbatim). Add at top of section:

  ```markdown
  > <!-- STUB:GAP-003 source="Re-run get-theme-tokens with broader search terms to confirm canonical names; token names currently use Figma CSS variable syntax (--ui/ui06) which may differ from the @8x8/oxygen-tokens registry" -->
  > **Note (GAP-003):** All token names below are sourced from Figma design inspection, not the Oxygen token registry. The canonical JavaScript token paths (e.g. from `@8x8/oxygen-tokens`) may differ. Cross-reference before using in implementation.
  ```

  Then include:
  - Color tokens table (from tokens.md)
  - Typography tokens table (from tokens.md)
  - Figma variant matrix (from tokens.md)
  - Spacing note:

  ```markdown
  ### Spacing

  <!-- GAP-007 (manual): Spacing values below are raw pixel values from Figma structure. It is unknown whether they are bound to Oxygen spacing tokens or hardcoded. Component owner confirmation needed. -->

  | Property | Value | Notes |
  |----------|-------|-------|
  | Header height | `48px` | Fixed |
  | Header padding horizontal | `16px` | |
  | Header padding vertical | `14px` | |
  | Content padding top | `8px` | |
  | Content padding bottom/horizontal | `16px` | |
  | Icon → content → arrow gap | `12px` | |
  | Title → AI badge gap | `4px` | |
  | Icon size | `20px` | Leading icon and chevron |
  | Focus ring | `2px solid` | `--interactive/focus01` |
  ```

- [ ] **Step 5: Write the Examples section**

  Source: post-fix `examples.md`. Include verbatim all examples (now 9 after additions):
  1. Basic group
  2. Controlled expansion
  3. With secondary text and leading icon
  4. Custom trigger mode — `expandTrigger="arrow"`
  5. Fixed-height group (one open at a time)
  6. Forced height on a standalone accordion *(new — GAP-011)*
  7. Nested accordion (max 2 levels)
  8. Without padding in content area
  9. Custom translations (i18n)
  10. Blocking navigation from `AccordionGroup.onChange`
  11. Dark mode and theming *(new — GAP-009)*

  Add at top of section:

  ```markdown
  > **WARN-001:** All examples are derived from prop documentation, usage guidelines, and Figma annotations. The Oxygen MCP returned 0 clean Storybook examples. Import paths (e.g. `@8x8/oxygen-icons`, `@8x8/oxygen-icon-button`) have not been verified against a running Storybook. Validate before publishing to Docusaurus.
  ```

- [ ] **Step 6: Write the Usage Guidelines section**

  Source: `accordion-usage.md` (full content verbatim). Add provenance note at top:

  ```markdown
  <!-- GAP-001 (partial): accordion-usage.md was authored editorially (2026-05-11) from oxygen.8x8.com/components/accordion/usage + Oxygen MCP. Three Do/Don't pairs are derived from the Best Practices section, not Figma-sourced. When the designer adds ✅ Do / ❌ Don't frames to Figma examples page 79430:614, re-run figma-extract-usage to replace with Figma-sourced pairs. -->
  ```

  Then include the full usage file content: Anatomy, Overview, Behavior, Best practices, Expand/Collapse all, When to use/not use, Do/Don't pairs, Related.

- [ ] **Step 7: Write the Design Decisions section**

  Source: `accordion-figma.md`. Include verbatim:
  - Visual reference (screenshot link)
  - Anatomy tables (Accordion container + _header atom)
  - API / Component properties (all variant axes + boolean toggles + instance swap slots)
  - The WARN-003 code mapping note (now applied in source file)
  - Color & token bindings table
  - Structure & spacing tables
  - Interaction states table
  - Component variants table
  - Figma examples page annotations

  Add stubs for SOURCE_GAPs:

  ```markdown
  <!-- STUB:GAP-014 source="Run figma_get_component on node 82572:13829 (_headerCustom) to extract its component properties; confirm whether contentAfterTitle slot maps to this Figma atom" -->
  > **GAP-014:** `_headerCustom` (node `82572:13829`) properties were not separately extracted. It mirrors `_header` with an additional icon button slot. See audit for details.

  <!-- STUB:GAP-015 source="Run figma_get_component with enrich=true via Desktop Bridge to obtain authoritative token coverage %" -->
  > **GAP-015:** Token coverage % not returned by `figma_get_component enrich` (REST API limitation without Desktop Bridge). Token values manually assessed as fully tokenised.
  ```

- [ ] **Step 8: Write the Accessibility section**

  Source: post-fix `accessibility.md`. Include verbatim all content including the new `aria-controls` row.

  Add STUB for GAP-012:

  ```markdown
  <!-- STUB:GAP-012 source="Check @8x8/oxygen-accordion source or Storybook for default translation strings for expand/collapse aria-labels; add default values to the Translations type table in props.md" -->
  > **GAP-012:** Default values for the `translations` prop (expand/collapse aria-labels) are not confirmed. The Oxygen MCP did not return them. Check component source or Storybook before publishing.
  ```

  Add STUB for GAP-013:

  ```markdown
  <!-- STUB:GAP-013 source="Designer should add ARIA role, focus order, and keyboard interaction annotations to the Figma Accordion component; engineering should confirm aria-expanded, role=region, aria-labelledby implementation" -->
  ```

- [ ] **Step 9: Write the Platform UI Integration section**

  ```markdown
  ## Platform UI Integration

  <!-- STUB:GAP-002 source="Run pui-mcp-extract for Accordion. If Platform UI has no equivalent component or hooks, create accordion-pui.md with <!-- NO RELEVANT PUI CONTEXT --> marker" -->

  > Platform UI integration data is not yet available. Run `pui-mcp-extract Accordion` to determine whether Platform UI exposes an Accordion wrapper, related hooks, or event bus integrations. If no PUI context exists, this section will be marked N/A.
  ```

- [ ] **Step 10: Write the spec file**

  Write all sections assembled above to `component-lib/Accordion/accordion-spec.md`. Confirm the file is non-empty and materially longer than any individual source file.

---

## Task 6 — Update pipeline-status.md and components-to-extract.md

**Files:**
- Modify: `pipeline-status.md`
- Modify: `components-to-extract.md`

- [ ] **Step 1: Update pipeline-status.md**

  Move Accordion from the `🟢 SPEC READY` table to the `✅ SPEC COMPLETE` table:

  New row for SPEC COMPLETE table:
  ```markdown
  | [[component-lib/Accordion/Accordion|Accordion]] | layout overlay | 🟢 YES | 0.73 | Spec written 2026-05-19. 6 auto-fixable gaps applied. 7 SOURCE_GAPs stubbed. 4 manual gaps open (GAP-004, GAP-007, GAP-008, GAP-010). |
  ```

  Remove the Accordion row from `🟢 SPEC READY`.

  Update the Summary counts:
  - `✅ SPEC COMPLETE`: 1 → 2
  - `🟢 SPEC READY`: 17 → 16

- [ ] **Step 2: Update components-to-extract.md**

  Find the Accordion row and strike it through:
  Change `| Accordion |` → `| ~~Accordion~~ |`

  Do NOT bump the Progress counter — the instructions say to bump it after extract + audit, not after rewrite. Accordion was already counted.

  > **Check first:** Verify whether the Accordion row is already struck through before editing.

---

## Completion summary template

```
doc-rewrite complete — Accordion

Gaps applied:      6  (DOC_GAPs fixed in source files)
Stubs inserted:    7  (SOURCE_GAPs — upstream work needed)
Skipped (manual):  4  (DOC_GAPs requiring human input)

Source files modified:
  - props.md          (GAP-005, GAP-006)
  - examples.md       (GAP-009, GAP-011)
  - accessibility.md  (GAP-016)
  - accordion-figma.md (WARN-003)

Spec written:
  component-lib/Accordion/accordion-spec.md

Manual gaps still open:
  GAP-004 · major · figma_alignment — AIBadge? code prop unknown; needs component owner
  GAP-007 · minor · token_coverage  — Spacing pixel values not confirmed as token-bound
  GAP-008 · minor · token_coverage  — Scrollbar thumb #858585 dark; token vs hardcoded TBD
  GAP-010 · minor · examples_coverage — Disabled example blocked by GAP-004

Stubs in spec (SOURCE_GAPs):
  GAP-001 · major · usage_guidelines — editorial usage.md; replace when Figma adds Do/Don't frames
  GAP-002 · major · pui_integration  — run pui-mcp-extract Accordion
  GAP-003 · major · token_coverage   — token names unverified against @8x8/oxygen-tokens registry
  GAP-012 · minor · accessibility    — translations prop defaults unconfirmed
  GAP-013 · minor · accessibility    — no ARIA annotations in Figma
  GAP-014 · minor · figma_alignment  — _headerCustom properties not extracted
  GAP-015 · minor · token_coverage   — token coverage % requires Desktop Bridge

Suggested next action:
  → Resolve GAP-002 (run pui-mcp-extract Accordion) — easiest remaining gap
  → Resolve GAP-004 (ask component owner about AIBadge?) — unblocks GAP-010
  → When stubs are resolved, re-run doc-audit + doc-rewrite to refresh the spec
```
