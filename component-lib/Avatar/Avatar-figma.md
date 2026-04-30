<!-- SOURCE: Figma MCP + Oxygen MCP -->
<!-- FILE KEY: 5YihJ5WuDvnvrlrRMC4sBp -->
<!-- NODE ID: 2073:11085 -->
<!-- EXTRACTED: 2026-04-28 -->
<!-- COMPONENT: Avatar -->
<!-- COLOR STRATEGY: A — one table per element; color-variant as row dimension -->

# Avatar — Figma Design Spec

> **See also:** [props.md](./props.md) · [tokens.md](./tokens.md) ·
> [examples.md](./examples.md) · [accessibility.md](./accessibility.md)

---

## Visual reference

![Avatar component set — all sizes, types, modes and states](figma-screenshot-avatar.png)

The component set shows a grid of all variants arranged by row (Mode: Light top / Dark bottom)
and column (Type × Size). The Atoms section beneath includes the full user-internal variant matrix
with Color, Content, State, and Status dimensions.

---

## Anatomy

The Avatar is a circular container that shows one of three content types (photo, initials, or icon)
with optional presence ring, focus ring, and status badge overlaid.

### Top-level component set structure

| # | Type | Name | Role | Notes |
|---|------|------|------|-------|
| 1 | frame | Avatar (component set) | Structural | Outer canvas; contains all variant symbols |
| 2 | symbol | Mode=*, Size=*, Type=* | Fixed variant | One symbol per Mode × Size × Type combination |

### User-internal atom (internal anatomy — single variant)

| # | Type | Name | Role | Notes |
|---|------|------|------|-------|
| 1 | frame | Avatar container | Structural | `border-radius: 1000px`; flex, center-align; size varies by Size variant |
| 2 | text | Initials | Content element | Shows computed initials; `typography/heading01`; controlled by `content=Initials` |
| 3 | image | Photo | Content element | User photo; controlled by `content=Photo` |
| 4 | instance | Icon | Content element | Fallback icon when no name or photo; controlled by `content=Icon` |
| 5 | frame | `_presence-ring` | Optional slot | Ring overlay showing status color; controlled by `hasStatusRing` boolean |
| 6 | frame | `Focus ring` | Optional slot | Focus border overlay; controlled by `focused` boolean |
| 7 | frame | `User status` (badge) | Optional slot | Bottom-right status badge; controlled by `hasStatus` boolean; see UserStatus docs |

### Sub-component: User status badge

| # | Type | Name | Role | Notes |
|---|------|------|------|-------|
| 1 | frame | User status | Structural | `border-radius: 10px`; positioned `inset: 58.33% 0 0 58.33%` (bottom-right) |
| 2 | image | Vector 1 (Stroke) | Content | Status icon SVG; changes per status value |

### Sub-component: Presence ring

| # | Type | Name | Role | Notes |
|---|------|------|------|-------|
| 1 | frame | `_presence-ring` | Structural | Full-size overlay; `border-2`; color = status token |
| 2 | div | Inner shadow | Structural/decorative | `inset 0 0 0 4px white`; creates separation gap between ring and avatar |

### Sub-component: Focus ring

| # | Type | Name | Role | Notes |
|---|------|------|------|-------|
| 1 | frame | Focus ring | Structural | `border-2`; color = `interactive/focus01`; full-size inset overlay |
| 2 | div | Inner shadow | Structural/decorative | `inset 0 0 0 4px ui/ui06`; creates white gap |

### Non-user types (Room, Auto Attendant, Call Queue, Ring Group, Channel, SMS Group)

These types use a simpler internal structure — a flat circular container with a pre-rendered icon,
no Color, Content, State, or Status variant axes. They are nested as `_user-external` or type-specific
atoms inside the `_user` wrapper.

---

## API — Component properties

### Variant axes (Figma component set — top level)

| Property | Values | Default | Notes |
|----------|--------|---------|-------|
| Mode | `Light`, `Dark` | `Light` | Maps to color mode |
| Size | `xsmall`, `small`, `medium`, `large`, `xlarge` | `medium` | See sizes table |
| Type | `User`, `Room`, `Auto Attendant`, `Call Queue`, `Ring Group`, `Channel`, `SMS Group` | `User` | Entity type represented |

### Variant axes (Figma user-internal atom — detailed)

