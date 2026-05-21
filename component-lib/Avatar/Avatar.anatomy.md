---
parent: "[[Avatar]]"
section: anatomy
component: Avatar
package: "@8x8/oxygen-avatar"
role: spoke
pipeline_stage: rewritten
audit_verdict: "NO"
tags: [oxygen, component/Avatar, role/spoke, spoke/anatomy]
---

# Avatar — Anatomy

A circular container that renders one of three content types (photo, initials, or icon) with optional presence ring, focus ring, and status badge overlaid.

---

## Top-level component set

| # | Type | Name | Role | Notes |
|---|---|---|---|---|
| 1 | frame | Avatar (component set) | Structural | Outer canvas; contains all variant symbols. |
| 2 | symbol | Mode=*, Size=*, Type=* | Fixed variant | One symbol per Mode × Size × Type combination. |

---

## User-internal atom

| # | Type | Name | Role | Notes |
|---|---|---|---|---|
| 1 | frame | Avatar container | Structural | `border-radius: 1000px`; flex, center-align; size varies by Size variant. |
| 2 | text | Initials | Content | Computed initials; `typography/heading01`; controlled by `content=Initials`. |
| 3 | image | Photo | Content | User photo; controlled by `content=Photo`. |
| 4 | instance | Icon | Content | Fallback icon when no name or photo; controlled by `content=Icon`. |
| 5 | frame | `_presence-ring` | Optional slot | Ring overlay showing status colour; controlled by `hasStatusRing`. |
| 6 | frame | `Focus ring` | Optional slot | Focus border overlay; controlled by `focused`. |
| 7 | frame | `User status` (badge) | Optional slot | Bottom-right status badge; controlled by `hasStatus`; see [[UserStatus]]. |

---

## Sub-component: User status badge

| # | Type | Name | Role | Notes |
|---|---|---|---|---|
| 1 | frame | User status | Structural | `border-radius: 10px`; positioned `inset: 58.33% 0 0 58.33%` (bottom-right). |
| 2 | image | Vector 1 (Stroke) | Content | Status icon SVG; changes per status value. |

---

## Sub-component: Presence ring

| # | Type | Name | Role | Notes |
|---|---|---|---|---|
| 1 | frame | `_presence-ring` | Structural | Full-size overlay; `border-2`; colour = status token. |
| 2 | div | Inner shadow | Structural | `inset 0 0 0 4px white`; creates separation gap between ring and avatar. |

---

## Sub-component: Focus ring

| # | Type | Name | Role | Notes |
|---|---|---|---|---|
| 1 | frame | Focus ring | Structural | `border-2`; colour = `interactive/focus01`; full-size inset overlay. |
| 2 | div | Inner shadow | Structural | `inset 0 0 0 4px ui/ui06`; creates white gap. |

---

## Non-user types

`Room`, `Auto Attendant`, `Call Queue`, `Ring Group`, `Channel`, `SMS Group` use a simpler internal structure — a flat circular container with a pre-rendered icon, no Color, Content, State, or Status variant axes. They are nested as `_user-external` or type-specific atoms inside the `_user` wrapper.

<!-- STUB:GAP-009 source="Run get_design_context on at least one non-User type variant to capture its internal layer structure" -->

---

## Variant axes (top level)

| Property | Values | Default |
|---|---|---|
| Mode | `Light`, `Dark` | `Light` |
| Size | `xsmall`, `small`, `medium`, `large`, `xlarge` | `medium` |
| Type | `User`, `Room`, `Auto Attendant`, `Call Queue`, `Ring Group`, `Channel`, `SMS Group` | `User` |

## Variant axes (user-internal atom)

| Property | Values | Default |
|---|---|---|
| Mode | `Light`, `Dark` | `Light` |
| Size | `large`, `medium`, `small` | `large` |
| State | `Rest`, `Hover` | `Rest` |
| Color | `Midnight`, `Teal`, `Pink`, `Magenta`, `Violet`, `n/a` | `Midnight` |
| Content | `Initials`, `Photo`, `Icon` | `Initials` |
| Status | `Available`, `Away`, `Busy`, `OnCall`, `DirectCall`, `DoNotDisturb`, `WorkingOffline`, `OnBreak`, `Offline`, `WrapUp`, `Gray`, `Green`, `Purple`, `Red`, `Yellow` | `Available` |
| focused | `true`, `false` | `false` |
| hasStatus | `true`, `false` | `true` |
| hasStatusRing | `true`, `false` | `false` |

---

## Interaction states

| State | Trigger | Visual change |
|---|---|---|
| Rest | default | Base avatar appearance. |
| Hover | pointer over | `avatarHover` overlay (`#29292926`) applied on top of avatar background. |
| Focus | keyboard tab / `isActive=true` | Focus ring border (`interactive/focus01`) replaces or overlays presence ring. |
| Pressed | pointer down | Not defined in Figma. |

<!-- STUB:GAP-008 source="Confirm with design team whether a pressed state is intended; if not, document explicitly as 'not designed' in interaction states" -->

> **Important behaviour:** When an avatar has a presence ring (`hasStatusRing=true`) and receives keyboard focus, the **presence ring border is replaced by the focus ring**. They do not stack simultaneously.

---

## Container sizes

| Size | px | rem | Use case |
|---|---|---|---|
| xsmall | 24 | 1.5 | Top bar |
| small | 32 | 2 | Small cards |
| medium | 40 | 2.5 | Small-width browsers |
| large | 48 | 3 | Wide browsers |
| xlarge | 80 | 5 | Profile picture update |

> Sizes are hardcoded px values in Figma. No dimension tokens exist.

---

## Shape and badge geometry

| Property | Value | Token |
|---|---|---|
| Avatar `border-radius` | `1000px` | — (intentional pill; no token) |
| Status badge position | `inset: 58.33% 0 0 58.33%` | — |
| Status badge `border-radius` | `10px` | — (hardcoded) |
| Status badge `border-width` | `3px` | — (hardcoded) |
| Status badge `border-color` | `ui/ui06` | ✓ |
| Presence ring `border-width` | `2px` | — (≈ `spacing01`) |
| Presence ring inner shadow gap | `4px` | — (hardcoded) |
| Focus ring `border-width` | `2px` | — (≈ `spacing01`) |
| Focus ring inner shadow gap | `4px` | — (hardcoded) |

---

## Auto-layout

- Direction: column (vertical flex).
- Alignment: center / center.
- Sizing: fixed × fixed per size variant (no auto-sizing).
- No density variants — discrete named sizes only.
