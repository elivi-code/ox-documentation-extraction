---
component: Pagination
package: "@8x8/oxygen-pagination"
category: navigation
role: usage
role_description: "Usage guidelines — editorial, compiled from the published Oxygen docs page and the extracted MCP/Figma artifacts"
pipeline_stage: editorial
pipeline_note: "Usage authored editorially from the published Oxygen docs page (https://oxygen.8x8.com/components/pagination/usage, fetched 2026-05-13 via WebFetch) cross-referenced with the existing figma-extract-usage descriptive variants and the MCP/Figma artifacts. The published docs page contains a one-line Overview, Behavior, When-to-use × 2, When-not-to-use × 1, and a Related entry — but NO Do/Don't card frames. The Figma '↳ Pagination examples' page documents behavioural variants (Type / Responsive / Size / Tooltips) without Do/Don't cards either (GAP-014 in Pagination-audit.md). Do/Don't pairs below are derived from the docs-page intent + behavioural variants + props.md, examples.md, accessibility.md, and Pagination-figma.md. Replace pairs with figma-extract-usage output if Do/Don't card frames are ever added to the Figma examples page."
source_type: editorial
audit_verdict: null
siblings:
  - "[[Pagination/props]]"
  - "[[Pagination/examples]]"
  - "[[Pagination/tokens]]"
  - "[[Pagination/accessibility]]"
  - "[[Pagination/Pagination-figma]]"
  - "[[Pagination/Pagination-audit]]"
tags:
  - oxygen
  - component/Pagination
  - role/usage
  - stage/editorial
  - category/navigation
