---
parent: "[[Avatar]]"
section: props
component: Avatar
package: "@8x8/oxygen-avatar"
role: spoke
pipeline_stage: rewritten
audit_verdict: "NO"
tags: [oxygen, component/Avatar, role/spoke, spoke/props]
---

# Avatar — Props

## Avatar props

| Name | Type | Default | Required | Description | Accepts |
|---|---|---|---|---|---|
| `size` | `AvatarSize \| number` | `"medium"` | false | Named size or custom number. When a number is passed, `userStatus` and `showEditOverlay` are ignored. | — |
| `name` | `string` | `""` | false | Name used to compute initials. | — |
| `maxInitials` | `number` | `2` | false | Maximum number of initials to render. | — |
| `src` | `string` | `""` | false | Image source URL for photo avatar. | — |
| `imageProps` | `Omit<React.ComponentPropsWithRef<'img'>, 'src' \| 'alt'>` | `{}` | false | Extra props passed to the `<img>` element; only applied when `src` is provided. | — |
| `children` | `ReactNode` | `null` | false | Custom content rendered inside the avatar — can be an Oxygen Icon, text, or anything. | [[Icon]] |
| `userStatus` | `AvatarUserStatus \| React.ReactElement` | `null` | false | Status badge value or renderable element. Available for all named sizes (`xsmall`–`xlarge`); ignored when `size` is a custom number. | [[UserStatus]] |
| `hasStatusBorder` | `boolean` | `false` | false | Shows the status colour as a border ring. Only active when `userStatus` is a valid `AvatarUserStatus` string. | — |
| `hasBorder` | `boolean` | `false` | false | Renders a border around the avatar. | — |
| `isGroup` | `boolean` | `false` | false | Shows the group placeholder icon instead of initials/photo. | — |
| `isActive` | `boolean` | `false` | false | Shows the focus border ring. | — |
| `showEditOverlay` | `boolean` | `false` | false | Shows the edit overlay on hover. Available on `large` and `xlarge` only; silently ignored at smaller sizes. | — |
| `onClick` | `(e?: React.MouseEvent<HTMLDivElement>) => void` | `noop` | false | Click handler. | — |
| `onEdit` | `(e?: React.MouseEvent<HTMLDivElement>) => void` | `noop` | false | Edit overlay click handler. | — |
| `testId` | `string` | `"AVATAR"` | false | `data-testid` DOM attribute value. | — |

<!-- RESOLVED:GAP-003 date="2026-05-21" resolution="Editorial decision: AvatarSize = xsmall|small|medium|large|xlarge (5 values). The Oxygen README userStatus constraint phrasing referencing 2xsmall/2xlarge is stale boilerplate from a generic Oxygen size scaffold; Figma component set + public Sizes table both define 5 sizes only. Flag README phrasing for upstream fix." -->
<!-- RESOLVED:GAP-004 date="2026-05-21" resolution="Raw colour values (Gray, Green, Purple, Red, Yellow) confirmed as internal Figma atom variants; not part of public AvatarUserStatus type per Oxygen MCP README." -->
<!-- RESOLVED:GAP-015 date="2026-05-21" resolution="Editorial decision: showEditOverlay applies to large and xlarge only. README phrasing 'l–3xl' is stale boilerplate (no l or 3xl size exists in this component); flag for upstream fix." -->

---

## AvatarSize values

```ts
type AvatarSize = 'xsmall' | 'small' | 'medium' | 'large' | 'xlarge'
```

| Token | px | rem | Figma name | Recommended use case |
|---|---|---|---|---|
| `xsmall` | 24 | 1.5 | xsmall | Top bar |
| `small` | 32 | 2 | small | Small cards |
| `medium` | 40 | 2.5 | medium | Small-width browsers (default) |
| `large` | 48 | 3 | large | Wide browsers |
| `xlarge` | 80 | 5 | xlarge | Profile picture update |

---

## AvatarUserStatus values

Public semantic values:

`Available` · `Away` · `Busy` · `OnCall` · `DirectCall` · `DoNotDisturb` · `WorkingOffline` · `OnBreak` · `Offline` · `WrapUp`

The raw colour names (`Gray`, `Green`, `Purple`, `Red`, `Yellow`) that appear in the Figma atom's `Status` axis are **internal atom variants**, not values of the public `AvatarUserStatus` type. Do not pass them as `userStatus`.

---

## AvatarStack

`AvatarStack` is exported from `@8x8/oxygen-avatar` but its props were not returned by the Oxygen MCP. Refer to Storybook (https://oxygen.8x8.com/components/avatar/usage) for the current API.

---

## Content fallback chain

1. **Photo** — if `src` is provided and loads successfully.
2. **Initials** — if `name` is provided; controlled by `maxInitials`.
3. **Icon** — fallback when neither photo nor name is available.

---

## Prop constraints

| Prop | Constraint |
|---|---|
| `userStatus` | Available for all named sizes (`xsmall`–`xlarge`). Ignored when `size` is a custom number. |
| `showEditOverlay` | Available on `large` and `xlarge` only. Silently ignored at smaller sizes and when `size` is a custom number. |
| `hasStatusBorder` | Only active when `userStatus` is a valid `AvatarUserStatus` string (not a ReactElement). |
| `imageProps` | Only applied when `src` is provided. |
