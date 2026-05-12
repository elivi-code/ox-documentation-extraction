---
component: Card
package: "@8x8/oxygen-card"
category: layout_overlay
role: usage_draft
role_description: "Usage guidelines draft — Do/Don't pairs scaffolded by usage-advisor, pending Figma review"
pipeline_stage: draft
pipeline_note: "Not a pipeline source. Scaffold for Figma examples page — produce Card-usage.md via figma-extract-usage once examples page exists."
status: DRAFT
drafted: "2026-05-12"
skill: usage-advisor
mode: open
grounding: full
siblings:
  - "[[Card/props]]"
  - "[[Card/examples]]"
  - "[[Card/accessibility]]"
  - "[[Card/Card-figma]]"
  - "[[Card/Card-audit]]"
tags:
  - oxygen
  - component/Card
  - role/usage_draft
  - stage/draft
  - category/layout_overlay
---

# Card — Usage Guidelines (Draft)

> **Draft only.** Scaffolding for the Figma examples page.
> The canonical `Card-usage.md` is produced by `figma-extract-usage` once a "↳ Card examples" page exists in Figma.

> ⚠️ **DEPRECATED** — `@8x8/oxygen-card` is deprecated with no stated replacement (see [Card-audit.md](Card-audit.md) WARN-002). These guidelines exist to scope and govern legacy usage, not to invite new instances.

## Grounding summary

- **Files used:** [props.md](props.md), [examples.md](examples.md), [tokens.md](tokens.md), [accessibility.md](accessibility.md), [Card-figma.md](Card-figma.md), [Card-audit.md](Card-audit.md)
- **Files missing:** `Card-pui.md` (N/A — Card has no application-layer concerns)
- **Internal precedent consulted:** [Button-usage.md](../Button/Button-usage.md) (one primary per surface), [Link-usage.md](../Link/Link-usage.md) (descriptive labels), [Accordion-usage.md](../Accordion/accordion-usage.md) (nesting depth)

---

## Pair 1 — Lifecycle: don't introduce new Card instances

**Decision:** Card is deprecated with no specified replacement. New work should not adopt Card; existing usage should be on a migration path.

**Grounded in:** [Card-audit.md](Card-audit.md) frontmatter (`deprecated: true`) and WARN-002 ("Component is deprecated with no stated replacement"); [props.md:34](props.md) banner ("Consider using an alternative layout pattern"); deprecation banners in [examples.md:27](examples.md), [tokens.md:27](tokens.md), [accessibility.md:27](accessibility.md), [Card-figma.md:35](Card-figma.md); [components-to-extract.md:52](../../components-to-extract.md) (`~~card~~`).

**Internal precedent:** none — first lifecycle-led pair in the workspace.

### ✅ Do — Build new layouts directly with Oxygen primitives

For new screens, compose headers, separators, and content blocks using current Oxygen typography, spacing, and surface tokens rather than reaching for Card. If a card-like grouping is needed, use a container with the same tokens Card uses (`ui02` background, `ui03` border, the spacing tokens in [tokens.md](tokens.md)).

### ❌ Don't — Pick Card for new screens because it "looks right"

A deprecated component has no upgrade path and no committed bug-fix lane. Every new instance is debt the team will pay back later, and visual familiarity is not a justification for adopting code marked for removal.

---

## Pair 2 — Clickable card semantics

**Decision:** When a card is interactive, it must be a single, semantically correct interactive element — not a clickable container with nested interactives.

**Grounded in:** [examples.md:73](examples.md) ("The whole card is clickable and should take you to a page with more information"); [accessibility.md:33](accessibility.md) ("Card renders as a generic container. If the card is interactive, the consuming element should carry `role='button'` or be a `<a>` / `<button>`"); [accessibility.md:51](accessibility.md) ("If the entire card is a link, use a single `<a>` wrapper rather than nested interactive elements to avoid ambiguous tab stops").

**Internal precedent:** [Link-usage.md](../Link/Link-usage.md) — *"Avoid vague labels like 'click here' — use accurate, descriptive words that describe the destination."*

### ✅ Do — Wrap the whole card in a single `<a>` for navigation

If the card represents one destination, the entire surface should be one tab stop with one accessible name. The label describes the destination, not the act of clicking.

```tsx
<a href="/usage" aria-label="View detailed usage stats">
  <Card>
    <Header>Usage stats</Header>
    {/* …content… */}
  </Card>
</a>
```

