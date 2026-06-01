---
component: Accordion
package: "@8x8/oxygen-accordion"
category: layout_overlay
role: props
role_description: "API props reference — all component properties with types, defaults, and descriptions"
pipeline_stage: spec_ready
pipeline_note: "Audit verdict YES/PARTIAL — doc-rewrite can run"
audit_verdict: YES
files_present:
  - props
  - examples
  - tokens
  - accessibility
  - figma
  - audit
siblings:
  - "[[Accordion/examples]]"
  - "[[Accordion/tokens]]"
  - "[[Accordion/accessibility]]"
  - "[[Accordion/accordion-figma]]"
  - "[[Accordion/accordion-audit]]"
tags:
  - oxygen
  - component/Accordion
  - role/props
  - stage/spec_ready
  - category/layout_overlay
---
# Accordion — Props

> **See also:** [examples.md](./examples.md) · [tokens.md](./tokens.md) · [accessibility.md](./accessibility.md) · [accordion-figma.md](./accordion-figma.md)

---

## Installation

```sh
# yarn
$ yarn add @8x8/oxygen-accordion

# npm
$ npm install @8x8/oxygen-accordion
```

**Registry configuration required (8x8 VPN required):**

```ini
# .npmrc
@8x8:registry=https://artifactory.es.8x8.com/artifactory/api/npm/npm-repository/
```

```yaml
# .yarnrc.yml
npmScopes:
  8x8:
    npmRegistryServer: "https://artifactory.es.8x8.com/artifactory/api/npm/npm-repository/"

nodeLinker: node-modules
```

---

## `Accordion`

| Prop | Type | Default | Required | Description |
|------|------|---------|:--------:|-------------|
| `children` | `React.ReactNode` | `null` | ✅ | Rendered content inside the Accordion |
| `title` | `string` | — | ✅ | Accordion title, shown in the Header on the left side |
| `testId` | `string` | `'ACCORDION'` | — | Test ID DOM attribute value |
| `text` | `string` | `''` | — | Secondary text, shown in the Header on the right side |
| `iconLeft` | `React.ReactNode` | `null` | — | Icon rendered inside the Accordion Header on the left side |
| `contentAfterTitle` | `React.ReactNode` | `null` | — | Custom content (e.g. `IconButton` with `Tooltip`) rendered after the accordion title. Don't use interactive elements when `expandTrigger="header"` |
| `id` | `string` | — | — | Unique identifier. If omitted, `AccordionGroup` will provide a guid. Sent as param in `AccordionGroup.onChange` |
| `isExpanded` | `boolean` | `false` | — | Controls whether the accordion is expanded or collapsed |
| `forcedHeight` | `number` | `0` | — | Forces accordion content to a specific height in pixels |
| `isContentScrollable` | `boolean` | `false` | — | Overrides the default scroll behaviour. By default, scrollable when height is fixed, non-scrollable otherwise |
| `hasPadding` | `boolean` | `true` | — | When `false`, removes the padding from the expanded content area |
| `expandTrigger` | `'header' \| 'arrow'` | `'header'` | — | `'header'` — entire header is clickable; `'arrow'` — only the chevron is clickable. Use `'arrow'` when `contentAfterTitle` contains interactive elements |
| `translations` | `Translations` | — | — | Custom translations for expand/collapse aria-labels. Supports partial overrides |
| `onChange` | `(id: string, isExpanded: boolean) => void` | — | — | Callback fired when accordion state changes |
| `shouldCloseOnActiveClick` | `boolean` | — | — | **@deprecated** If true, clicking the active Accordion will close it |

> **Figma-only — `divider?`:** The Figma component exposes a `divider?` boolean toggle (default: `true`) that shows a 1px separator below the accordion row. There is no corresponding code prop — the divider is always rendered in the DOM. Use CSS overrides to suppress it if needed.

> **Figma-only — `scrollbar?`:** The Figma component exposes a `scrollbar?` boolean toggle (default: `false`) that renders a Mac OS–style scrollbar overlay in design previews. There is no corresponding code prop — scroll behaviour in code is governed by `isContentScrollable` and `forcedHeight`. The browser's native scrollbar renders automatically when content overflows a fixed-height container.

---

## `AccordionGroup`

| Prop | Type | Default | Required | Description |
|------|------|---------|:--------:|-------------|
| `children` | `React.ReactNode` | `null` | ✅ | Rendered `Accordion` items inside the group |
| `testId` | `string` | `'ACCORDION'` | — | Test ID DOM attribute value |
| `initialActiveElementId` | `string` | — | — | ID of the initially active accordion. Ignored on subsequent renders (uncontrolled initial value only) |
| `hasFixedHeight` | `boolean` | `false` | — | If `true`, the group fills the parent container height and the active accordion content fills the remaining space. Only one accordion can be open at a time in this mode |
| `expandTrigger` | `'header' \| 'arrow'` | — | — | Default interaction mode for all child accordions. Individual accordions can override |
| `translations` | `Translations` | — | — | Default translations for all child accordions. Individual accordions can override with their own |
| `onChange` | `(id: string, isExpanded: boolean) => boolean \| void` | — | — | Callback fired when an accordion header is clicked. Return `false` to block the state change; `void` or `true` allows it |
| `shouldCloseOnActiveClick` | `boolean` | `true` | — | **@deprecated** If true, clicking the active Accordion will close it |

---

## `Translations` type

| Key | Description |
|-----|-------------|
| `expand` | Aria-label for the expand action |
| `collapse` | Aria-label for the collapse action |

---

_Source: Oxygen MCP · Extracted 2026-04-28_