---
<!-- SOURCE: editorial — published Oxygen docs page (https://oxygen.8x8.com/components/pagination/usage, fetched 2026-05-13 via WebFetch) + figma-extract-usage descriptive variants (existing Pagination-usage.md, 2026-05-01) + extracted MCP/Figma artifacts -->
<!-- FIGMA EXAMPLES PAGE: present but descriptive only — no ✅ Do / ❌ Don't card frames (GAP-014) -->
<!-- GROUNDING: full — props.md, examples.md, tokens.md, accessibility.md, Pagination-figma.md, Pagination-audit.md, published docs page -->
<!-- DRAFTED: 2026-05-13 -->
<!-- MODE: docs-mirrored -->
<!-- PAIRS: 7 (derived from docs page Best Practices + Figma examples behavioural sections + extracted artifacts) -->
<!-- REPLACES: figma-extract-usage descriptive output from 2026-05-01 (variants carried forward into Behaviour section) -->
<!-- STATUS: editorial draft — replace pairs with figma-extract-usage output if a Figma "↳ Pagination examples" page is ever populated with Do/Don't card frames -->

# Pagination — Usage Guidelines

> **See also:** [props.md](./props.md) · [examples.md](./examples.md) · [tokens.md](./tokens.md) ·
> [accessibility.md](./accessibility.md) · [Pagination-figma.md](./Pagination-figma.md)

> **Editorial guidance — mirrors the published Oxygen docs page.** No `↳ Pagination examples` Figma page with `✅ Do —` / `❌ Don't —` card frames exists; the Figma examples page documents behavioural variants only (Type, Responsive, Size, Tooltips) — tracked as **GAP-014** in [Pagination-audit.md](./Pagination-audit.md). The body below transcribes the published Oxygen docs page (`https://oxygen.8x8.com/components/pagination/usage`, fetched 2026-05-13) verbatim where the page asserts something, carries forward the descriptive variants from the prior `figma-extract-usage` run as the **Behaviour** section, and derives Do/Don't pairs from the docs page's intent + Figma behavioural variants cross-validated against [props.md](./props.md), [examples.md](./examples.md), [accessibility.md](./accessibility.md), and [Pagination-figma.md](./Pagination-figma.md).

Pagination lets users move through a large dataset that has been split across multiple pages. It is the canonical navigation control for paginated lists and data tables in 8x8 product surfaces — anywhere the result set is too big for a single screen but small enough that loading it all at once is wasteful or visually overwhelming. The component renders a horizontal control with three logical regions: a rows-per-page selector on the left, page navigation (previous · current page · count · next) on the right, and a compact mode that drops the rows-per-page region below 548 px container width.

---

## Anatomy

The Figma anatomy ([Pagination-figma.md:48](./Pagination-figma.md)) and the published docs anatomy ([examples.md:76](./examples.md)) compose as follows:

1. **Rows per page label** — a localised string ("Rows per page:") preceding the rows dropdown. Lives inside the optional `Rows per page` slot ([Pagination-figma.md:52](./Pagination-figma.md)). Value comes from `translations.rowsPerPage` ([props.md:97](./props.md)).
2. **Rows per page dropdown** — a `Select` sub-component bound to the array passed via `rowsPerPageOptions` ([props.md:77](./props.md)). Width is hardcoded — 88 px at default size, 72 px at small size ([Pagination-figma.md:54](./Pagination-figma.md)). The whole slot is hidden when `rowsPerPageOptions` is omitted and is **always hidden** below the 548 px breakpoint ([Pagination-figma.md:52](./Pagination-figma.md)).
3. **Previous button** — an icon button (`arrow-left-long`) with a tooltip showing `translations.prevPage` on hover and on keyboard focus. Disabled visually + programmatically when `canGoBack === false` ([props.md:70](./props.md)). Padding varies with size and breakpoint ([Pagination-figma.md:75](./Pagination-figma.md)).
4. **Page selector** — a `Select` sub-component listing every available page; the user can jump directly. The preceding "Page" label is localised; value comes from `translations` (label text is fixed in the Figma example).
5. **Page count** — the optional "of {numberOfPages} pages" text right of the page selector. Hidden in the "Unknown page number" variant. Text comes from `translations.numberOfPages` interpolated against the `numberOfPages` prop ([props.md:72](./props.md)).
6. **Next button** — mirror of the Previous button, icon `arrow-right-long`, tooltip from `translations.nextPage`, disabled when `canGoNext === false`.

A focus ring is not modelled in the Figma component variant set ([GAP-010](./Pagination-audit.md)) but is required by WCAG 2.4.7 for every interactive control — keep the platform default.

**Source:** [Pagination-figma.md:48-76](./Pagination-figma.md) · [props.md:68-81](./props.md) · [examples.md:76-83](./examples.md).

---

## Overview

> **Verbatim from the docs page:** "Pagination is a component used to navigate through a large set of data divided into multiple pages."

A single Oxygen package, `@8x8/oxygen-pagination`, exports one component plus a state hook ([props.md:62](./props.md)):

| Export | Use for | Key props / signature |
|--------|---------|----------------------|
| `Pagination` | The visible control — renders the rows-per-page selector, prev / next buttons, page selector, and page count. | `canGoBack`, `canGoNext`, `numberOfPages`, `pageNumber`, `rowsPerPage`, `onPaginationChange`, `translations`, optional `rowsPerPageOptions`, `size`, `isDisabled` |
| `usePagination` | State derivation hook. Computes `canGoBack`, `canGoNext`, and `numberOfPages` from a `PaginationState` + `totalRecords`. Always used **outside** the `<Pagination>` element. | `usePagination(pagination, totalRecords)` → `{ canGoBack, canGoNext, numberOfPages, pageNumber, rowsPerPage }` |
| `PaginationState` | The state shape held by the consumer's `useState`. | `{ pageNumber: number; rowsPerPage: number }` |

> **Verbatim from the docs page (Behavior):** "The component enables users to interact through navigation controls featuring previous/next buttons, adjustable row display options, and page location selection."

---

## Behaviour

The Figma `↳ Pagination examples` page (extracted 2026-05-01) documents four behavioural variants. They are not Do/Don't card pairs — they are descriptive renderings of how the component changes shape under different prop combinations and container widths. The screenshots referenced below were extracted as part of the original `figma-extract-usage` run.

### Type — known vs. unknown page number

![Pagination type variants](./figma-usage-type.png)

**Known page number** — *"To be used when the page numbers are known."* (verbatim Figma caption). Shows the full pagination bar with rows-per-page dropdown, previous/next buttons, page selector, and the "of N pages" count.

**Unknown page number** — *"To be used when the page numbers are unknown."* (verbatim Figma caption). The "of N pages" count is hidden; the page selector still works but no total is shown.

**Without rows per page** — *"Pagination can be used without the control of the number of rows per page."* (verbatim Figma caption). Two sub-variants: with and without the page count. Omit `rowsPerPageOptions` ([props.md:77](./props.md)) to suppress the entire rows-per-page slot ([Pagination-figma.md:225](./Pagination-figma.md)).

### Responsive — full layout vs. compact layout

![Pagination responsive rules](./figma-usage-responsive.png)

**Containers ≥ 548 px wide** — full layout. Rows-per-page section on the left, page controls on the right. Container width capped at 640 px in the Figma example.

**Containers < 548 px wide** — compact layout. The rows-per-page section is hidden; only the page controls render. Width constrained to 547 px max, 288 px min in the Figma example.

> **Note:** The 548 px breakpoint is a **Figma design decision** — there is no `breakpoint` prop on the React component ([CON-001 / Pagination-audit.md](./Pagination-audit.md)). Responsive layout is the consuming application's responsibility (CSS media queries, container queries, or conditional rendering of the `rowsPerPageOptions` array).

### Size — default vs. small

![Pagination size variants](./figma-usage-size.png)

**Default** — 40 px height ([Pagination-figma.md:165](./Pagination-figma.md)). Used in standard data-table contexts. `size` prop omitted or set to the default value.

**Small** — 32 px height ([Pagination-figma.md:166](./Pagination-figma.md)). For denser layouts, narrow side panels, or compact admin tables. Set `size="small"` ([props.md:78](./props.md), [examples.md:93](./examples.md)).

Both sizes are shown at both breakpoints in the Figma examples — `size` is an independent axis from `breakpoint`. The exact `PaginationSize` enum values are not exposed by the MCP ([GAP-004](./Pagination-audit.md)); `"small"` is taken from the docs page and the Figma variant axis.

### Tooltips & keyboard focus on Previous / Next

![Pagination tooltips and keyboard focus](./figma-usage-tooltips.png)

The Previous and Next buttons are **icon-only**. Their accessible name and their visible tooltip both come from the `translations` prop — `translations.prevPage` for the left button, `translations.nextPage` for the right ([props.md:99-100](./props.md), [accessibility.md:36-37](./accessibility.md)).

The Figma examples page renders the tooltip both on **hover** and on **keyboard focus** for both buttons. Keyboard focus must surface the same affordance as pointer hover so that keyboard-only users have access to the same label.

---

## Best Practices

### When to use

Verbatim from the published docs page:

- "Use pagination when there are too many results to display on one page."
- "Use pagination for tables with more than ten rows."

### When not to use

Verbatim from the published docs page:

- "Do not use pagination if the items or data are not part of the same set."

Two patterns are commonly mistaken for pagination but solve a different problem:

| Pattern | Use it when | Don't confuse with pagination |
|---------|-------------|------------------------------|
| Infinite scroll | The user wants to skim; the result set is open-ended; the order is feed-style. | Pagination preserves position and supports keyboard "jump to page" — infinite scroll does neither. |
| Tabs / Steppers | The content is structured into distinct labelled sections. | Pagination is for one ordered list split by count, not by category. |

---

## Do / Don't

These pairs are derived editorially from the docs page's Best Practices + the Figma examples page's behavioural variants combined with the extracted API and accessibility data. No Figma ✅ Do / ❌ Don't card frames exist for Pagination at the time of writing — the `↳ Pagination examples` page contains descriptive variant sections only (**GAP-014** in [Pagination-audit.md](./Pagination-audit.md)).

### Pair 1 — Paginate one logical dataset, not a mix of disjoint items

#### ✅ Do — Paginate a single query result, list, or filterable dataset

Pagination is a position cursor on one ordered collection. Use it when the user is moving through pages of the same kind of thing — call records, contacts, support tickets — produced by a single query or filter. The user's mental model is "page 2 of the same list", which only holds when the items are part of the same set.

```tsx
const [pagination, setPagination] = useState<PaginationState>({
  pageNumber: 1,
  rowsPerPage: 25,
});

const { canGoBack, canGoNext, numberOfPages, pageNumber, rowsPerPage } =
  usePagination(pagination, totalContactsMatchingFilter);

<Pagination
  canGoBack={canGoBack}
  canGoNext={canGoNext}
  numberOfPages={numberOfPages}
  onPaginationChange={setPagination}
  pageNumber={pageNumber}
  rowsPerPage={rowsPerPage}
  rowsPerPageOptions={[10, 25, 50, 100]}
  translations={{
    rowsPerPage: 'Rows per page:',
    prevPage: 'Previous page',
    numberOfPages: `of ${numberOfPages} pages`,
    nextPage: 'Next page',
  }}
/>
```

#### ❌ Don't — Wrap pagination around a mixed set of unrelated items

If the "list" is actually multiple disjoint collections concatenated together (recent activity + saved filters + suggested contacts), the page number is meaningless — paging forward doesn't take the user *further into the same list*, it crosses category boundaries. Group by category and let each region have its own affordance.

```tsx
{/* Wrong — three disjoint result sets paginated as one */}
const merged = [
  ...recentActivity,    // 12 items
  ...savedFilters,      // 4 items
  ...suggestedContacts, // 30 items
];

<Pagination
  /* ...rowsPerPage = 10, numberOfPages = 5...
     Page 2 = end of activity + all saved filters + start of suggestions */
/>
```

**Source:** Published docs — Best Practices "When not to use" · [examples.md:107-109](./examples.md) · [Pagination-figma.md:219-225](./Pagination-figma.md).

---

### Pair 2 — Only paginate when there's more than fits on one screen

#### ✅ Do — Add Pagination once the result count exceeds roughly ten rows or fills the viewport

The docs page sets a floor: tables with more than ten rows. The intent is "more than the user can comfortably scan at a glance" — short lists don't benefit from a control that adds visual noise and a click cost.

```tsx
{totalRecords > rowsPerPage && (
  <Pagination
    canGoBack={canGoBack}
    canGoNext={canGoNext}
    numberOfPages={numberOfPages}
    /* ...rest of required props... */
  />
)}
```

#### ❌ Don't — Render Pagination over a short, fully-visible list

A pagination control on a five-row table reads as a bug to the user and to assistive tech: there's nothing to navigate. It also occupies vertical space that could surface the actual content. Conditionally render the control once `totalRecords > rowsPerPage`.

```tsx
{/* Wrong — only 7 results but the control still renders */}
<Pagination
  canGoBack={false}
  canGoNext={false}
  numberOfPages={1}
  pageNumber={1}
  rowsPerPage={10}
  /* ...the user sees a disabled control with "1 of 1 pages"... */
/>
```

**Source:** Published docs — Best Practices "When to use" · [examples.md:103-106](./examples.md).

---

### Pair 3 — Match the Type variant to what you actually know

#### ✅ Do — Use the "Unknown page number" variant when the total isn't queryable

If the backend can't (or won't) return a total count — common with cursor-paginated APIs, streamed search results, or expensive full-text queries — render the "Unknown page number" Figma variant: keep `canGoBack` / `canGoNext` accurate from the cursor, but hide the "of N pages" label by omitting `translations.numberOfPages` (or pass an empty string). The page selector + prev / next still work; the user just doesn't see a fabricated total.

