---
component: Avatar
package: "@8x8/oxygen-avatar"
category: data_display
role: props
role_description: "API props reference — all component properties with types, defaults, and descriptions"
pipeline_stage: blocked
pipeline_note: "Audit verdict NO — resolve CONFLICTs before rewrite"
audit_verdict: NO
siblings:
  - "[[Avatar/examples]]"
  - "[[Avatar/tokens]]"
  - "[[Avatar/accessibility]]"
  - "[[Avatar/Avatar-figma]]"
  - "[[Avatar/Avatar-audit]]"
tags:
  - oxygen
  - component/Avatar
  - role/props
  - stage/blocked
  - category/data_display
---
# Avatar — Props

> **See also:** [examples.md](./examples.md) · [tokens.md](./tokens.md) · [accessibility.md](./accessibility.md)

---

## Installation

```sh
# yarn
yarn add @8x8/oxygen-avatar

# npm
npm install @8x8/oxygen-avatar
```

**Registry config required** (must be on 8x8 VPN):

```
# .npmrc
@8x8:registry=https://artifactory.es.8x8.com/artifactory/api/npm/npm-repository/
```

---

## Components in this package

| Component | Description |
|-----------|-------------|
| `Avatar` | Single user or entity avatar with optional status badge |
| `AvatarStack` | Stacked group of avatars (no props documented in MCP) |

---

## Avatar props

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `size` | `AvatarSize \| number` | `'medium'` | Named size or custom number. When a number is passed, `userStatus` and `showEditOverlay` are ignored |
| `name` | `string` | `''` | Name used to compute initials |
| `maxInitials` | `number` | `2` | Maximum number of initials to render |
| `src` | `string` | `''` | Image source URL for photo avatar |
| `imageProps` | `Omit<React.ComponentPropsWithRef<'img'>, 'src' \| 'alt'>` | `{}` | Extra props passed to the `<img>` element; only applied when `src` is provided |
| `children` | `ReactNode` | `null` | Custom content rendered inside the avatar — can be an Oxygen Icon, text, or anything |
| `userStatus` | `AvatarUserStatus \| React.ReactElement` | `null` | Status badge value or renderable element. Only available for sizes `2xsmall`–`2xlarge` |
| `hasStatusBorder` | `boolean` | `false` | Shows the status colour as a border ring around the avatar. Only active when `userStatus` is a valid string |
| `hasBorder` | `boolean` | `false` | Renders a border around the avatar |
| `isGroup` | `boolean` | `false` | Shows the group placeholder icon instead of user initials/photo |
| `isActive` | `boolean` | `false` | Shows the focus border ring |
| `showEditOverlay` | `boolean` | `false` | Shows the edit overlay on hover. Only available for sizes `l`–`3xl` |
| `onClick` | `(e?: React.MouseEvent<HTMLDivElement>) => void` | `noop` | Click handler |
| `onEdit` | `(e?: React.MouseEvent<HTMLDivElement>) => void` | `noop` | Edit overlay click handler |
| `testId` | `string` | `'AVATAR'` | `data-testid` DOM attribute value |

---

## AvatarSize values

| Token | px | rem | Figma name | Recommended use case |
|-------|----|-----|------------|---------------------|
| `2xsmall` | — | — | — | <!-- NOT CONFIRMED IN MCP --> |
| `xsmall` | 24 | 1.5 | xsmall | Top bar |
| `small` | 32 | 2 | small | Small cards |
| `medium` | 40 | 2.5 | medium | Small-width browsers |
| `large` | 48 | 3 | large | Wide browsers |
| `xlarge` | 80 | 5 | xlarge | Profile picture update |
| `2xlarge` | — | — | — | <!-- NOT CONFIRMED IN MCP --> |

> The full `AvatarSize` enum was not returned by the MCP. Values above `xsmall`–`xlarge` are
> inferred from Figma metadata. Sizes `2xsmall` and `2xlarge` are referenced in `userStatus`
> constraint docs but not present in the Figma component set.

---

## AvatarUserStatus values

From Figma atom variants. Full Oxygen enum not returned by MCP — values listed from Figma:

`Available` · `Away` · `Busy` · `OnCall` · `DirectCall` · `DoNotDisturb` · `WorkingOffline` · `OnBreak` · `Offline` · `WrapUp`

> Raw colour values also appear in Figma atom internals (`Gray`, `Green`, `Purple`, `Red`, `Yellow`) — these are likely internal design tokens, not public API values.

---

## Content fallback chain

When rendering user avatars, the component falls back in this order:

1. **Photo** — if `src` is provided and loads successfully
2. **Initials** — if `name` is provided; controlled by `maxInitials` (default: 2)
3. **Icon** — fallback when neither photo nor name is available

---

## Prop constraints

| Prop | Constraint |
|------|-----------|
| `userStatus` | Only available for sizes `2xsmall`–`2xlarge`. Ignored when `size` is a number. |
| `showEditOverlay` | Only available for sizes `l`–`3xl` |
| `hasStatusBorder` | Only active when `userStatus` is a valid `AvatarUserStatus` string (not a ReactElement) |
| `imageProps` | Only applied when `src` is provided |

---

_Source: Oxygen MCP · Extracted 2026-04-28_