### ❌ Don't — Make the card clickable AND nest interactive elements inside it

Nested buttons and links inside a clickable card create ambiguous tab stops, double the screen-reader announcement, and trigger the wrong action on Enter/Space. Pick one: clickable card, or static card with an inner CTA — never both.

```tsx
{/* Wrong — nested interactives compete with the wrapping link */}
<a href="/usage">
  <Card>
    <Header>Usage stats</Header>
    <Button>Open report</Button>
    <Link href="/details">Details</Link>
  </Card>
</a>
```

---

## Pair 3 — Header heading level (`aria-level`)

**Decision:** Every Card that has a header must set `aria-level` to fit the surrounding heading hierarchy. The default of `3` is not a safe assumption.

**Grounded in:** [props.md:84](props.md) ("`aria-level` defaults to `3` if not provided. Set explicitly to match the surrounding document outline"); [accessibility.md:34](accessibility.md) ("Set `aria-level` to match surrounding document heading hierarchy"); [accessibility.md:58](accessibility.md) WCAG 1.3.1 Info and Relationships ("Use `Card.Header` with correct `aria-level` to convey heading hierarchy programmatically").

**Internal precedent:** none in the workspace specific to `aria-level`. Parallel pattern: Accordion's nested-depth rule treats heading structure as load-bearing rather than decorative.

### ✅ Do — Set `aria-level` on `Card.Header` to match the page outline

If the card sits under an `<h2>` section, the header is `aria-level={3}`. If it sits under an `<h3>` subsection, set `aria-level={4}`. Levels should never skip a step.

```tsx
<section> {/* contains an <h2> */}
  <Card>
    <Header aria-level={3}>Usage stats</Header>
  </Card>
</section>
```

### ❌ Don't — Let `aria-level` fall back to the default on every card

The default of `3` silently breaks WCAG 1.3.1 whenever cards are nested under sections at other depths. Screen-reader users navigating by heading lose the document structure, and a card under an `<h1>` reading as `aria-level={3}` skips a level entirely.

---

## Pair 4 — Default to a header and a CTA

**Decision:** Cards default to including both a header and a CTA. Hide either only when the card is read-only summary content, and only after deciding deliberately.

**Grounded in:** [examples.md:72](examples.md) ("Cards by default must have a header and a CTA"); [Card-figma.md](Card-figma.md) `Show actions` boolean default `true`; [accessibility.md:46](accessibility.md) ("Cards should default to having a CTA — ensure it is keyboard-reachable and has a descriptive accessible label").

**Internal precedent:** [Button-usage.md](../Button/Button-usage.md) Pair 1 — *"Use a single Primary button for the most important action … Establish a clear focal point. Secondary and Text buttons handle everything else on the surface."*

### ✅ Do — Give each card one clear primary action

A card with a header and one primary `Button` reads as a self-contained unit of work. The button label names the destination action ("Open report", "Renew now") — not a generic "View" or "More".

```tsx
<Card>
  <Header aria-level={3}>Renewal due</Header>
  {/* …summary content… */}
  <Button variant="primary">Renew now</Button>
</Card>
```

### ❌ Don't — Strip the CTA "to reduce clutter" and rely on the whole card being clickable as an undocumented affordance

If you remove the CTA, you also remove the visible signal that the card is interactive. Sighted users guess; keyboard users can't tell at all. Either keep the CTA, or commit explicitly to the clickable-card pattern in [Pair 2](#pair-2--clickable-card-semantics) with a descriptive `aria-label` — don't split the difference.

---

## Axes presented but skipped

Audit trail — these were on the Step 1 shortlist but ranked lower than the four picks above.

- **Slot composition constraints** — [Card-figma.md](Card-figma.md) does not document accepted content types or nesting depth; any rule would be a craft heuristic without file grounding.
- **Header icon (`Show icon` boolean)** — purely stylistic; no accessibility or destructive-action leverage.
- **Image/media aspect ratio** — no aspect-ratio rule documented in [Card-figma.md](Card-figma.md); writing one would invent guidance the audit explicitly avoids.
- **Card height & density** — [Card-figma.md](Card-figma.md) shows a fixed 226px but documents no rule about whether that's a hard constraint or content-driven.
- **Hover state applicability** — mechanical; resolves automatically once Pair 2 (clickable semantics) is settled.

## Axes flagged as ungrounded

None — all four approved pairs trace to specific file:section evidence inside `component-lib/Card/`.
