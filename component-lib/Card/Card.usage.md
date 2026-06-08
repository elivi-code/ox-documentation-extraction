---
parent: "[[Card]]"
section: usage
---

# Card — Usage

> ⚠️ **DEPRECATED** — `@8x8/oxygen-card` is deprecated with no stated replacement. These guidelines scope and govern legacy usage; they do not invite new instances.

<!-- STUB:GAP-001 source="Designer must populate the ↳ Card examples Figma page (node 49372:112) with ✅ Do / ❌ Don't template frames. Once complete, re-run figma-extract-usage to produce the canonical Card-usage.md." -->
> **PROVISIONAL (GAP-001)** — No canonical `Card-usage.md` exists yet: the Figma `↳ Card examples` page (node `49372:112`) holds only a freeform "Contact card" wireframe, no Do/Don't frames. The pairs below are drafted from grounded source evidence (props, examples, accessibility, figma) pending the Figma examples page and a `figma-extract-usage` run.

## Do / Don't

### Pair 1 — Lifecycle: don't introduce new Card instances

**✅ Do — Build new layouts directly with Oxygen primitives**
For new screens, compose headers, separators, and content blocks using current Oxygen typography, spacing, and surface tokens rather than reaching for Card. If a card-like grouping is needed, use a container with the same tokens Card uses (`ui02` background, `ui03` border, the spacing tokens in [[Card.tokens]]).

**❌ Don't — Pick Card for new screens because it "looks right"**
A deprecated component has no upgrade path and no committed bug-fix lane. Every new instance is debt the team will pay back later, and visual familiarity is not a justification for adopting code marked for removal.

---

### Pair 2 — Clickable card semantics

**✅ Do — Wrap the whole card in a single `<a>` for navigation**
If the card represents one destination, the entire surface should be one tab stop with one accessible name. The label describes the destination, not the act of clicking.

```tsx
<a href="/usage" aria-label="View detailed usage stats">
  <Card>
    <Header>Usage stats</Header>
    {/* …content… */}
  </Card>
</a>
```

**❌ Don't — Make the card clickable AND nest interactive elements inside it**
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

### Pair 3 — Header heading level (`aria-level`)

**✅ Do — Set `aria-level` on `Card.Header` to match the page outline**
If the card sits under an `<h2>` section, the header is `aria-level={3}`. If it sits under an `<h3>` subsection, set `aria-level={4}`. Levels should never skip a step.

```tsx
<section> {/* contains an <h2> */}
  <Card>
    <Header aria-level={3}>Usage stats</Header>
  </Card>
</section>
```

**❌ Don't — Let `aria-level` fall back to the default on every card**
The default of `3` silently breaks WCAG 1.3.1 whenever cards are nested under sections at other depths. Screen-reader users navigating by heading lose the document structure, and a card under an `<h1>` reading as `aria-level={3}` skips a level entirely.

---

### Pair 4 — Default to a header and a CTA

**✅ Do — Give each card one clear primary action**
A card with a header and one primary `Button` reads as a self-contained unit of work. The button label names the destination action ("Open report", "Renew now") — not a generic "View" or "More".

```tsx
<Card>
  <Header aria-level={3}>Renewal due</Header>
  {/* …summary content… */}
  <Button variant="primary">Renew now</Button>
</Card>
```

**❌ Don't — Strip the CTA "to reduce clutter" and rely on the whole card being clickable as an undocumented affordance**
If you remove the CTA, you also remove the visible signal that the card is interactive. Sighted users guess; keyboard users can't tell at all. Either keep the CTA, or commit explicitly to the clickable-card pattern (Pair 2) with a descriptive `aria-label` — don't split the difference.
