---
parent: "[[Tag]]"
section: usage
component: Tag
package: "@8x8/oxygen-tag"
role: usage
pipeline_stage: doc_rewrite
audit_verdict: YES
source_type: editorial
siblings:
  - "[[Tag]]"
  - "[[Tag.props]]"
  - "[[Tag.anatomy]]"
  - "[[Tag.tokens]]"
  - "[[Tag.accessibility]]"
  - "[[Tag.platform]]"
  - "[[Tag.composition]]"
tags: [component, data_display, role/usage]
---

<!-- STUB:GAP-011 source="Request designer to create ✅ Do / ❌ Don't card frames in the Figma examples page (node 52829:11107) following the standard template. Re-run figma-extract-usage once frames are in place and replace this editorial draft." -->

> **Editorial guidance — not Figma-sourced.** The Figma examples page for Tag (`52829:11107`) contains anatomy and type documentation, not ✅ Do / ❌ Don't card frames, so `figma-extract-usage` cannot run (GAP-011). Pairs below are inferred from `props.md`, `examples.md`, `accessibility.md`, `tokens.md`, `Tag-figma.md`, and the public usage page at [oxygen.8x8.com/components/tags/usage](https://oxygen.8x8.com/components/tags/usage). Treat as provisional until a designer reviews. Replace with `figma-extract-usage` output once Do/Don't card frames exist in Figma.

---

## When to use

- **Categorize content, display metadata, filter items, or indicate status** — the canonical purpose: "Tags help users quickly understand the attributes associated with different entities."
- **As selected pills inside a multi-select Select** — Avatar Tags or Standard Tags representing each chosen value, each with its own remove (×) button. Documented explicitly in the Figma examples page: "The tags used inside the select component when multiple selection is on."
- **As a static status indicator on a card or list row** — e.g. an "External" blue Standard Tag with a leading icon and no remove button. Display-only tags omit `action` entirely.
- **As a RAG (Red / Amber / Green) status group** — only on Standard Tag, where `variant="red"` / `"yellow"` / `"green"` produces the three status colors. The Figma examples page names this pattern explicitly.

## When not to use

| Situation | Use instead |
|---|---|
| You need a **clickable affordance** that triggers an action | [[Button]] — Tag's only interactive part is the × button; the tag body has no role and no keyboard focus |
| You want to convey **count or numeric magnitude** (e.g. "12 unread") | [[Badge]] — counts belong in Badge, not Tag |
| The content is a **long phrase or sentence** | Re-think the data shape — Tag's label uses `label01` (12 px, single line); long text wraps or truncates poorly |
| You want **RAG colour on Avatar Tag** | Use Standard Tag — Avatar Tag omits `yellow` and `green` variants (supports only `default`, `blue`, `grey`, `red`, `yellow-emphasis`) |
| You want a **persistent emphasised warning** colour | Use `variant="yellow-emphasis"` (solid yellow) — distinct from `hasError`, which is a transient "this entity failed" state on Avatar Tag |
| You need a **hover-styled chip** that changes on mouseover | Tag has no hover or pressed state modelled in Figma — only the focus ring on the × button is modelled |

---

## Do / Don't

### Pair 1 — Keep labels short; attach `action` only when the user can actually remove the item

#### ✅ Do — Short keyword, deliberate removability

Tag is a single-line `label01` pill — use it for keywords, metadata, status words, or entity names. Pass `action` only when the user is meant to remove the item (e.g. a filter chip, a selected pill in a Select). For purely informational status tags, omit `action` so no × button renders.

```tsx
import { Tag } from '@8x8/oxygen-tag';

// Display-only status tag — no action, no × button
<Tag variant="blue">
  <GroupIcon />
  External
</Tag>

// Removable filter chip — action + accessible label
<Tag
  action={() => removeFilter('happy')}
  actionProps={{ 'aria-label': 'Remove Happy filter' }}
>
  Happy
</Tag>
```

#### ❌ Don't — Wrap long phrases or attach `action` to non-removable content