| Property | Values | Default | Notes |
|----------|--------|---------|-------|
| Mode | `Light`, `Dark` | `Light` | |
| Size | `large`, `medium`, `small` | `large` | Atom-level; maps to top-level sizes |
| State | `Rest`, `Hover` | `Rest` | Transient — see interaction states |
| Color | `Midnight`, `Teal`, `Pink`, `Magenta`, `Violet`, `n/a` | `Midnight` | Background color family |
| Content | `Initials`, `Photo`, `Icon` | `Initials` | Avatar content type |
| Status | `Available`, `Away`, `Busy`, `OnCall`, `DirectCall`, `DoNotDisturb`, `WorkingOffline`, `OnBreak`, `Offline`, `WrapUp`, `Gray`, `Green`, `Purple`, `Red`, `Yellow` | `Available` | UserStatus badge value |
| focused | `true`, `false` | `false` | Persistent interactive state |
| hasStatus | `true`, `false` | `true` | Toggle status badge visibility |
| hasStatusRing | `true`, `false` | `false` | Toggle presence ring border |

### Oxygen API props (package: `@8x8/oxygen-avatar`)

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `size` | `AvatarSize \| number` | `'medium'` | Named size or custom number (number disables UserStatus and EditOverlay) |
| `name` | `string` | `''` | Name to compute initials from |
| `maxInitials` | `number` | `2` | Maximum initials to render |
| `src` | `string` | `''` | Photo image source |
| `imageProps` | `Omit<HTMLProps, 'src' \| 'alt'>` | `{}` | Extra props for `<img>` element; only used when `src` is provided |
| `children` | `ReactNode` | `null` | Custom content override (icon, text, anything) |
| `userStatus` | `AvatarUserStatus \| ReactElement` | `null` | Status badge; available only for sizes `2xsmall`–`2xlarge` |
| `hasStatusBorder` | `boolean` | `false` | Status color shown as border ring (requires valid `userStatus` string) |
| `isGroup` | `boolean` | `false` | Use group placeholder icon |
| `hasBorder` | `boolean` | `false` | Render border around avatar |
| `isActive` | `boolean` | `false` | Show focus border |
| `showEditOverlay` | `boolean` | `false` | Show edit overlay; available only for sizes `l`–`3xl` |
| `onClick` | `(e?) => void` | `noop` | Click handler |
| `onEdit` | `(e?) => void` | `noop` | Edit overlay click handler |
| `testId` | `string` | `'AVATAR'` | Test ID DOM attribute |

### Boolean toggles (Figma)

| Property | Default | Notes |
|----------|---------|-------|
| `hasStatus` | `true` | Shows/hides the status badge (`User status` layer) |
| `hasStatusRing` | `false` | Shows/hides the presence ring (`_presence-ring` layer) |
| `focused` | `false` | Shows/hides the focus ring (`Focus ring` layer) |

### Persistent states

| State | Figma property | Oxygen prop | Notes |
|-------|---------------|-------------|-------|
| Active / focused | `focused=true` | `isActive=true` | Shows blue focus ring border |
| Has status | `hasStatus=true` | `userStatus={...}` | Shows status badge |
| Has status border/ring | `hasStatusRing=true` | `hasStatusBorder=true` | Shows colored ring around avatar |

### Token coverage

- **Coverage:** High — all background colors, text colors, status badge colors, focus ring, and hover overlay are tokenised.
- **Hardcoded values flagged:**
  - `User status.border-radius`: `10px` — hardcoded; no token mapping found
  - `_presence-ring.border-width`: `2px` — hardcoded; maps conceptually to `spacing01` (2px)
  - `Focus ring.border-width`: `2px` — hardcoded; maps conceptually to `spacing01` (2px)
  - `User status.border-width`: `3px` — hardcoded; no token found
  - Avatar container `border-radius`: `1000px` — hardcoded pill value (intentional; no token)

---

## Color & token bindings

<!-- COLOR STRATEGY A: one table per element, color-variant as rows, mode as columns -->

### Avatar background

| Color variant | Token | Light | Dark |
|---------------|-------|-------|------|
| Midnight (default) | `avatarBackground01` | `#BAC6D9` (midnight09) | `#0B49AA` (midnight04) |
| Teal | `avatarBackground02` | `#98CDC2` (teal09) | `#17655A` (teal04) |
| Pink | `avatarBackground03` | `#F9B5BE` (pink10) | `#9B374F` (pink04) |
| Magenta | `avatarBackground04` | `#E9BED4` (magenta10) | `#92306C` (magenta05) |
| Violet | `avatarBackground05` | `#D1B9D8` (violet09) | `#73348C` (violet05) |
| External / n/a | `avatarBackground06` | `#57554E` (offwhite04) | `#525252` (gray04) |

