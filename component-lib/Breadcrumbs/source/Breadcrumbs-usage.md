---
component: Breadcrumbs
package: "@8x8/oxygen-breadcrumbs"
category: navigation
role: usage
role_description: "Usage guidelines — editorial, compiled from the published Oxygen docs page and the extracted MCP/Figma artifacts"
pipeline_stage: editorial
pipeline_note: "Usage authored editorially from the published Oxygen docs page (screenshot) cross-referenced with extracted MCP/Figma artifacts — NOT from Figma Do/Don't card frames. Re-run doc-audit after creation; replace pairs with figma-extract-usage output when a Figma examples page exists."
source_type: editorial
audit_verdict: null
siblings:
  - "[[Breadcrumbs/props]]"
  - "[[Breadcrumbs/examples]]"
  - "[[Breadcrumbs/tokens]]"
  - "[[Breadcrumbs/accessibility]]"
  - "[[Breadcrumbs/Breadcrumbs-figma]]"
  - "[[Breadcrumbs/Breadcrumbs-pui]]"
  - "[[Breadcrumbs/Breadcrumbs-audit]]"
tags:
  - oxygen
  - component/Breadcrumbs
  - role/usage
  - stage/editorial
  - category/navigation
---
<!-- SOURCE: editorial — published Oxygen docs page (screenshot, 2026-05-11) + extracted MCP/Figma artifacts -->
<!-- FIGMA EXAMPLES PAGE: absent — figma-extract-usage cannot run for this component -->
<!-- GROUNDING: full — props.md, examples.md, accessibility.md, Breadcrumbs-figma.md, Breadcrumbs-audit.md, published docs screenshot -->
<!-- DRAFTED: 2026-05-11 -->
<!-- MODE: docs-mirrored -->
<!-- PAIRS: 6 -->
<!-- STATUS: editorial draft — replace with figma-extract-usage output when a Figma "↳ Breadcrumbs examples" page is created -->

# Breadcrumbs — Usage Guidelines

> **See also:** [props.md](./props.md) · [examples.md](./examples.md) · [tokens.md](./tokens.md) ·
> [accessibility.md](./accessibility.md) · [Breadcrumbs-figma.md](./Breadcrumbs-figma.md)

> **Editorial guidance — mirrors the published Oxygen docs page.** No `↳ Breadcrumbs examples` Figma page exists, so `figma-extract-usage` cannot run. The guidance below is transcribed from the published Oxygen docs page for Breadcrumbs (screenshot, 2026-05-11) and cross-validated against [props.md](./props.md), [examples.md](./examples.md), [accessibility.md](./accessibility.md), and [Breadcrumbs-figma.md](./Breadcrumbs-figma.md). Replace with `figma-extract-usage` output if a Figma examples page is ever created.

A breadcrumb is a navigation pattern that lets users navigate a nested path of pages within a hierarchical structure of a site.

---

## Anatomy

1. **Home link** — the first item in the trail. Points to the root of the site (or the highest-level parent).
2. **Page link** — intermediate, clickable trail items. One per hierarchy level between Home and the current page.
3. **Separator** — decorative glyph between items. Defaults to `/`; the `separator` prop accepts any `React.ReactNode`. See [props.md](./props.md).
4. **Current page** — the last item in the trail. Rendered as plain text, not a link, and carries `aria-current="page"`. See [accessibility.md](./accessibility.md).

---

## Overview

Breadcrumbs are a **secondary** navigational system: they show users their current location relative to the information architecture. Each page link should be short and clearly reflect the location or entity it links to so users understand where they are and can move between levels. The trail starts at the Home (or highest-level parent) page and ends at the parent section of the current page; the current page itself is **never a link**.

**Source:** Published docs — Overview section · [Breadcrumbs-figma.md:229](./Breadcrumbs-figma.md) (Figma component description).

---

## Behaviour

### States

Breadcrumb link items expose four interaction states:

| # | State | Trigger |
|---|-------|---------|
| 1 | Rest | Default. |
| 2 | Hover | Pointer over the link. |
| 3 | Active | Pointer pressed on the link. |
| 4 | Focus | Link receives keyboard focus (Tab order, [accessibility.md](./accessibility.md)). |

Visual styling for each state is defined in the Figma `_Text link breadcrumb` and `_Text link elipsis` atoms — see [Breadcrumbs-figma.md](./Breadcrumbs-figma.md). Only rest-state token bindings are currently resolved; hover/active/focus tokens remain a `SOURCE_GAP` per [Breadcrumbs-audit.md](./Breadcrumbs-audit.md) GAP-001.

