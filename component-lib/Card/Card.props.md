---
parent: "[[Card]]"
section: props
---

# Card — Props

> ⚠️ **DEPRECATED** — `@8x8/oxygen-card` is deprecated. The entire package including all sub-components (Card, Header, Separator, Statistics) is marked deprecated, with no stated replacement. Do not adopt for new work.

## Installation

```sh
# yarn
$ yarn add @8x8/oxygen-card

# npm
$ npm install @8x8/oxygen-card
```

**Registry prerequisite** — add to `.npmrc` (or `.yarnrc.yml` for Yarn):

```
@8x8:registry=https://artifactory.es.8x8.com/artifactory/api/npm/npm-repository/
```

> VPN required to access the private Artifactory registry.

## Import

```tsx
import { Card, Header, Separator, Statistics } from '@8x8/oxygen-card';
```

---

## `Card` (default export)

Root container component.

| Prop | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| `children` | `React.ReactNode` | No | — | Card content |
| `testId` | `string` | No | `'CARD'` | `data-testid` DOM attribute value |
| `theme` | `Partial<CardTheme>` | No | — | Theme override object for the component |

---

## `Card.Header`

Section heading rendered inside a Card. Uses `role="heading"` with `aria-level` for flexible heading hierarchy.

| Prop | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| `children` | `React.ReactNode` | **Yes** | — | Header content |
| `testId` | `string` | No | `'CARD_HEADER'` | `data-testid` DOM attribute value |
| `theme` | `Partial<CardTheme>` | No | — | Theme override object |

> `aria-level` defaults to `3` if not provided. Set explicitly to match the surrounding document outline.

---

## `Card.Separator`

Visual horizontal divider between card sections.

| Prop | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| `testId` | `string` | No | `'CARD_SEPARATOR'` | `data-testid` DOM attribute value |
| `theme` | `Partial<CardTheme>` | No | — | Theme override object |

---

## `Card.Statistics` _(deprecated)_

Displays a list of labelled statistic items inside a card.

| Prop | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| `data` | `StatisticsItemData[]` | **Yes** | — | Array of statistic items to display |
| `testId` | `string` | No | `'CARD_STATISTICS'` | `data-testid` DOM attribute value |
| `theme` | `Partial<StatisticsTheme>` | No | — | Theme override object |

<!-- STUB:GAP-003 source="Locate the StatisticsItemData type definition in the @8x8/oxygen-card package source (TypeScript types or JSDoc). Add the interface definition under Card.Statistics." -->
> **SOURCE_GAP (GAP-003)** — The `StatisticsItemData` type body was not returned by the MCP (description ends with "where `StatisticsItemData` is:" with no body). The shape of each array item — required fields, optional fields, field types — is unknown. Consumers cannot use `Card.Statistics` without it.

## Theming

All sub-components (`Card`, `Card.Header`, `Card.Separator`) accept `theme: Partial<CardTheme>`; `Card.Statistics` accepts `theme: Partial<StatisticsTheme>`.

<!-- STUB:GAP-004 source="Locate CardTheme and StatisticsTheme interface definitions in the @8x8/oxygen-card source. Document the available theme keys in props and tokens." -->
> **SOURCE_GAP (GAP-004)** — The `CardTheme` and `StatisticsTheme` interface shapes were not returned by the MCP. Which CSS properties each theme object exposes is unknown from available sources.
