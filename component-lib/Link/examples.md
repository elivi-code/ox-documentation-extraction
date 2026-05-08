---
component: Link
package: "@8x8/oxygen-link"
category: navigation
role: examples
role_description: "Code examples — usage patterns from basic to advanced"
pipeline_stage: blocked
pipeline_note: "Audit verdict NO — resolve CONFLICTs before rewrite"
audit_verdict: NO
siblings:
  - "[[Link/props]]"
  - "[[Link/tokens]]"
  - "[[Link/accessibility]]"
  - "[[Link/Link-figma]]"
  - "[[Link/Link-usage]]"
  - "[[Link/Link-audit]]"
tags:
  - oxygen
  - component/Link
  - role/examples
  - stage/blocked
  - category/navigation
---
# Link — Examples

> **See also:** [props.md](props.md) · [tokens.md](tokens.md) · [accessibility.md](accessibility.md)

> **Data gap:** The Oxygen MCP returned 0 clean code examples for this component (`cleanExamples: true` produced an empty set). The documentation Storybook story below is the only programmatic reference available. Concrete usage snippets should be sourced from the Figma spec or internal Storybook.

## Basic usage

```tsx
import { Link } from '@8x8/oxygen-link';

<Link href="https://example.com">Visit example</Link>
```

## With icon

```tsx
import { Link } from '@8x8/oxygen-link';
import { ExternalIcon } from '@8x8/oxygen-icons';

<Link href="https://example.com" icon={<ExternalIcon />}>
  Open in new tab
</Link>
```

## Inline (within text)

```tsx
<p>
  Read more in our{' '}
  <Link href="/docs/getting-started">getting started guide</Link>.
</p>
```

## Chat surface

When rendered inside a sent chat bubble (`$ui13`/`$ui14` surface), set `isChat` so the link uses `$action07` instead of the default `$action08`:

```tsx
<Link href="https://example.com" isChat>
  https://example.com
</Link>
```

## Storybook documentation story

The following is the only example returned by the MCP (Storybook documentation wrapper — not intended for direct copy-paste):

```tsx
export const LinkDocumentation: StoryObj = {
  name: 'Documentation',
  args: argsConfig,
  argTypes: argTypesConfig,
  render: (
    args: React.JSX.IntrinsicAttributes &
      LinkProps &
      React.RefAttributes<HTMLAnchorElement>,
  ) => (
    <>
      <Doc markdown>{README}</Doc>
      <Doc markdown>{example}</Doc>
      <ComponentSection>
        <Link {...args} />
      </ComponentSection>
      <Doc markdown>{CHANGELOG}</Doc>
    </>
  ),
};

const meta: Meta = {
  title: 'Components/Link',
};
```

_Source: Oxygen MCP · Extracted 2026-05-01_
