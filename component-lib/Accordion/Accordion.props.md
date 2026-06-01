---
parent: "[[Accordion]]"
section: props
---

## Props

### `Accordion`

| Name | Type | Default | Required | Description | Accepts |
|---|---|---|---|---|---|
| `children` | `ReactNode` | `null` | ✅ | Rendered content inside the panel | — |
| `title` | `string` | — | ✅ | Header label | — |
| `testId` | `string` | `'ACCORDION'` | — | Test ID DOM attribute | — |
| `text` | `string` | `''` | — | Secondary text, right side of header | — |
| `iconLeft` | `ReactNode` | `null` | — | Leading icon in header | [[Icon]] |
| `contentAfterTitle` | `ReactNode` | `null` | — | Slot after title. Use interactive elements only with `expandTrigger="arrow"` | [[IconButton]], [[Tooltip]] |
| `id` | `string` | — | — | Unique identifier. `AccordionGroup` provides a guid if omitted | — |
| `isExpanded` | `boolean` | `false` | — | Controlled expanded state | — |
| `forcedHeight` | `number` | `0` | — | Pixel height cap on content area | — |
| `isContentScrollable` | `boolean` | `false` | — | Override scroll behaviour. Defaults to scrollable when height is fixed | — |
| `hasPadding` | `boolean` | `true` | — | When `false`, removes padding from content area | — |
| `expandTrigger` | `'header' \| 'arrow'` | `'header'` | — | `'header'` — full header clicks; `'arrow'` — chevron only | — |
| `translations` | `Translations` | — | — | Aria-labels for expand/collapse. Supports partial overrides | — |
| `onChange` | `(id: string, isExpanded: boolean) => void` | — | — | Fired on state change | — |
| `shouldCloseOnActiveClick` | `boolean` | — | — | **@deprecated** Clicking active accordion closes it | — |

<!-- source: figma-only -->
> **`divider?`** — Figma boolean toggle (default `true`) showing a 1px separator below the row. No code prop — always rendered. Override via CSS if needed.

<!-- source: figma-only -->
> **`scrollbar?`** — Figma boolean toggle (default `false`) showing a Mac OS–style scrollbar in design previews. No code prop — scroll behaviour in code is controlled by `isContentScrollable` and `forcedHeight`.

<!-- SKIP:GAP-004 type=DOC_GAP manual — Component owner confirmation required: The Figma _header atom has AIBadge? toggle (default false). No code prop documented. Confirm whether achievable via contentAfterTitle or a planned prop. -->

<!-- SKIP:GAP-010 type=DOC_GAP manual depends_on=GAP-004 — No disabled state example. Confirm whether disabled is passed as an HTML attribute on the button element. -->

---

### `AccordionGroup`

| Name | Type | Default | Required | Description | Accepts |
|---|---|---|---|---|---|
| `children` | `ReactNode` | `null` | ✅ | `Accordion` items | [[Accordion]] |
| `testId` | `string` | `'ACCORDION'` | — | Test ID DOM attribute | — |
| `initialActiveElementId` | `string` | — | — | ID of initially open accordion (uncontrolled) | — |
| `hasFixedHeight` | `boolean` | `false` | — | Group fills parent height; only one accordion open at a time | — |
| `expandTrigger` | `'header' \| 'arrow'` | — | — | Default for all child accordions | — |
| `translations` | `Translations` | — | — | Default translations for all children | — |
| `onChange` | `(id: string, isExpanded: boolean) => boolean \| void` | — | — | Return `false` to block state change | — |
| `shouldCloseOnActiveClick` | `boolean` | `true` | — | **@deprecated** | — |

---

### `Translations` type

| Key | Type | Description |
|---|---|---|
| `expand` | `string` | Aria-label for expand action |
| `collapse` | `string` | Aria-label for collapse action |

<!-- STUB:GAP-012 source="Check @8x8/oxygen-accordion source or Storybook for default values of expand/collapse translations strings. Add defaults here and confirm whether English-only or localised." -->
