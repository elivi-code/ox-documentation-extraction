---
parent: "[[Badge]]"
section: composition
---

## Composition

<!-- STUB:GAP-001 source="Run figma-extract for Badge (node 2565:14) to produce badge-figma.md; the composition/subcomponent section depends on the Figma layer tree." -->
<!-- source: figma-only -->

> **Source gap:** Figma-confirmed composition (subcomponent containment, slot structure) is unavailable until `figma-extract` is run. The notes below derive from code examples only.

### Observed usage (from examples)

Badge is positioned relative to a host element rather than containing children components:

- **On an icon button** — `<Badge isInner>` absolutely positioned at the top-right of an `IconButton` / icon (e.g. `BellIcon`).
- **On a list item** — dot badge positioned below/centred on a `ListItem`.
- **Inside a wrapper** — `isInner` renders the badge absolutely positioned within a `position: relative` parent.

### AIBadge

`AIBadge` is a separate exported component that composes a **star icon** with text content. Its internal icon binding is unverified pending `figma-extract`.