**Source:** Published docs — Behaviour → States · [Breadcrumbs-figma.md](./Breadcrumbs-figma.md) · [accessibility.md](./accessibility.md).

---

## Placement

Breadcrumbs are placed in the **top-left** portion of the page, **above the page title**, and should **never wrap onto a second line**. If the trail is too long for the available width, collapse it with the overflow menu — do not allow the line to wrap.

**Source:** Published docs — Placement section · Figma auto-layout `overflow: no wrap` [Breadcrumbs-figma.md:205](./Breadcrumbs-figma.md).

---

## Overflow menu

When a breadcrumb contains **more than eight items**, or the space becomes limited, the breadcrumb auto-collapses and uses an ellipsis (`…`) to indicate more information. The **first and last items are shown by default**. Clicking the ellipsis opens an overflow menu showing the truncated breadcrumbs.

The collapse behaviour is controlled by these props (see [props.md:50](./props.md)):

| Prop                  | Default            | Purpose                                                                                                                                        |
| --------------------- | ------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------- |
| `maxItems`            | `4`                | Threshold above which the trail collapses. The published docs reference an eight-item threshold; override `maxItems` to align with that limit. |
| `itemsBeforeCollapse` | `1`                | How many items remain visible before the ellipsis.                                                                                             |
| `itemsAfterCollapse`  | `1`                | How many items remain visible after the ellipsis.                                                                                              |
| `collapsedTitle`      | `'Show all links'` | Accessible title on the ellipsis `<button>`.                                                                                                   |

See the collapsed-overflow code example in [examples.md](./examples.md).

**Source:** Published docs — Overflow menu section · [props.md:50](./props.md) · [examples.md](./examples.md).

---

## Best Practices

### When to use

- Use the breadcrumbs component to help users understand and move between the multiple levels of a website.

### When not to use

| Situation | Why | Use instead |
|-----------|-----|-------------|
| Product has a flat structure (no nested hierarchy) | Nothing for a trail to represent — adds noise. | Primary nav alone. |
| Showing progress through a linear journey (e.g. a wizard or multi-step form) | Breadcrumbs reflect location in a hierarchy, not stages in a flow. | Progress indicator / stepper. |
| The page already exposes the same hierarchy elsewhere (e.g. a persistent sidebar) | Breadcrumbs duplicate navigation the user already has. | Rely on the existing pattern; only add breadcrumbs if they genuinely add wayfinding value. |

**Source:** Published docs — Best Practices → When to use / When not to use.

---

## Do / Don't

### Do — Keep link labels short and reflective of the destination

Each page link should clearly identify the page or section it points to. Prefer the page's own title; avoid generic placeholders.

```tsx
<Breadcrumb href="/billing">Billing</Breadcrumb>
<Breadcrumb href="/billing/invoices">Invoices</Breadcrumb>
```

### Don't — Use vague, duplicated, or truncated labels

Generic labels ("Page", "Section") or mid-string ellipses defeat the wayfinding purpose. Let the component handle overflow instead of hand-truncating labels.

```tsx
{/* Wrong */}
<Breadcrumb href="/billing">Page</Breadcrumb>
<Breadcrumb href="/billing/invoices">Pa…</Breadcrumb>
```

**Source:** Published docs — Overview section · [accessibility.md:61](./accessibility.md) (WCAG 2.4.4 Link Purpose).

---

### Do — Make the current page the last, non-link item

Use `isActive` on the final `Breadcrumb`. It renders as plain text and carries `aria-current="page"`, telling assistive tech where the user is.

```tsx
<Breadcrumbs>
  <Breadcrumb href="/">Home</Breadcrumb>
  <Breadcrumb href="/billing">Billing</Breadcrumb>
  <Breadcrumb isActive>Invoices</Breadcrumb>
</Breadcrumbs>
```

### Don't — Render the current page as a link

A self-referencing link is misleading, fails `aria-current` expectations, and contradicts the published guidance ("this page is never a link").

```tsx
{/* Wrong — current page is a clickable link */}
<Breadcrumb href="/billing/invoices">Invoices</Breadcrumb>
```

**Source:** Published docs — Overview section · [props.md:67](./props.md) · [accessibility.md:35](./accessibility.md).

---

### Do — Keep the trail on a single line, top-left, above the page title

Breadcrumbs sit above the page title, anchored to the left, on a single row.

### Don't — Let the trail wrap to a second line