### Initials text

| Color variant | Token | Light | Dark |
|---------------|-------|-------|------|
| Midnight | `avatarText01` | `#0D2A58` (midnight01) | `#D7E3F9` (blue10) |
| Teal | `avatarText02` | `#15342E` (teal02) | `#E4F8ED` (green10) |
| Pink | `avatarText03` | `#5B2530` (pink02) | `#FAEAEC` (red10) |
| Magenta | `avatarText04` | `#562241` (magenta03) | `#FAEAEC` (red10) |
| Violet | `avatarText05` | `#3A1F45` (violet02) | `#FAEAEC` (red10) |
| External / n/a | `avatarText06` | `#F4F3EE` (offwhite10) | `#F1F1F1` (gray10) |

> **Pairing rule:** `avatarTextN` must only be used on `avatarBackgroundN` (same index). These are purpose-paired for contrast.

### Hover overlay

| Element | Token | Light | Dark |
|---------|-------|-------|------|
| Avatar container (hover) | `avatarHover` | `#29292926` (gray02 @ ~15%) | `#29292926` (same) |

### Focus ring

| Element | Token | Light | Dark |
|---------|-------|-------|------|
| Focus ring border | `interactive/focus01` | `#0056E0` (blue05) | `#D7E3F9` (blue10) |
| Focus ring inner gap | `ui/ui06` | `#FFFFFF` (white) | `#171719` (purple01) |

### Presence ring

| Status | Token | Light | Dark |
|--------|-------|-------|------|
| Available | `status/statusAvailable01` | `#189B55` (green04) | `#189B55` (green04) |
| Away | `status/statusAway01` | `#DD7011` (orange06) | `#DD7011` (orange06) |
| Busy | `status/statusBusy01` | `#CB2233` (red05) | `#F24D5F` (red07) |
| Offline | `status/statusOffline01` | `#6C6862` (offwhite05) | `#666666` (gray05) |
| WrapUp | `status/statusWrapup01` | `#73348C` (violet05) | `#8B559F` (violet06) |

### Status badge

| Element | Token | Light | Dark |
|---------|-------|-------|------|
| Badge background | Same as presence ring — `status/status*01` | see above | see above |
| Badge border (separation gap) | `ui/ui06` | `#FFFFFF` | `#171719` |

### Text styles

| Element | Style name / token | Size | Weight | Line height | Letter spacing |
|---------|------------|------|--------|-------------|---------------|
| Initials | `typography/heading01` | 1.25rem (20px) | 600 (SemiBold) | 1.75rem (28px) | -0.017rem |

> **Note:** Typography is driven by CSS variable tokens (`--typography/heading01/font-family`, etc.) — all tokenised.

### Effect styles

<!-- NO EFFECT STYLES FOUND ON AVATAR COMPONENT IN FIGMA RESPONSE -->

---

## Structure & spacing

### Container sizes

| Size name | Token | px | rem | Use case |
|-----------|-------|----|-----|---------|
| xsmall | — | 24 | 1.5 | Top bar |
| small | — | 32 | 2 | Small cards |
| medium | — | 40 | 2.5 | Small-width browsers |
| large | — | 48 | 3 | Wide browsers |
| xlarge | — | 80 | 5 | Profile picture update |

> Sizes are hardcoded px values in Figma. No dimension tokens found — flag for token consideration.

### Shape

| Property | Value | Token |
|----------|-------|-------|
| Border radius | `1000px` | — (intentional pill value; no token) |

### Status badge position and size

| Property | Value | Token |
|----------|-------|-------|
| Position | `inset: 58.33% 0 0 58.33%` | — (percentage-based, relative to container) |
| Border radius | `10px` | — (hardcoded) |
| Border width | `3px` | — (hardcoded) |
| Border color | `ui/ui06` | ✓ |

### Presence ring

| Property | Value | Token |
|----------|-------|-------|
| Border width | `2px` | — (hardcoded; ≈ `spacing01`) |
| Inner shadow gap | `4px` (inset shadow) | — (hardcoded) |
| Size | Matches container (100%) | — |

### Focus ring

