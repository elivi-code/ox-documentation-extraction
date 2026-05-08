---
component: Button
package: "@8x8/oxygen-button"
category: interaction
role: props
role_description: "API props reference — all component properties with types, defaults, and descriptions"
pipeline_stage: blocked
pipeline_note: "Audit verdict NO — resolve CONFLICTs before rewrite"
audit_verdict: NO
siblings:
  - "[[Button/examples]]"
  - "[[Button/tokens]]"
  - "[[Button/accessibility]]"
  - "[[Button/Button-figma]]"
  - "[[Button/Button-audit]]"
tags:
  - oxygen
  - component/Button
  - role/props
  - stage/blocked
  - category/interaction
---
# Button — Props

> **See also:** [Examples](examples.md) · [Tokens](tokens.md) · [Accessibility](accessibility.md)

## Installation

**Package:** `@8x8/oxygen-button`

```bash
# yarn
yarn add @8x8/oxygen-button

# npm
npm install @8x8/oxygen-button
```

**Registry prerequisite** — add to `.npmrc` (VPN required):
```
@8x8:registry=https://artifactory.es.8x8.com/artifactory/api/npm/npm-repository/
```

Or for Yarn (`.yarnrc.yml`):
```yaml
npmScopes:
  8x8:
    npmRegistryServer: "https://artifactory.es.8x8.com/artifactory/api/npm/npm-repository/"

nodeLinker: node-modules
```

## Import

```tsx
import Button, { ButtonGroup, DropdownButton, IconButton } from '@8x8/oxygen-button';
```

---

## Button Props

| Prop | Type | Default | Required | Description |
|------|------|---------|----------|-------------|
| `children` | `ReactNode` | — | **yes** | Button content (label text or icon for circular) |
| `variant` | `ButtonVariant` | `'primary'` | no | Visual style variant (see Variants table below) |
| `size` | `ButtonSize` | `'medium'` | no | Button size. Use `'large'` for touch targets |
| `iconLeft` | `ReactNode` | — | no | Icon rendered on the left side of the label |
| `iconRight` | `ReactNode` | — | no | Icon rendered on the right side of the label |
| `isActive` | `boolean` | `false` | no | Active/pressed state |
| `isDisabled` | `boolean` | `false` | no | Disabled state — button is still focusable |
| `isCircular` | `boolean` | `false` | no | Circular shape. Use with a single `Icon` child |
| `isDestructive` | `boolean` | `false` | no | Destructive action styling |
| `testId` | `string` | `'BUTTON'` | no | Selector for automated testing |
| `theme` | `object` | `{}` | no | Per-instance theme customisation |
| `secondary` | `boolean` | — | no | **Deprecated** — use `variant="secondary"` instead |
| `hasShadow` | `boolean` | — | no | **Deprecated** |

### ButtonVariant values

| Value | Use case |
|-------|----------|
| `'primary'` | Default / most important action on a page or dialog |
| `'secondary'` | Alternative, less prominent action |
| `'tertiary'` | Control action (e.g. call controls). Use with `isCircular` |
| `'tertiaryReversed'` | Control action on inverted/dark backgrounds (e.g. in-call UI) |
| `'text'` | Low-priority action; no visible container in rest state |
| `'success'` | Positive call action (e.g. answer). Use with `isCircular` |
| `'destructive'` | Destructive control action (e.g. hang up). Use with `isCircular` |

### ButtonSize values

| Value | Notes |
|-------|-------|
| `'small'` | Compact layout |
| `'medium'` | Default |
| `'large'` | Recommended for touch targets |
| `'big'` | Extra large |

---

## ButtonGroup Props

| Prop | Type | Default | Required | Description |
|------|------|---------|----------|-------------|
| `spacing` | `'small' \| 'large'` | — | no | Gap between buttons |
| `align` | `'left' \| 'center' \| 'right'` | — | no | Horizontal alignment of buttons |

---

## DropdownButton Props

| Prop | Type | Default | Required | Description |
|------|------|---------|----------|-------------|
| `children` | `ReactNode` | — | no | Button label |
| `size` | `'small' \| 'medium' \| 'large'` | — | no | Button size |
| `isActive` | `boolean` | — | no | Active state |
| `isDisabled` | `boolean` | — | no | Disabled state |
| `fullWidth` | `boolean` | — | no | Full-width layout |
| `testId` | `string` | — | no | Selector for automated testing |

> Usually paired with `Popover` or `PopoverMenu` components.

---

## IconButton Props

| Prop | Type | Default | Required | Description |
|------|------|---------|----------|-------------|
| `children` | `ReactNode` | — | no | Icon child |
| `size` | `iconButtonSize` enum | — | no | Icon button size |
| `isInverted` | `boolean` | — | no | Inverted styling for dark backgrounds |

> Always pair `IconButton` with a `Tooltip` to provide an accessible text label.

---

_Source: Oxygen MCP · Extracted 2026-04-28_
