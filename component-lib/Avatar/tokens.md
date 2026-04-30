# Avatar — Tokens

> **See also:** [props.md](./props.md) · [examples.md](./examples.md) · [accessibility.md](./accessibility.md)

---

## Avatar background tokens

Each colour variant has a paired background + text token. **Always use the matching pair** (same index number) — they are purpose-tuned for contrast.

| Token | Figma colour | Light value | Dark value | Palette ref (Light) |
|-------|-------------|-------------|------------|---------------------|
| `avatarBackground01` | Midnight | `#BAC6D9` | `#0B49AA` | `colorPalette.midnight09` |
| `avatarBackground02` | Teal | `#98CDC2` | `#17655A` | `colorPalette.teal09` |
| `avatarBackground03` | Pink | `#F9B5BE` | `#9B374F` | `colorPalette.pink10` |
| `avatarBackground04` | Magenta | `#E9BED4` | `#92306C` | `colorPalette.magenta10` |
| `avatarBackground05` | Violet | `#D1B9D8` | `#73348C` | `colorPalette.violet09` |
| `avatarBackground06` | External / n/a | `#57554E` | `#525252` | `colorPalette.offwhite04` |

---

## Avatar text tokens

| Token | Pair with | Light value | Dark value | Palette ref (Light) |
|-------|-----------|-------------|------------|---------------------|
| `avatarText01` | `avatarBackground01` | `#0D2A58` | `#D7E3F9` | `colorPalette.midnight01` |
| `avatarText02` | `avatarBackground02` | `#15342E` | `#E4F8ED` | `colorPalette.teal02` |
| `avatarText03` | `avatarBackground03` | `#5B2530` | `#FAEAEC` | `colorPalette.pink02` |
| `avatarText04` | `avatarBackground04` | `#562241` | `#FAEAEC` | `colorPalette.magenta03` |
| `avatarText05` | `avatarBackground05` | `#3A1F45` | `#FAEAEC` | `colorPalette.violet02` |
| `avatarText06` | `avatarBackground06` | `#F4F3EE` | `#F1F1F1` | `colorPalette.offwhite10` |

---

## Hover overlay token

| Token | Description | Light value | Dark value |
|-------|-------------|-------------|------------|
| `avatarHover` | Semi-transparent overlay applied on hover | `#29292926` (~15% gray02) | `#29292926` (same) |

---

## Status badge / presence ring tokens

Used by the `User status` badge and `_presence-ring` elements. Shared with the `UserStatus` component.

| Status | Token | Light value | Dark value |
|--------|-------|-------------|------------|
| Available | `statusAvailable01` | `#189B55` | `#189B55` |
| Away | `statusAway01` | `#DD7011` | `#DD7011` |
| Busy | `statusBusy01` | `#CB2233` | `#F24D5F` |
| Offline | `statusOffline01` | `#6C6862` | `#666666` |
| WrapUp | `statusWrapup01` | `#73348C` | `#8B559F` |

> **Note:** Tokens for `OnCall`, `DirectCall`, `DoNotDisturb`, `WorkingOffline`, `OnBreak` statuses
> were not returned by the MCP theme tokens endpoint. These statuses appear in Figma but their
> specific tokens are not confirmed.

---

## Interactive / structural tokens

| Usage | Token | Light value | Dark value |
|-------|-------|-------------|------------|
| Focus ring border | `focus01` (via `interactive/focus01`) | `#0056E0` | `#D7E3F9` |
| Focus ring inner gap / badge border | `ui06` (via `ui/ui06`) | `#FFFFFF` | `#171719` |

---

## Typography tokens (initials)

| Token | Value |
|-------|-------|
| `typography/heading01/font-family` | Inter, sans-serif |
| `typography/heading01/font-size` | 1.25rem (20px) |
| `typography/heading01/font-weight` | 600 (SemiBold) |
| `typography/heading01/line-height` | 1.75rem (28px) |
| `typography/heading01/letter-spacing` | -0.017rem |

> Typography is applied via CSS custom properties (`--typography/heading01/*`), fully tokenised.

---

## Hardcoded values (not tokenised)

| Element | Property | Value | Notes |
|---------|----------|-------|-------|
| All sizes | `width` / `height` | 24 / 32 / 40 / 48 / 80px | No dimension tokens; hardcoded per size |
| All variants | `border-radius` | `1000px` | Intentional pill; no token |
| Status badge | `border-radius` | `10px` | No token |
| Status badge | `border-width` | `3px` | No token (≈ spacing01 + 1px) |
| Presence ring | `border-width` | `2px` | No token (≈ `spacing01`) |
| Focus ring | `border-width` | `2px` | No token (≈ `spacing01`) |
| Focus ring gap | `box-shadow inset` | `4px` | No token |

---

_Source: Oxygen MCP · Extracted 2026-04-28_
