---
parent: "[[Avatar]]"
section: composition
component: Avatar
package: "@8x8/oxygen-avatar"
role: spoke
pipeline_stage: rewritten
audit_verdict: "NO"
tags: [oxygen, component/Avatar, role/spoke, spoke/composition]
---

# Avatar — Composition

How Avatar combines with sub-components, sibling components, and broader patterns.

---

## Subcomponents (rendered inside Avatar)

| Component | Role |
|---|---|
| [[UserStatus]] | Status badge rendered as the `User status` slot when `userStatus` is set. Standalone component with its own spec. |
| [[Icon]] | Fallback content when `src` and `name` are absent; also valid as `children` for custom content. |

---

## Sibling components (used alongside)

| Component | Relationship |
|---|---|
| [[AvatarStack]] | Wraps multiple `Avatar` instances with overlap and "+N" overflow. Exported from the same package (`@8x8/oxygen-avatar`); MCP returned no prop data — see Storybook. |

---

## Common patterns

Avatar is a building block for these patterns (dead wikilinks are intentional — these pages may not exist yet):

- [[ContactList]] — vertical list of users with photo/initials + presence.
- [[ParticipantPanel]] — call/meeting participants grid using `AvatarStack` or per-row `Avatar`.
- [[ConversationListItem]] — Avatar + name + last message preview.
- [[ProfileHeader]] — `xlarge` avatar with `showEditOverlay` for profile picture management.
- [[TopBar]] — current-user avatar at `xsmall` size as an account menu trigger.

---

## Content composition

Avatar resolves its content via the fallback chain `photo → initials → icon`. Override with `children` for custom content:

```tsx
<Avatar size="medium">
  <SomeIcon />
</Avatar>
```

---

## Layering rules

| Layer | Controlled by | Notes |
|---|---|---|
| Avatar background | `Color` variant (or default Midnight) | One of 6 colour families. |
| Avatar content | `src` / `name` / `children` | Photo > initials > icon fallback. |
| Hover overlay | pointer over | Adds `avatarHover` overlay; not stackable with other content. |
| Presence ring | `hasStatusBorder=true` + valid string `userStatus` | Renders as colour ring around the avatar. |
| Focus ring | `isActive=true` or keyboard focus | Replaces presence ring when both are active. |
| Status badge | `userStatus` set | Bottom-right; can coexist with presence ring. |
| Edit overlay | `showEditOverlay=true` + size ≥ `large` | Hover affordance; silently ignored below `large`. |

---

## Non-User types

`Room`, `Auto Attendant`, `Call Queue`, `Ring Group`, `Channel`, `SMS Group` use the simpler non-User anatomy — no Color/Content/Status axes, just a type-specific icon inside the circular container.

<!-- STUB:GAP-011 source="Flag all examples in examples.md as 'unverified reconstruction'; verify each example against Storybook or live package before doc-rewrite — composition patterns above are sourced from props/figma metadata, not verified runnable code" -->
<!-- STUB:GAP-007 source="Re-run get_screenshot and embed the returned image URL in Avatar-figma.md visual reference section" -->