```tsx
<Pagination
  canGoBack={hasPrevCursor}
  canGoNext={hasNextCursor}
  numberOfPages={0}       /* sentinel for unknown */
  pageNumber={pageNumber}
  rowsPerPage={rowsPerPage}
  onPaginationChange={setPagination}
  translations={{
    rowsPerPage: 'Rows per page:',
    prevPage: 'Previous page',
    numberOfPages: '',    /* hides the "of N pages" string */
    nextPage: 'Next page',
  }}
/>
```

#### ❌ Don't — Invent a total just to render the "of N pages" count

A guessed or capped total ("of 100+ pages") is worse than no total — the user trusts the number and plans accordingly, then the count contradicts itself when they reach the end. If the total isn't known, say nothing about it.

```tsx
{/* Wrong — fabricated total, cursor API doesn't return one */}
<Pagination
  numberOfPages={999}     /* placeholder; the API has no real total */
  /* ...the "of 999 pages" label now lies to the user */
  translations={{ numberOfPages: `of ${999} pages`, ...rest }}
/>
```

**Source:** [Pagination-figma.md:84](./Pagination-figma.md) (`numberOfPages` boolean) · existing Figma examples Type section (above) · [props.md:72](./props.md).

---

### Pair 4 — Drive the responsive layout from the container, not from a Pagination prop

