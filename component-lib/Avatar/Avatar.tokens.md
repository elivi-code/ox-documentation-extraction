---
parent: "[[Avatar]]"
section: tokens
component: Avatar
package: "@8x8/oxygen-avatar"
role: spoke
pipeline_stage: rewritten
audit_verdict: "NO"
tags: [oxygen, component/Avatar, role/spoke, spoke/tokens]
---

# Avatar — Tokens

---

## Background tokens

Each colour variant has a paired background + text token. **Always use the matching pair (same index number)** — they are purpose-tuned for contrast.

| Token | Figma colour | Light | Dark | Palette ref (Light) |
|---|---|---|---|---|
| [[token.color.avatarBackground01]] | Midnight | `#BAC6D9` | `#0B49AA` | `colorPalette.midnight09` |
| [[token.color.avatarBackground02]] | Teal | `#98CDC2` | `#17655A` | `colorPalette.teal09` |
| [[token.color.avatarBackground03]] | Pink | `#F9B5BE` | `#9B374F` | `colorPalette.pink10` |
| [[token.color.avatarBackground04]] | Magenta | `#E9BED4` | `#92306C` | `colorPalette.magenta10` |
| [[token.color.avatarBackground05]] | Violet | `#D1B9D8` | `#73348C` | `colorPalette.violet09` |
| [[token.color.avatarBackground06]] | External / n/a | `#57554E` | `#525252` | `colorPalette.offwhite04` |

---

## Text tokens (initials)

| Token | Pair with | Light | Dark | Palette ref (Light) |
|---|---|---|---|---|
| [[token.color.avatarText01]] | `avatarBackground01` | `#0D2A58` | `#D7E3F9` | `colorPalette.midnight01` |
| [[token.color.avatarText02]] | `avatarBackground02` | `#15342E` | `#E4F8ED` | `colorPalette.teal02` |
| [[token.color.avatarText03]] | `avatarBackground03` | `#5B2530` | `#FAEAEC` | `colorPalette.pink02` |
| [[token.color.avatarText04]] | `avatarBackground04` | `#562241` | `#FAEAEC` | `colorPalette.magenta03` |
| [[token.color.avatarText05]] | `avatarBackground05` | `#3A1F45` | `#FAEAEC` | `colorPalette.violet02` |
| [[token.color.avatarText06]] | `avatarBackground06` | `#F4F3EE` | `#F1F1F1` | `colorPalette.offwhite10` |

> **Pairing rule:** `avatarTextN` must only be used on `avatarBackgroundN` (same index).

---

## Hover overlay

| Token | Description | Light | Dark |
|---|---|---|---|
| [[token.color.avatarHover]] | Semi-transparent overlay applied on hover | `#29292926` (~15% gray02) | `#29292926` (same) |

---

## Status badge / presence ring tokens

Shared with the `UserStatus` component.

| Status | Token | Light | Dark |
|---|---|---|---|
| Available | [[token.color.statusAvailable01]] | `#189B55` | `#189B55` |
| Away | [[token.color.statusAway01]] | `#DD7011` | `#DD7011` |
| Busy | [[token.color.statusBusy01]] | `#CB2233` | `#F24D5F` |
| Offline | [[token.color.statusOffline01]] | `#6C6862` | `#666666` |
| WrapUp | [[token.color.statusWrapup01]] | `#73348C` | `#8B559F` |
| OnCall | (token not returned by MCP) | — | — |
| DirectCall | (token not returned by MCP) | — | — |
| DoNotDisturb | (token not returned by MCP) | — | — |
| WorkingOffline | (token not returned by MCP) | — | — |
| OnBreak | (token not returned by MCP) | — | — |

<!-- SKIP:GAP-006 manual="Query the UserStatus component token data or inspect the Figma file directly (Desktop Bridge) to find the missing 5 status tokens and add them to tokens.md — requires MCP/Desktop Bridge access" -->
<!-- SKIP:GAP-010 manual="Re-run extraction with Figma Desktop Bridge plugin open to obtain full figma_get_variables output and cross-check against MCP token data" -->

---

## Interactive / structural tokens

| Usage | Token | Light | Dark |
|---|---|---|---|
| Focus ring border | [[token.color.focus01]] (via `interactive/focus01`) | `#0056E0` | `#D7E3F9` |
| Focus ring inner gap / badge border | [[token.color.ui06]] (via `ui/ui06`) | `#FFFFFF` | `#171719` |

---

## Typography tokens (initials)

| Token | Value |
|---|---|
| `typography/heading01/font-family` | Inter, sans-serif |
| `typography/heading01/font-size` | 1.25rem (20px) |
| `typography/heading01/font-weight` | 600 (SemiBold) |
| `typography/heading01/line-height` | 1.75rem (28px) |
| `typography/heading01/letter-spacing` | -0.017rem |

> Typography is driven by CSS custom properties (`--typography/heading01/*`) — fully tokenised.

---

## Hardcoded values (not tokenised)

| Element | Property | Value |
|---|---|---|
| All sizes | `width` / `height` | 24 / 32 / 40 / 48 / 80px |
| All variants | `border-radius` | `1000px` (intentional pill) |
| Status badge | `border-radius` | `10px` |
| Status badge | `border-width` | `3px` |
| Presence ring | `border-width` | `2px` (≈ `spacing01`) |
| Focus ring | `border-width` | `2px` (≈ `spacing01`) |
| Focus ring gap | `box-shadow inset` | `4px` |
