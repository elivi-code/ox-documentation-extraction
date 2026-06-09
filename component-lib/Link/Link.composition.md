---
component: Link
parent: "[[Link]]"
section: composition
pipeline_stage: draft
siblings:
  - "[[Link.props]]"
  - "[[Link.anatomy]]"
  - "[[Link.tokens]]"
  - "[[Link.usage]]"
  - "[[Link.accessibility]]"
  - "[[Link.platform]]"
tags:
  - oxygen
  - component/Link
  - role/spoke-composition
---

## Subcomponents

`Link` contains one optional internal slot:

| Slot | Accepted | Notes |
|------|---------|-------|
| `icon` | Any ReactNode / icon component | Built-in `pop-out` vector renders when `hasIcon=true` and no icon is passed |

## Related components

| Component | Relationship |
|-----------|-------------|
| [[Button]] | Peer — use Button when the action changes app state; use Link when navigating |
| [[Icon]] | Slot — icon component passed to the `icon` prop |

## Patterns

| Pattern | Usage |
|---------|-------|
| [[Form]] | Links often appear within form layouts for ancillary navigation (e.g. "Forgot password?") |
| [[Typography]] | Inline links inherit from surrounding type styles and must match the enclosing text size |

## Usage in context

**Inline within body text:**

```tsx
<p>
  Read more in our{' '}
  <Link href="/docs/getting-started">getting started guide</Link>.
</p>
```

**Standalone with external icon:**

```tsx
<Link href="https://oxygen.8x8.com" icon={<ExternalIcon />}>
  Oxygen Design System
</Link>
```

<!-- STUB:GAP-006 source="Source verified code snippets from the internal Storybook or the package README at https://oxygen.8x8.com/docs/components/textlink/usage. Replace inferred examples above with confirmed ones." -->
<!-- SKIP:GAP-007 manual="Standalone variant example depends on GAP-003 resolution — the correct prop shape for standalone/size must be confirmed before a standalone code example can be written." -->