| Property | Value | Token |
|----------|-------|-------|
| Border width | `2px` | — (hardcoded) |
| Inner shadow gap | `4px` (inset shadow) | — (hardcoded) |
| Size | Matches container (inset 0) | — |

### Auto-layout

- Direction: column (vertical flex)
- Alignment: center / center
- Sizing: fixed × fixed per size variant (no auto-sizing)

### Density / size variants

No density variants — Avatar uses discrete named sizes only (see container sizes above).

---

## Interaction states

| State | Trigger | Visual change |
|-------|---------|---------------|
| hover | pointer over | `avatarHover` overlay (`#29292926`) applied on top of avatar background |
| focus | keyboard tab / `isActive=true` | Focus ring border (`interactive/focus01`) replaces or overlays presence ring |
| pressed | pointer down | <!-- NOT FOUND IN FIGMA RESPONSE — no pressed variant in metadata --> |

> **Important behaviour:** When an avatar has a presence ring (`hasStatusRing=true`) and receives keyboard focus, the **presence ring border is replaced by the focus ring**. They do not stack simultaneously.

---

## Design decisions & annotations

> **Mode=Light, Size=xlarge, State=Rest, Saved=False (node 30485:71525):** "External users, not saved in the 8x8 Contact Directory"

> **Avatar documentation link (node 30485:70564):** https://oxygen.8x8.com/components/avatar/usage

> **user node (node 85729:18982):** "user · person · single" — classification annotation for the User type

> **User status sub-component (node 2653:15515):** Referenced via https://oxygen.8x8.com/components/userstatus/usage — the badge is a standalone component with its own spec.

> **Oxygen usage docs:** "By default if the app does not have an image for that user or group the app shows the users initials. If the app does not have initials for the user the product shows an icon." — defines the fallback chain: photo → initials → icon.

> **Presence options (from Oxygen usage):** "When presence is used there are 2 options. One is with just the presence component and the other is to add the status color to the border of the avatar component. This is an optional enhancement the designer can use."

---

## Accessibility (from Figma annotations only)

- **ARIA role:** <!-- NOT ANNOTATED IN FIGMA -->
- **Focus order:** Focus ring shown when `isActive=true` or keyboard tab — ring style replaces presence ring border
- **Keyboard interactions:** <!-- NOT ANNOTATED IN FIGMA — see accessibility.md for full spec -->

> **Gap:** No explicit ARIA role, label, or screen-reader annotation found in Figma. Full accessibility spec should be authored in `accessibility.md`.

---

## Gaps & conflicts

| Type | Description |
|------|-------------|
| Missing annotation | No ARIA role annotated on Avatar or any variant in Figma |
| Missing annotation | No screen-reader label guidance in Figma (how to announce avatar name/status) |
| Missing annotation | No pressed/active interaction state variant in Figma component set |
| Missing token | Container dimensions (24/32/40/48/80px) have no dimension tokens — hardcoded px values |
| Missing token | Status badge `border-radius: 10px` is hardcoded |
| Missing token | Status badge `border-width: 3px` is hardcoded |
| Missing token | Presence ring `border-width: 2px` is hardcoded (≈ spacing01) |
| Missing token | Focus ring `border-width: 2px` is hardcoded (≈ spacing01) |
| Missing token | Focus ring inner shadow `4px` is hardcoded |
| Missing token | Avatar container `border-radius: 1000px` is hardcoded (intentional — confirm with design) |
| Incomplete data | figma-console tools unavailable (Desktop Bridge not open) — `figma_get_variables`, `figma_get_styles`, `figma_get_component_details` all failed |
| Incomplete data | No `get_design_context` data for non-User types (Room, Auto Attendant, etc.) — internal anatomy assumed similar from metadata |
| Conflict | Figma `Size` axis uses `xsmall/small/medium/large/xlarge`; Oxygen API uses `AvatarSize` (names like `2xsmall`, `2xlarge` mentioned in userStatus constraint) — full enum mapping not confirmed |
| Conflict | Figma shows `Status` values including raw colors (`Gray`, `Green`, `Purple`, `Red`, `Yellow`) — these may be internal atom values not exposed in the public Oxygen `AvatarUserStatus` enum; needs verification |

---

_Source: Figma MCP (`mcp__claude_ai_Figma`) · Oxygen MCP (`mcp__oxygen-mcp`) · Extracted 2026-04-28_