If the trail is too long for the row, collapse it with the overflow menu. Wrapping breaks visual hierarchy and the component's auto-layout.

**Source:** Published docs — Placement section · [Breadcrumbs-figma.md:205](./Breadcrumbs-figma.md) (`overflow: no wrap`).

---

### Do — Let the component auto-collapse beyond the threshold

Set `maxItems` to reflect your hierarchy depth and let the component render the ellipsis and overflow menu automatically.

```tsx
<Breadcrumbs maxItems={8} itemsBeforeCollapse={1} itemsAfterCollapse={1}>
  {/* …deep trail… */}
</Breadcrumbs>
```

### Don't — Hand-truncate or hand-omit middle items

Manually dropping items or shortening labels bypasses the accessible overflow `<button>` and hides destinations the user might need.

```tsx
{/* Wrong — middle items silently dropped */}
<Breadcrumbs>
  <Breadcrumb href="/">Home</Breadcrumb>
  <Breadcrumb isActive>Invoice 1042</Breadcrumb>
</Breadcrumbs>
```

**Source:** Published docs — Overflow menu section · [examples.md](./examples.md) · [props.md:50](./props.md).

---

### Do — Localise `collapsedTitle` and `ariaLabel`

Both props default to English strings. Translate them to match the rest of the UI; the ellipsis `<button>` `title` and the `<nav>` `aria-label` are read aloud by screen readers.

```tsx
<Breadcrumbs
  ariaLabel={t('breadcrumbs.nav')}
  collapsedTitle={t('breadcrumbs.showAllLinks')}
>
  {/* … */}
</Breadcrumbs>
```

### Don't — Ship the default English strings to a translated UI

Mixed-language ARIA text confuses screen-reader users and fails localisation review.

**Source:** [props.md:57](./props.md) · [accessibility.md:50](./accessibility.md).

---

### Do — Use breadcrumbs to complement primary navigation for deep hierarchies

Breadcrumbs are most valuable when users land deep in a hierarchy from search or external links and need to orient themselves and step back up.

### Don't — Use breadcrumbs on flat sites or as a progress tracker

If there is no hierarchy, there is no trail to show. For step-by-step flows, use a progress indicator or stepper instead.

**Source:** Published docs — Best Practices → When not to use.

---

## Accessibility quick reference

Cross-references to [accessibility.md](./accessibility.md):

- The root renders as `<nav>` with `aria-label` (defaults to `'Breadcrumbs'`; override via `ariaLabel`).
- Items render inside an `<ol>` — the sequence is conveyed to screen readers.
- The active item carries `aria-current="page"`; do not add it manually elsewhere.
- The ellipsis renders as a `<button>` with a `title` (`collapsedTitle`); it is keyboard-activatable.
- The separator is decorative and is expected to be excluded from the accessibility tree by the component.

See [accessibility.md](./accessibility.md) for the full WCAG 2.1 AA checklist.

---

## Gaps

| Item | Type | Description |
|------|------|-------------|
| Figma Do/Don't examples | SOURCE_GAP | No `↳ Breadcrumbs examples` Figma page with Do/Don't card frames found. Guidelines above are editorially transcribed from the published Oxygen docs page (screenshot, 2026-05-11) and cross-validated against MCP/Figma extraction. Re-run `figma-extract-usage` if such a page is ever created. |
| State token bindings (hover/active/focus) | SOURCE_GAP | Tracked as GAP-001 in [Breadcrumbs-audit.md](./Breadcrumbs-audit.md). Atoms exist in Figma but token bindings come from a shared library not resolved by the current extraction. Described behaviourally only — no token names asserted here. |
| Overflow Menu hardcoded values | SOURCE_GAP | Background, border, shadow, radius, width, and padding-y on the Overflow Menu container are hardcoded values, not bound tokens — see [Breadcrumbs-figma.md:127](./Breadcrumbs-figma.md). |
| "How to use slots" related guide URL | SOURCE_GAP | The published docs page links to a "How to use slots" guide under Related → Guides. The destination URL is not present in any extracted artifact and is not asserted here. <!-- TODO: confirm URL when guide URL is available --> |
| "Current page" typo | DESIGN_GAP | Figma text property is `curent page#20679:3` (one `r`). Tracked in [Breadcrumbs-figma.md:236](./Breadcrumbs-figma.md). Do not replicate the typo in code or copy. |

---

_Source: Published Oxygen docs page (screenshot, 2026-05-11) · Cross-referenced with Oxygen MCP and Figma extraction · Editorial draft_
