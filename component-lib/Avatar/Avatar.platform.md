---
parent: "[[Avatar]]"
section: platform
component: Avatar
package: "@8x8/oxygen-avatar"
role: spoke
pipeline_stage: rewritten
audit_verdict: "NO"
tags: [oxygen, component/Avatar, role/spoke, spoke/platform]
---

# Avatar — Platform UI

Avatar's primary Platform UI tie-in is the [[useUserDetails]] hook from `@8x8/pui-use-user-details`, which exposes the currently authenticated user's identity data emitted by the Platform UI Shell.

---

## Hooks

### useUserDetails

- **Package:** `@8x8/pui-use-user-details` (v2.0.0)
- **Import:** `import { useUserDetails } from '@8x8/pui-use-user-details';`
- **Returns:** `name`, `firstName`, `lastName`, `userId`, `customerId`, `loginId`, `jobTitle`, `email`, `language`.
- **Avatar relevance:** `name` feeds the Avatar's `name` prop (initials computation). A photo URL from a user-profile service would feed `src`.

---

## Events

### `shell-userDetails` (`shell.userDetails.v1`)

- **Direction:** subscribe (via `useUserDetails`).
- **Emitter:** Platform UI Shell.
- **Payload:** `ShellUserDetailsPayload` (the 9 fields listed above).
- **Schema reference:** https://oxygen-dev.8x8.com/events/latest/modules/shell.userDetails.v1.html

---

## Related MFEs

### Platform UI Shell

Renders a built-in `User Avatar` component in the top-right header bar. Header-dependency MFEs (Notifications Center, Activities, Help, Walkme, …) are loaded **after** this Avatar in the order declared in the shell config.

The shell's initialisation flow that affects Avatar consumers:

1. Shell calls `queryUserDetails()`.
2. Validates payload against `UserDetailsSchema` (Zod).
3. On success → emits `shell-userDetails`. Child MFEs read it via `useUserDetails`.
4. On failure → emits `shell-init-error-v1` with `errorType: userDetails`; no user data is downstream-available and Avatars will render their fallback (empty `name` → icon).

---

## Usage pattern

```tsx
import { Avatar } from '@8x8/oxygen-avatar';
import { useUserDetails } from '@8x8/pui-use-user-details';

const CurrentUserAvatar = () => {
  const { name } = useUserDetails();
  return <Avatar name={name} size="xsmall" />;
};
```

> The PUI docs show `useUserDetails` returning user metadata only — they do not expose a photo URL field. If the application has profile imagery, source it from a user-profile service and pass to `src`. See [Avatar.props](Avatar.props.md) for the `name` → initials → icon fallback chain.

---

## See also

- [[Avatar.props]] — `name`, `src`, `imageProps` props that consume PUI user data.
- [[Avatar.accessibility]] — screen-reader labelling for user identification.
- [[Avatar.composition]] — common composition contexts (top bar, contact lists).