#### ✅ Do — Below 548 px, suppress the rows-per-page control at the consumer level

The 548 px breakpoint is a Figma design decision — there is no `breakpoint` prop on `<Pagination>` ([CON-001](./Pagination-audit.md)). The consumer owns the responsive swap: at narrow widths, omit `rowsPerPageOptions` or hide the section via CSS / container queries. The component already produces the compact layout when no rows-per-page choices exist.

```tsx
const isNarrow = containerWidth < 548;

<Pagination
  canGoBack={canGoBack}
  canGoNext={canGoNext}
  numberOfPages={numberOfPages}
  pageNumber={pageNumber}
  rowsPerPage={rowsPerPage}
  rowsPerPageOptions={isNarrow ? undefined : [10, 25, 50, 100]}
  onPaginationChange={setPagination}
  translations={translations}
/>
```

#### ❌ Don't — Cram the full layout into a narrow container and expect Pagination to adapt

Forcing the desktop layout below ~548 px overflows the row, wraps awkwardly, or pushes the next button off-screen. There is no `breakpoint` prop to flip — passing one will throw a type error or be silently ignored. The Figma examples page treats this as a layout constraint, not a component capability.

```tsx
{/* Wrong — pretending there's a breakpoint prop on the component */}
<div style={{ width: 320 }}>
  <Pagination
    /* @ts-expect-error — no such prop */
    breakpoint="< 548px"
    rowsPerPageOptions={[10, 25, 50, 100]}
    /* ...the rows-per-page section now overflows the 320px container */
  />
</div>
```

