---
component: Link
package: "@8x8/oxygen-link"
category: navigation
role: props
role_description: "API props reference — all component properties with types, defaults, and descriptions"
pipeline_stage: blocked
pipeline_note: "Audit verdict NO — resolve CONFLICTs before rewrite"
audit_verdict: NO
siblings:
  - "[[Link/examples]]"
  - "[[Link/tokens]]"
  - "[[Link/accessibility]]"
  - "[[Link/Link-figma]]"
  - "[[Link/Link-usage]]"
  - "[[Link/Link-audit]]"
tags:
  - oxygen
  - component/Link
  - role/props
  - stage/blocked
  - category/navigation
---
# Link — Props

> **See also:** [examples.md](examples.md) · [tokens.md](tokens.md) · [accessibility.md](accessibility.md)

## Installation

```bash
# yarn
$ yarn add @8x8/oxygen-link

# npm
$ npm install @8x8/oxygen-link
```

> **Registry prerequisite:** Add `@8x8:registry=https://artifactory.es.8x8.com/artifactory/api/npm/npm-repository/` to `.npmrc` (npm) or configure `npmScopes` in `.yarnrc.yml` (yarn). VPN connection to 8x8 required.

## Import

```tsx
import { Link } from '@8x8/oxygen-link';
```

## Description

`Link` is a wrapper around the HTML `<a>` element. It provides two main variants:

- **Inline** (default) — integrates with surrounding text content, adopting the typography and text style of its context.
- **Standalone** — offers enhanced typography and spacing controls, typically uses the `$body02` token.

Both variants support icons and chat-specific styling.

## Props

| Prop | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| `children` | `ReactNode` | No | — | Link label content |
| `icon` | `ReactNode` | No | — | Icon element rendered alongside the link label |
| `isChat` | `boolean` | No | `false` | Applies chat-surface color tokens (`$action05`/`$action07` depending on surface) |
| `standalone` | `false` | No | `false` | Constrains to inline variant; type `false` indicates standalone mode is resolved via a separate component variant |
| `size` | `never` | No | — | Not applicable to the inline variant |
| `testId` | `string` | No | — | `data-testid` attribute for automated testing |

> **Note:** `Link` forwards a ref to the underlying `<HTMLAnchorElement>` and accepts all standard HTML anchor attributes (`href`, `target`, `rel`, `aria-label`, etc.) via prop spread.

> **Data gap:** The `standalone` prop type is `false` and `size` is `never` in the MCP response, suggesting a discriminated union type where standalone mode is expressed differently (possibly a separate export or prop combination). Confirm with source code.

## Variants

| Variant | Description |
|---------|-------------|
| Inline | Default. Inherits surrounding typography size and style. No explicit `size` control. |
| Standalone | Separated from body content. Uses `$body02` typography. |

## States

| State | Description |
|-------|-------------|
| Rest | Default appearance |
| Hover | Visual feedback on hover |
| Active | Press/click state |
| Focus | Keyboard focus ring |
| Visited | Distinct visited color (`$textColor08`) |

_Source: Oxygen MCP · Extracted 2026-05-01_
