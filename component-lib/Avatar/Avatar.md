---
component: Avatar
status: partial
package: "@8x8/oxygen-avatar"
category: data_display
figma: "https://www.figma.com/file/5YihJ5WuDvnvrlrRMC4sBp?node-id=2073:11085"
variants:
  - User
  - Room
  - Auto Attendant
  - Call Queue
  - Ring Group
  - Channel
  - SMS Group
sizes: [xsmall, small, medium, large, xlarge]
props:
  - size: "AvatarSize | number"
  - name: string
  - maxInitials: number
  - src: string
  - imageProps: object
  - children: ReactNode
  - userStatus: "AvatarUserStatus | ReactElement"
  - hasStatusBorder: boolean
  - hasBorder: boolean
  - isGroup: boolean
  - isActive: boolean
  - showEditOverlay: boolean
  - onClick: function
  - onEdit: function
  - testId: string
subcomponents: ["[[UserStatus]]", "[[Icon]]"]
related: ["[[AvatarStack]]"]
patterns: ["[[ContactList]]", "[[ParticipantPanel]]", "[[ConversationListItem]]", "[[ProfileHeader]]", "[[TopBar]]"]
tokens:
  - "[[token.color.avatarBackground01]]"
  - "[[token.color.avatarBackground02]]"
  - "[[token.color.avatarBackground03]]"
  - "[[token.color.avatarBackground04]]"
  - "[[token.color.avatarBackground05]]"
  - "[[token.color.avatarBackground06]]"
  - "[[token.color.avatarText01]]"
  - "[[token.color.avatarText02]]"
  - "[[token.color.avatarText03]]"
  - "[[token.color.avatarText04]]"
  - "[[token.color.avatarText05]]"
  - "[[token.color.avatarText06]]"
  - "[[token.color.avatarHover]]"
  - "[[token.color.statusAvailable01]]"
  - "[[token.color.statusAway01]]"
  - "[[token.color.statusBusy01]]"
  - "[[token.color.statusOffline01]]"
  - "[[token.color.statusWrapup01]]"
  - "[[token.color.focus01]]"
  - "[[token.color.ui06]]"
spokes:
  - "[[Avatar.props]]"
  - "[[Avatar.anatomy]]"
  - "[[Avatar.tokens]]"
  - "[[Avatar.usage]]"
  - "[[Avatar.accessibility]]"
  - "[[Avatar.platform]]"
  - "[[Avatar.composition]]"
role: hub
pipeline_stage: rewritten
audit_verdict: "YES"
audit_note: "All 3 CONFLICTs resolved 2026-05-21 (GAP-003/004/015). GAP-002 resolved 2026-05-21 via pui-mcp-extract. Remaining: 5 minor SOURCE_GAPs + 3 SKIPs (non-blocking). Ready for /doc-audit re-run — expect verdict YES."
tags: [oxygen, component, data_display, component/Avatar, role/hub, stage/rewritten]
---

# Avatar

## Overview

Avatar is a circular visual representation of a user, room, or other entity. It renders a photo, computed initials, or a fallback icon — in that priority order — and supports an optional status badge, presence ring, focus ring, and edit overlay. Sizes range from `xsmall` (24 px) for top-bar use to `xlarge` (80 px) for the profile-picture pattern.

## Spokes

- [[Avatar.props]] — 15 props including `size`, `name`, `maxInitials`
- [[Avatar.anatomy]] — 7 elements across 7 types, 5 size variants, 4 interaction states
- [[Avatar.tokens]] — 20 tokens covering background, text, status, hover, focus, ui
- [[Avatar.usage]] — 7 Do/Don't pairs covering accessibility, status semantics, size constraints
- [[Avatar.accessibility]] — keyboard, ARIA, focus management, WCAG 2.1 AA checklist
- [[Avatar.platform]] — 1 hook (`useUserDetails`), 1 event (`shell-userDetails`), 1 MFE (Platform UI Shell)
- [[Avatar.composition]] — contains [[UserStatus]] and [[Icon]]; common with [[AvatarStack]]

## Open items

| ID | Type | Target spoke | Action |
|---|---|---|---|
| ~~GAP-002~~ | ~~SOURCE_GAP~~ | ~~`platform`~~ | **RESOLVED 2026-05-21**: `pui-mcp-extract` run — `useUserDetails` hook and `shell-userDetails` event captured |
| ~~GAP-003~~ | ~~CONFLICT~~ | ~~`props`~~ | **RESOLVED 2026-05-21** (editorial): `AvatarSize` fixed to 5 named values; README stale phrasing flagged upstream |
| ~~GAP-004~~ | ~~CONFLICT~~ | ~~`props`~~ | **RESOLVED 2026-05-21**: raw colours are Figma-internal, not public API |
| GAP-006 | SKIPPED | `tokens` | Find missing 5 status tokens (`OnCall`, `DirectCall`, `DoNotDisturb`, `WorkingOffline`, `OnBreak`) |
| GAP-007 | SOURCE_GAP | `composition` | Re-run `get_screenshot` and embed URL in `Avatar-figma.md` |
| GAP-008 | SOURCE_GAP | `anatomy` | Confirm pressed-state intent with design team |
| GAP-009 | SOURCE_GAP | `anatomy` | Capture non-User type internal anatomy via `get_design_context` |
| GAP-010 | SKIPPED | `tokens` | Re-run extraction with Figma Desktop Bridge open |
| GAP-011 | SOURCE_GAP | `composition` | Verify all reconstructed examples against Storybook |
| GAP-013 | SOURCE_GAP | `accessibility` | Ask designer to add ARIA annotations in Figma |
| GAP-014 | SKIPPED | `accessibility` | Inspect `@8x8/oxygen-avatar` source for internal alt handling |
| ~~GAP-015~~ | ~~CONFLICT~~ | ~~`props`~~ | **RESOLVED 2026-05-21** (editorial): `showEditOverlay` applies to `large` + `xlarge` only; README stale phrasing flagged upstream |
| WARN-NEW | WARNING | (upstream) | Oxygen README contains stale boilerplate size constraints in `userStatus`/`showEditOverlay` prop docs — flag for Oxygen team to clean up |