**Source:** [Pagination-figma.md:223](./Pagination-figma.md) · [Pagination-audit.md CON-001](./Pagination-audit.md) · existing Figma examples Responsive section (above).

---

### Pair 5 — Localise every visible string via `translations`; icon-only buttons need it most

#### ✅ Do — Pass a complete `translations` object so prev / next get tooltips and accessible names

The Previous and Next buttons are icon-only ([Pagination-figma.md:75](./Pagination-figma.md)). The chevrons mean nothing to a screen reader and nothing to a user who doesn't share the icon convention. `translations.prevPage` and `translations.nextPage` feed both the visible tooltip and the `aria-label` ([accessibility.md:36-37](./accessibility.md)). Localise all four strings — `rowsPerPage`, `prevPage`, `numberOfPages`, `nextPage` — using the same source as the rest of the page's UI strings.

```tsx
import { t } from '@/i18n';

<Pagination
  /* ...required props... */
  translations={{
    rowsPerPage: t('pagination.rowsPerPage'),    /* "Rows per page:" */
    prevPage:    t('pagination.prevPage'),       /* "Previous page" */
    numberOfPages: t('pagination.numberOfPages', /* "of {n} pages"  */
                    { n: numberOfPages }),
    nextPage:    t('pagination.nextPage'),       /* "Next page"     */
  }}
/>
```

#### ❌ Don't — Ship the component with hardcoded English strings or rely on the chevron icon alone

Hardcoding "Prev" / "Next" breaks every non-English surface. Worse, omitting `translations` entirely (the prop is required — TypeScript will complain) or passing empty strings strips the buttons of their accessible name, failing WCAG 4.1.2 ([accessibility.md:72](./accessibility.md)).

```tsx
{/* Wrong — translations stripped to bare icons; aria-label is empty */}
<Pagination
  /* ...required props... */
  translations={{
    rowsPerPage: '',
    prevPage: '',
    numberOfPages: '',
    nextPage: '',
  }}
/>
```

**Source:** [accessibility.md:36-37](./accessibility.md) · [props.md:96-101](./props.md) · [Pagination-figma.md:75](./Pagination-figma.md) · existing Figma examples Tooltips section (above).

---

### Pair 6 — Keep every control keyboard-operable and the focus ring visible

#### ✅ Do — Let the platform focus ring render on rows-per-page, prev, page selector, next

Pagination is `role="navigation"` ([accessibility.md:34](./accessibility.md)). Every interactive control inside it (the two `Select`s and the two icon buttons) must be reachable with `Tab` / `Shift+Tab` and must show a visible focus indicator (WCAG 2.4.7, [accessibility.md:70](./accessibility.md)). The Figma tooltips section explicitly mirrors hover and keyboard-focus states, so the tooltip + focus ring should appear together when the user tabs to prev / next.