A long sentence in a Tag pushes the row width and wraps awkwardly at 12 px. Attaching `action` to a display-only status tag puts a × button next to information the user cannot delete — the affordance misleads.

```tsx
// Long sentence in a Tag — wraps awkwardly
<Tag>Customer has not responded in 48 hours</Tag>

// × on a static status — user has no permission to remove "External"
<Tag variant="blue" action={() => {}}>
  External
</Tag>
```

---

### Pair 2 — Pick the right form for the entity

#### ✅ Do — Avatar Tag for people / groups; Standard Tag for keywords, metadata, and status

Avatar Tag's canonical home is a multi-select Select where each selected pill represents a user or group. Standard Tag covers everything else: filter chips, status badges, metadata labels.

```tsx
// Avatar Tag — person in a multi-select Select
<Tag
  avatar={{ name: 'Josephine Lu', src: '/avatars/jlu.jpg' }}
  action={() => removeUser('jlu')}
  actionProps={{ 'aria-label': 'Remove Josephine Lu' }}
>
  Josephine Lu
</Tag>

// Standard Tag — keyword / metadata
<Tag variant="grey">Engineering</Tag>
```

#### ❌ Don't — Use Avatar Tag for status or stuff Standard Tag with an arbitrary photo

Avatar Tag's leading slot is the `Avatar` sub-component (24×24 px, circular) — it expects a person/group avatar, not an icon or product thumbnail. Using it for status color confuses readers because the photo carries entity identity, not status meaning.

```tsx
// Avatar Tag used for status — the photo competes with the status color
<Tag avatar={{ name: 'Alert', src: '/icons/alert.png' }} variant="red">
  Critical
</Tag>
```

---

### Pair 3 — Use RAG colors on Standard Tag only; remember `variant="yellow"` is "Amber" in design conversation

#### ✅ Do — Build RAG status groups with Standard Tag

The Figma examples page names this pattern: "RAG tags — Red · Amber (yellow) · Green." The `variant` prop value is `"yellow"`, but designers and the Figma `color` axis label it "Amber" (audit WARN-003). When a spec or PR says "Amber tag", the code is `variant="yellow"`.

```tsx
<div style={{ display: 'flex', gap: 'var(--spacing/spacing02)' }}>
  <Tag variant="red">Critical</Tag>
  <Tag variant="yellow">Warning</Tag>  {/* aka "Amber" */}
  <Tag variant="green">Healthy</Tag>
</div>
```

#### ❌ Don't — Apply RAG colors to Avatar Tag

Avatar Tag's `color` axis ships only five values: `default`, `blue`, `grey`, `red`, `yellow-emphasis` — no `yellow` or `green`. Passing `variant="green"` on an Avatar Tag won't match any Figma component and may fall back to default. For a person/group with a status color, render the entity in Avatar Tag and put the status color on an adjacent Standard Tag.

```tsx
// Avatar Tag does not have a `green` variant
<Tag
  avatar={{ name: 'Josephine Lu', src: '/avatars/jlu.jpg' }}
  variant="green"
>
  Josephine Lu
</Tag>
```

---

### Pair 4 — Label the × button, not the tag body; the tag itself never takes focus

#### ✅ Do — Pass `actionProps={{ 'aria-label': 'Remove [label]' }}` whenever `action` is set

The tag body has no `role`, no `tabIndex`, and no keyboard interaction — only the × button is focusable. The focus ring in Figma confirms this: it sits on the close button area only, never the pill. The × is icon-only, so without an accessible label on `actionProps`, screen readers announce it as just "button".

```tsx
<Tag
  avatar={{ name: 'Josephine Lu', src: '/avatars/jlu.jpg' }}
  action={() => removeUser('jlu')}
  actionProps={{ 'aria-label': 'Remove Josephine Lu' }}
>
  Josephine Lu
</Tag>
```

#### ❌ Don't — Set `aria-label` on the tag element or omit the label entirely

