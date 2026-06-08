---
parent: "[[Card]]"
section: composition
---

# Card — Composition

> ⚠️ **DEPRECATED** — `@8x8/oxygen-card` is deprecated. Composition examples preserved for reference only.

Card is composed from its sub-components: [[Header]] (section heading), [[Separator]] (visual divider), and [[Statistics]] (labelled statistic list). All are imported from the same package.

## Basic Card with Header

```tsx
import { Card, Header } from '@8x8/oxygen-card';

<Card>
  <Header>Oxygen Card</Header>
</Card>
```

## Card with Separator

```tsx
import { Card, Header, Separator } from '@8x8/oxygen-card';

<Card>
  <Header>Section Title</Header>
  <Separator />
  {/* card body content */}
</Card>
```

## Card with Statistics

```tsx
import { Card, Header, Statistics } from '@8x8/oxygen-card';

<Card>
  <Header>Usage Stats</Header>
  <Statistics data={[/* StatisticsItemData[] */]} />
</Card>
```

<!-- STUB:GAP-012 source="Blocked by GAP-003 for the Statistics shape. For remaining patterns, obtain confirmed usage examples from Storybook stories. Add: (1) clickable card wrapping in <a>, (2) Show actions=false variant, (3) custom icon via Select Light icon prop." -->
> **SOURCE_GAP (GAP-012)** — `get-component-examples` (cleanExamples:true) returned 0 results for the card package; the examples above are derived from the Storybook documentation story. The Statistics example uses a placeholder because the `StatisticsItemData` shape is unknown (depends on **GAP-003**, see [[Card.props]]). No examples cover: themed card, clickable-card pattern, custom icon selection, or `Show actions` / `Show icon` toggle usage.

## Usage guidance (from MCP)

Cards are used to show snippets of information which can lead the user to more info.

- A card can hold any kind of information.
- The size can be adapted to the needs of the design.
- Cards by default must have a header and a CTA.
- The whole card is clickable and should take you to a page with more information.

> See [[Card.usage]] for Do/Don't guidelines on clickable semantics, heading levels, and CTA defaults.