```tsx
{/* No custom focus styling needed — the platform handles it.
    Just don't override outline / box-shadow to "none". */}
<Pagination
  /* ...required props... */
/>
```

#### ❌ Don't — Suppress the focus ring or trap focus inside a disabled state

`outline: none` (or a global `*:focus { outline: 0 }`) removes the only signal keyboard users have for "where am I?". When `canGoBack` is `false` or `isDisabled` is `true`, the prev button is `aria-disabled="true"` ([accessibility.md:40](./accessibility.md)) but still keeps focus order coherent — don't `tabindex="-1"` it out of the order.

```css
/* Wrong — kills the focus indicator the component relies on */
button:focus,
.oxygen-pagination * { outline: none !important; }
```

**Source:** [accessibility.md:34, 42-50, 64-72](./accessibility.md) · [Pagination-figma.md:230-235](./Pagination-figma.md) (no Figma a11y annotations — see GAP-009).

---

### Pair 7 — `rowsPerPageOptions` exists to give the user a real choice — don't pass a single value

#### ✅ Do — Pass two or more meaningful row-count options, or omit `rowsPerPageOptions` entirely

`rowsPerPageOptions` ([props.md:77](./props.md)) is optional. If you pass it, the rows-per-page section renders and the user can choose. Pass at least two values that actually differ in user value (e.g. `[10, 25, 50, 100]`). If your surface doesn't offer a choice — the row count is fixed by product or contract — omit the prop and the entire section hides ([Pagination-figma.md:225](./Pagination-figma.md)), which is the "Without rows per page" Figma variant above.

```tsx
{/* Choice offered */}
<Pagination
  /* ...required props... */
  rowsPerPageOptions={[10, 25, 50, 100]}
/>

{/* No choice — fixed at 25, omit the prop */}
<Pagination
  /* ...required props with rowsPerPage={25}... */
/>
```

#### ❌ Don't — Render a `rowsPerPageOptions` dropdown that has only one option

A single-option dropdown is a non-choice with visual cost: it implies a choice that doesn't exist, the user clicks it once, sees one item, and learns to ignore it. Either give a real choice or hide the section.

```tsx
{/* Wrong — dropdown shows one option; just hide the section */}
<Pagination
  /* ...required props... */
  rowsPerPageOptions={[25]}
/>
```

**Source:** [props.md:77](./props.md) · [Pagination-figma.md:225](./Pagination-figma.md) (`rowsPerPage` boolean) · existing Figma examples "Without rows per page" variant (above).

---

## Accessibility quick reference

Cross-references to [accessibility.md](./accessibility.md):

- The component is `role="navigation"` with `aria-label="Pagination"` (or the localised equivalent) so screen readers can distinguish it from other `<nav>` regions ([accessibility.md:34-35](./accessibility.md)).
- Previous / Next are icon-only buttons — they must carry `aria-label` values from `translations.prevPage` / `translations.nextPage` ([accessibility.md:36-37](./accessibility.md)). The same strings drive the visible tooltip on hover **and** keyboard focus.
- Both `Select` controls must expose accessible names; the visible "Rows per page:" / "Page" labels do that job when associated correctly ([accessibility.md:38-39](./accessibility.md)).
- Disabled state propagates via `aria-disabled="true"` on the affected button(s) — `canGoBack === false` disables prev, `canGoNext === false` disables next, `isDisabled` disables everything ([accessibility.md:40, 53](./accessibility.md)).
- Tab order: rows-per-page → prev → page selector → next ([accessibility.md:69](./accessibility.md)). `Tab` / `Shift+Tab` move; `Enter` / `Space` activate; `↑` / `↓` move within an open dropdown; `Esc` closes a dropdown ([accessibility.md:43-50](./accessibility.md)).
- Focus ring must clear WCAG 1.4.11 (≥ 3:1 contrast). The Figma component set does not model focus visually ([GAP-010](./Pagination-audit.md)) — keep the platform default; never `outline: none`.
- A page change should not cause a context shift (WCAG 3.2.2); only the user's explicit click / Enter activates the change ([accessibility.md:71](./accessibility.md)). Pair the paginated content region with `aria-live="polite"` if you want screen readers to announce the new page content ([accessibility.md:58-60](./accessibility.md)).
- All accessibility content in [accessibility.md](./accessibility.md) is **inferred** — neither the OX MCP nor the Figma component set provided explicit a11y data ([WARN-001, GAP-008, GAP-009](./Pagination-audit.md)). Spot-check ARIA against the rendered DOM before publishing.

