---
component: Card
package: "@8x8/oxygen-card"
category: layout_overlay
role: props
role_description: "API props reference — all component properties with types, defaults, and descriptions"
pipeline_stage: spec_ready
pipeline_note: "Audit verdict YES/PARTIAL — doc-rewrite can run"
audit_verdict: YES
files_present:
  - props
  - examples
  - tokens
  - accessibility
  - figma
  - audit
siblings:
  - "[[Card/examples]]"
  - "[[Card/tokens]]"
  - "[[Card/accessibility]]"
  - "[[Card/Card-figma]]"
  - "[[Card/Card-audit]]"
tags:
  - oxygen
  - component/Card
  - role/props
  - stage/spec_ready
  - category/layout_overlay
---
# Card — Props

> **See also:** [examples.md](examples.md) · [tokens.md](tokens.md) · [accessibility.md](accessibility.md)

> ⚠️ **DEPRECATED** — `@8x8/oxygen-card` is deprecated. The entire package including all sub-components (Card, Header, Separator, Statistics) has been marked deprecated. Consider using an alternative layout pattern.

## Installation

```sh
# yarn
$ yarn add @8x8/oxygen-card

# npm
$npm install @8x8/oxygen-card
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

> **DOC\_GAP** — The `StatisticsItemData` type definition was not returned by the MCP (description ends with "where `StatisticsItemData` is:" but includes no type body). The shape of each array item is unknown from available sources.

---

_Source: Oxygen MCP · Extracted 2026-05-05_
