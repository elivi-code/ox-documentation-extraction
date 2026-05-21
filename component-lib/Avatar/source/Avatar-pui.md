<!-- SOURCE: platform-ui-mcp snapshotId: 2026-02-24 -->
<!-- EXTRACTED: 2026-05-21 -->
<!-- COMPONENT: Avatar -->
<!-- CONFIRMED BY: engineer (relevance check step 2) -->

---
component: Avatar
package: "@8x8/oxygen-avatar"
category: data_display
role: pui
role_description: "Platform UI infrastructure context — hooks, events, and MFE relationships for Avatar"
pipeline_stage: extracted
source_type: platform-ui-mcp
siblings:
  - "[[Avatar/props]]"
  - "[[Avatar/examples]]"
  - "[[Avatar/tokens]]"
  - "[[Avatar/accessibility]]"
  - "[[Avatar/Avatar-figma]]"
  - "[[Avatar/Avatar-usage]]"
  - "[[Avatar/Avatar-audit]]"
tags:
  - oxygen
  - component/Avatar
  - role/pui
  - stage/extracted
  - category/data_display
---

# Avatar — Platform UI Context

> **See also:** [props.md](./props.md) · [examples.md](./examples.md) · [Avatar-figma.md](./Avatar-figma.md) · [accessibility.md](./accessibility.md)

---

## Hooks

### useUserDetails

- **Package:** `@8x8/pui-use-user-details` (v2.0.0)
- **Import:** `import { useUserDetails } from '@8x8/pui-use-user-details';`
- **Purpose (verbatim from docs):** "The `useUserDetails` hook is part of the `@8x8/pui-use-user-details` package. It provides access to key information about the currently authenticated user."
- **Returned properties (ShellUserDetailsPayload):**

  | Property | Type | Description |
  |---|---|---|
  | `name` | `string` | Full name of the user |
  | `firstName` | `string` | First name of the user |
  | `lastName` | `string` | Last name of the user |
  | `userId` | `string` | Unique identifier for the user |
  | `customerId` | `string` | ID of the customer/account |
  | `loginId` | `string` | Login ID/username of the user |
  | `jobTitle` | `string` | Job title (if available) |
  | `email` | `string` | Email address of the user |
  | `language` | `string` | Preferred language (locale code) |

- **Relevance to Avatar:** `name` feeds the Avatar's `name` prop for initials computation. Once a photo URL is wired in (e.g. via a user-profile service), it would feed the `src` prop.

---

## Events

### shell-userDetails (shell.userDetails.v1)

- **Direction:** subscribe (via the `useUserDetails` hook abstraction)
- **Payload:** `ShellUserDetailsPayload` — see properties table above.
- **Docs path:** `mfes/hooks/use-user-details.md`
- **Schema reference:** https://oxygen-dev.8x8.com/events/latest/modules/shell.userDetails.v1.html
- **Emitter:** Platform UI Shell — emits this event with the details of the currently authenticated user after `queryUserDetails()` resolves at shell init.

---

## Related MFEs

### Platform UI Shell

- **Docs path:** `mfes/platform-ui-shell.md`
- **Relevance:** The shell renders a built-in `User Avatar` component in the top-right header bar. Per the docs: _"Header dependencies: Those MFEs will get loaded in the top right header bar, after the `User Avatar` component, in the order they are declared in the config. Use cases would be something like a Notifications Center MFE, Activities, Help, Walkme etc."_
- **Initialisation flow relevant to Avatar:**
  1. Shell queries user details via `queryUserDetails()` at init.
  2. Validates payload against `UserDetailsSchema` (Zod).
  3. Emits `shell-userDetails` event on success — picked up by child MFEs through `useUserDetails`.
  4. If validation fails, shell emits `shell-init-error-v1` with `errorType: userDetails` (no avatar data available downstream).
- **Consistency concern (verbatim):** The shell ensures "a consistent look and feel across multiple apps (like notifications, feedback, navigation, block navigation, user status and details, etc)."

---

## Usage examples

Verbatim from `mfes/hooks/use-user-details.md`:

```tsx
import { useUserDetails } from '@8x8/pui-use-user-details';

const {
  name,
  firstName,
  lastName,
  userId,
  customerId,
  loginId,
  jobTitle,
  email,
  language,
} = useUserDetails();
```

```tsx
import { useUserDetails } from '@8x8/pui-use-user-details';

const UserProfile = () => {
  const { name, email, jobTitle } = useUserDetails();

  return (
    <div>
      <h1>Welcome, {name}</h1>
      <p>Email: {email}</p>
      <p>Job Title: {jobTitle}</p>
    </div>
  );
};
```

**Demo:** https://app-acceptance.8x8.com/demo/shell-data/user-details

**Suggested Avatar composition** (derived from the hook payload — not present verbatim in PUI docs):

```tsx
import { Avatar } from '@8x8/oxygen-avatar';
import { useUserDetails } from '@8x8/pui-use-user-details';

const CurrentUserAvatar = () => {
  const { name } = useUserDetails();
  return <Avatar name={name} size="xsmall" />;
};
```

---

## Candidates rejected

For audit trail — these search results were surfaced but the engineer did not confirm them as relevant:

- `docs/03-designers/03-team.md` — sample HTML mockup of a team page; no infrastructure relevance.
- `mfes/mfe-authoring.md` — generic MFE authoring intro; surfaced only via "user details" keyword match.
- Observability dashboards, iframe MFEs, intro pages — keyword noise.

Searches with zero hits: `presence status`, `profile photo`.