See [accessibility.md](./accessibility.md) for the full WCAG 2.1 AA checklist.

---

## Related components

The published docs page lists one neighbour under **Related → Components**:

- **Breadcrumbs** — pagination moves through the *same* dataset; breadcrumbs move *up* a navigation hierarchy. Don't substitute one for the other.

Adjacent 8x8 components that compose with Pagination:

- **DataTable** — the most common host for Pagination; the rows-per-page choice changes the DataTable's visible row count.
- **Select** — Pagination uses two `Select` sub-components internally (rows-per-page and page number); if your dataset needs filtering above the table, use Select outside the Pagination control, not inside it.
- **Button** — page-level actions ("Add", "Export") sit outside Pagination, not in the same row.

---

## Gaps

| Item | Type | Description |
|------|------|-------------|
| Figma Do/Don't examples | SOURCE_GAP · GAP-014 | The `↳ Pagination examples` page documents behavioural variants only — no Do/Don't card frames. Pairs above are editorially derived. Re-run `figma-extract-usage` if such cards are added. |
| `breakpoint` Figma axis vs. React prop | CONFLICT (resolved) · CON-001 | Figma models `> 548px` / `< 548px` as a variant axis; the React component has no `breakpoint` prop. Documented as a consumer responsibility in Pair 4. |
| `rowsPerPage` Figma boolean vs. React prop | CONFLICT (resolved) · CON-002 | The Figma `rowsPerPage` boolean maps to **omitting** `rowsPerPageOptions` on the React side. Documented in Pair 7 and in the "Without rows per page" Behaviour subsection. |
| `PaginationSize` enum values inferred | SOURCE_GAP · GAP-004 | MCP returned the type name without enum members. `"small"` is taken from the docs page and the Figma variant axis; verify against package source. |
| 7 props lack OX descriptions | SOURCE_GAP · GAP-005 | `canGoBack`, `canGoNext`, `numberOfPages`, `pageNumber`, `rowsPerPage`, `rowsPerPageOptions`, `size` have inferred descriptions in `props.md`. The semantics used in the pairs above are anchored in the Figma anatomy + the usage Behaviour section. |
| No disabled / dark-mode / small-with-required-props examples | SOURCE_GAP · GAP-006 | Storybook / MCP returned only one functional snippet (BasicUsage). The pairs above hand-derive TSX from the prop API. |
| Hardcoded inner spacings | SOURCE_GAP · GAP-012 | 10 hardcoded values flagged in `Pagination-figma.md` (Select widths, container widths, button paddings, 6 px border radius). None bound to a spacing token. Not blocking. |
| Accessibility content entirely inferred | WARN · WARN-001 | `accessibility.md` reads ARIA roles, focus order, and keyboard interactions off standard patterns. Spot-check against rendered DOM before publishing. |
| No hover / focus / pressed Figma variants | SOURCE_GAP · GAP-010 | Only Default and Disabled variants are modelled. Tooltip + focus behaviour is documented on the examples page (carried forward into Behaviour) but not as discrete component states. |
| OX MCP returned 0 theme tokens | SOURCE_GAP · GAP-001 | The token names used in `Pagination-figma.md` (e.g. `text/textcolor01`, `ui/ui05`) were confirmed via alias-chain traversal (2026-05-05) but `tokens.md` is still empty pending `doc-rewrite`. |

---

_Source: Published Oxygen docs page (`https://oxygen.8x8.com/components/pagination/usage`, fetched 2026-05-13 via WebFetch) · figma-extract-usage descriptive variants (existing `Pagination-usage.md`, 2026-05-01) · Oxygen MCP + Figma MCP extraction (`@8x8/oxygen-pagination`, Figma file `5YihJ5WuDvnvrlrRMC4sBp`, Pagination node `55766:411`) · Editorial draft 2026-05-13._
