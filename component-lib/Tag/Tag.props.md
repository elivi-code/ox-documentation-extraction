---
parent: "[[Tag]]"
section: props
component: Tag
package: "@8x8/oxygen-tag"
role: props
pipeline_stage: doc_rewrite
audit_verdict: YES
siblings:
  - "[[Tag]]"
  - "[[Tag.anatomy]]"
  - "[[Tag.tokens]]"
  - "[[Tag.usage]]"
  - "[[Tag.accessibility]]"
  - "[[Tag.platform]]"
  - "[[Tag.composition]]"
tags: [component, data_display, role/props]
---

## Props

| Name | Type | Default | Required | Description | Accepts |
|---|---|---|---|---|---|
| `children` | `ReactNode` | — | No | Component content — the visible label text. When a leading icon is used, it is also passed here as the first child element. | — |
| `variant` | `Variant` | `'default'` | No | Color variant controlling background and text tokens. | See values below |
| `avatar` | `Pick<AvatarProps, 'name' \| 'src' \| 'isGroup'>` | — | No | When provided, switches the component to Avatar Tag form. | [[Avatar]] |
| `action` | `React.MouseEventHandler<HTMLDivElement>` | — | No | Click handler for the remove (×) button. When set, the close button is rendered. | — |
| `actionProps` | `React.HTMLAttributes<HTMLDivElement>` | — | No | Extra props applied to the remove-button `<div>` — use for `aria-label`, `data-*`. | — |
| `hasError` | `boolean` | `false` | No | Adds a red `error01` border around the tag. Maps to Figma `type=withActionError` on Avatar Tag. | — |
| `isFocused` | `boolean` | `false` | No | Forces the focused ring appearance without keyboard interaction. Use when a parent (e.g. Select) controls focus programmatically. | — |
| `testId` | `string` | — | No | Sets `data-testid` on the root element. | — |

---

## `variant` values

<!-- STUB:GAP-002 source="Check @8x8/oxygen-tag TypeScript types for the Variant union. Confirm all 7 values are present and correctly named. Update props.md if any differ." -->

The `Variant` type alias is opaque in the Oxygen MCP response. Values listed are sourced from the Figma `color` variant axis.

| Value | Available on | Description |
|---|---|---|
| `'default'` | Standard, Avatar | Neutral off-white (light) / neutral grey (dark) — default appearance |
| `'blue'` | Standard, Avatar | Subtle blue background |
| `'grey'` | Standard, Avatar | Strong grey background with white text (inverted) |
| `'red'` | Standard, Avatar | Subtle red — RAG status (Red) |
| `'yellow'` | Standard only | Subtle yellow — RAG status (Amber). **Not available on Avatar Tag.** |
| `'green'` | Standard only | Subtle green — RAG status (Green). **Not available on Avatar Tag.** |
| `'yellow-emphasis'` | Standard, Avatar | Solid yellow — emphasized warning |

---

## `avatar` shape

When `avatar` is provided, the component renders in Avatar Tag form. The Avatar is positioned at the leading edge; the tag body does not change.

| Property | Type | Description |
|---|---|---|
| `name` | `string` | Generates avatar initials when `src` is not provided |
| `src` | `string` | URL of the avatar image |
| `isGroup` | `boolean` | Renders the avatar as a group avatar |

---

## `action` and `actionProps`

When `action` is set, a remove (×) button renders at the trailing edge. Figma `type=withAction` matches this state. Always pass an accessible label via `actionProps`:

```tsx
actionProps={{ 'aria-label': 'Remove [tag label]' }}
```

Without it, screen readers announce the button as just "button". See [[Tag.accessibility]] for full guidance.

---

## `hasError`

Adds a 2 px solid `error/error01` border around the tag container. In Figma this is the `type=withActionError` variant on **Avatar Tag only** — confirm whether `hasError` also affects Standard Tag in code.

---

## `isFocused`

Programmatically renders the focused ring without requiring keyboard focus. Use sparingly — only when a parent component (e.g. a multi-select Select) controls focus state externally.

---

## Leading icon delivery

<!-- STUB:GAP-001 source="Inspect @8x8/oxygen-tag source to confirm whether the leading icon is passed via children (first ReactElement) or a dedicated icon prop. Update props.md with the confirmed mechanism and add a verified example." -->

The icon delivery mechanism is unverified. Current evidence from Figma Code Connect suggests the icon is the first `ReactElement` passed as `children`. Inspect `@8x8/oxygen-tag` source to confirm before using in production.

```tsx
{/* Assumed pattern — verify against package source */}
<Tag variant="blue">
  <GroupIcon />
  External
</Tag>
```

<!-- SKIP:GAP-004 manual="Once GAP-001 is resolved, update the leading icon example with the confirmed prop usage pattern and remove the verification caveat." -->

---

## Figma ↔ code variant mapping

| Figma property | Code equivalent |
|---|---|
| `mode` (light/dark) | Inherited from theme provider — not a direct prop |
| `color` | `variant` |
| `type=withAction` | `action` prop present |
| `type=withActionError` | `action` + `hasError` |
| `icon?` boolean (Standard Tag) | Icon passed as first child in `children` (unverified — GAP-001) |
| `focus?` boolean | `isFocused` |
| Avatar / Standard form | Switched by `avatar` prop presence |

---

_Source: Oxygen MCP (`@8x8/oxygen-tag`) · Figma node 8083:8359 · Extracted 2026-05-01_
