---
parent: "[[Breadcrumbs]]"
section: usage
---

<!-- STUB:GAP-012 source="If a Figma '↳ Breadcrumbs examples' page is ever created with Do/Don't card frames, run figma-extract-usage for Breadcrumbs and replace this content with its output. Until then, the editorial guidance is canonical." -->
> **Editorial provenance (GAP-012):** No Figma `↳ Breadcrumbs examples` page exists, so `figma-extract-usage` could not run. The guidance below is **editorial** — transcribed from the published Oxygen docs page (screenshot, 2026-05-11) and cross-validated against [[Breadcrumbs.props]], [[Breadcrumbs.anatomy]], [[Breadcrumbs.accessibility]], and the source examples. Quality is high; provenance is editorial, not designer-authored Figma frames.

## Overview

Breadcrumbs are a **secondary** navigational system showing the user's location within a hierarchical site structure. The trail starts at Home (or the highest-level parent) and ends at the parent of the current page; the current page itself is **never a link**.

## Placement

Place breadcrumbs in the **top-left** of the page, **above the page title**, on a **single line**. If the trail is too long for the available width, collapse it with the overflow menu — never let it wrap to a second line.

## Overflow menu

When a trail grows long (the published docs reference an eight-item threshold) or space is limited, the component auto-collapses and shows an ellipsis (`…`). The first and last items remain visible by default; clicking the ellipsis opens an overflow menu of the truncated items. Collapse behaviour is controlled by `maxItems`, `itemsBeforeCollapse`, `itemsAfterCollapse`, and `collapsedTitle` — see [[Breadcrumbs.props]].

## When to use

- To help users understand and move between the multiple levels of a hierarchical website — especially when they land deep in the hierarchy from search or an external link.

## When not to use

| Situation | Why | Use instead |
|-----------|-----|-------------|
| Flat site (no nested hierarchy) | Nothing for a trail to represent — adds noise. | Primary nav alone. |
| Progress through a linear journey (wizard / multi-step form) | Breadcrumbs reflect location in a hierarchy, not stages in a flow. | Progress indicator / stepper. |
| Hierarchy already exposed elsewhere (e.g. persistent sidebar) | Breadcrumbs duplicate existing navigation. | Existing pattern; add breadcrumbs only if they add wayfinding value. |

## Do / Don't

### Do — Keep link labels short and reflective of the destination
Each page link should clearly identify the page it points to. Prefer the page's own title; avoid generic placeholders.

### Don't — Use vague, duplicated, or truncated labels
Generic labels ("Page", "Section") or mid-string ellipses defeat wayfinding. Let the component handle overflow instead of hand-truncating labels.

---

### Do — Make the current page the last, non-link item
Use `isActive` on the final `Breadcrumb`. It renders as plain text and carries `aria-current="page"`. See [[Breadcrumbs.accessibility]].

### Don't — Render the current page as a link
A self-referencing link is misleading, fails `aria-current` expectations, and contradicts the guidance that "this page is never a link".

---

### Do — Keep the trail on a single line, top-left, above the page title
Breadcrumbs sit above the page title, anchored left, on a single row.

### Don't — Let the trail wrap to a second line
If too long, collapse with the overflow menu. Wrapping breaks visual hierarchy and the component's auto-layout (`overflow: no wrap`).

---

### Do — Let the component auto-collapse beyond the threshold
Set `maxItems` to reflect your hierarchy depth and let the component render the ellipsis and overflow menu automatically.

### Don't — Hand-truncate or hand-omit middle items
Manually dropping items or shortening labels bypasses the accessible overflow `<button>` and hides destinations the user might need.

---

### Do — Localise `collapsedTitle` and `ariaLabel`
Both default to English strings. Translate them — the ellipsis `<button>` `title` and the `<nav>` `aria-label` are read aloud by screen readers.

### Don't — Ship the default English strings to a translated UI
Mixed-language ARIA text confuses screen-reader users and fails localisation review.

---

### Do — Use breadcrumbs to complement primary navigation for deep hierarchies
Most valuable when users arrive deep in a hierarchy and need to orient themselves and step back up.

### Don't — Use breadcrumbs on flat sites or as a progress tracker
No hierarchy → no trail to show. For step-by-step flows, use a progress indicator or stepper.

_Source: [[Breadcrumbs/Breadcrumbs-usage]] · Published Oxygen docs page (screenshot, 2026-05-11), cross-validated against MCP/Figma extraction · Editorial_
