---
component: Card
package: "@8x8/oxygen-card"
category: layout_overlay
role: examples
role_description: "Code examples — usage patterns from basic to advanced"
pipeline_stage: spec_ready
pipeline_note: "Audit verdict YES/PARTIAL — doc-rewrite can run"
audit_verdict: YES
siblings:
  - "[[Card/props]]"
  - "[[Card/tokens]]"
  - "[[Card/accessibility]]"
  - "[[Card/Card-figma]]"
  - "[[Card/Card-audit]]"
tags:
  - oxygen
  - component/Card
  - role/examples
  - stage/spec_ready
  - category/layout_overlay
---
# Card — Examples

> **See also:** [props.md](props.md) · [tokens.md](tokens.md) · [accessibility.md](accessibility.md)

> ⚠️ **DEPRECATED** — `@8x8/oxygen-card` is deprecated. Examples are preserved for reference only.

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

> **DOC\_GAP** — No clean code examples were returned by the Oxygen MCP for this package (0 clean examples). The basic example above is derived from the Storybook documentation story. The `StatisticsItemData` shape is also unknown; see [props.md](props.md).

---

## Usage Guidance (from MCP)

Cards are used to show snippets of information which can lead the user to more info.

- A card can hold any kind of information.
- The size can be adapted to the needs of the design.
- Cards by default must have a header and a CTA.
- The whole card is clickable and should take you to a page with more information.

---

_Source: Oxygen MCP · Extracted 2026-05-05_