`aria-label` on the Tag element itself does nothing — the element has no role or tab stop. A bare `action={fn}` with no `actionProps` produces "Josephine Lu, button" or just "button" — the user cannot tell what removing it does until they activate it.

```tsx
// aria-label on the tag body — ignored by AT
<Tag aria-label="Remove Josephine Lu" action={remove}>
  Josephine Lu
</Tag>

// Bare action with no accessible label on the × button
<Tag action={remove}>Josephine Lu</Tag>
```

---

### Pair 5 — Lay out adjacent tags with `gap: var(--spacing/spacing02)` (4 px)

#### ✅ Do — Use a flex container with 4 px gap

The public usage page is explicit: "Tags should be 4px apart ($spacing02)." `spacing02` is the same token Tag uses internally between its leading visual, label, and × — so the rhythm carries across the row. Use `gap` on the container, not margins on individual tags.

```tsx
<div style={{ display: 'flex', gap: 'var(--spacing/spacing02)', flexWrap: 'wrap' }}>
  {items.map((item) => (
    <Tag
      key={item.id}
      action={() => remove(item.id)}
      actionProps={{ 'aria-label': `Remove ${item.label}` }}
    >
      {item.label}
    </Tag>
  ))}
</div>
```

#### ❌ Don't — Set margins on individual tags or use a different gap value

Per-tag margins fight `flex-wrap` and collapse unpredictably across rows. A gap wider than 4 px (e.g. 8 px or 12 px) breaks the visual rhythm that connects the row to the component's internal spacing.

```tsx
// Per-tag margin + larger gap
<div style={{ display: 'flex', gap: '12px' }}>
  <Tag style={{ marginRight: 8 }}>One</Tag>
  <Tag>Two</Tag>
</div>
```

---

### Pair 6 — `hasError` is a "retry this entity" signal on Avatar Tag; it's not a generic warning color

#### ✅ Do — Use `hasError` + `action={retry}` on Avatar Tag when an entity has failed and needs re-attempt

`hasError` adds a red `error01` border (Figma `type=withActionError`) — the Avatar-Tag-only state for "this person/group failed to load/send/sync and the user can retry." Pair it with an action that retries, and announce the error in text, not color alone.

```tsx
<Tag
  avatar={{ name: 'Failed user', src: '/avatars/failed.jpg' }}
  action={() => retry('failed')}
  actionProps={{ 'aria-label': 'Retry sending to Failed user' }}
  hasError
>
  Failed user
</Tag>
```

#### ❌ Don't — Use `hasError` as a generic warning color or on Standard Tag for emphasis

A persistent warning color belongs on `variant="yellow-emphasis"` (solid yellow). `hasError` is the transient "this Avatar Tag has failed" state — using it for emphasis on Standard Tag confuses readers, and the `withActionError` type is only defined on Avatar Tag in Figma.

```tsx
// hasError as generic warning — use yellow-emphasis instead
<Tag variant="default" hasError>
  Heads up
</Tag>

// ✅ For an emphasised warning, use the dedicated variant
<Tag variant="yellow-emphasis">Heads up</Tag>
```

---

## Open gaps

| ID | Description |
|---|---|
| GAP-011 | Figma examples page (52829:11107) has no ✅ Do / ❌ Don't card frames — pairs above are editorial |
| GAP-USAGE-002 | Leading icon delivery mechanism unverified — Pair 1 code assumes icon via `children`; update when GAP-001 resolves |
| GAP-USAGE-003 | Avatar Tag yellow/green omission unconfirmed — Pair 3 "Don't use RAG on Avatar Tag" rule pending component-owner confirmation (GAP-008) |
| GAP-USAGE-004 | No hover/pressed states in Figma — if hover styling is added in code, Pair 4's "body is non-interactive" rule may need updating (GAP-009) |

---

_Source: editorial — props.md, examples.md, accessibility.md, tokens.md, Tag-figma.md, Tag-audit.md, oxygen.8x8.com/components/tags/usage · 2026-05-15_
