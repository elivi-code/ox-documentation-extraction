---
component: Tag
package: "@8x8/oxygen-tag"
category: data_display
role: usage
role_description: "Usage guidelines — editorially authored from extracted artifacts and the public Oxygen Tag usage page; the Figma examples page has anatomy/type sections but no Do/Don't card frames"
pipeline_stage: editorial
pipeline_note: "Usage authored editorially from extracted artifacts + oxygen.8x8.com/components/tags/usage — NOT from Figma Do/Don't frames. Re-run doc-audit after creation; replace pairs with figma-extract-usage output when designers add ✅ Do / ❌ Don't card frames to the Tag examples page (node 52829:11107)."
source_type: editorial
audit_verdict: null
siblings:
  - "[[Tag/props]]"
  - "[[Tag/examples]]"
  - "[[Tag/tokens]]"
  - "[[Tag/accessibility]]"
  - "[[Tag/Tag-figma]]"
  - "[[Tag/Tag-audit]]"
tags:
  - oxygen
  - component/Tag
  - role/usage
  - stage/editorial
  - category/data_display
---
<!-- SOURCE: editorial — Figma examples page (52829:11107) carries anatomy/type sections, not ✅ Do / ❌ Don't card frames -->
<!-- FIGMA EXAMPLES PAGE: present (node 52829:11107) but lacks Do/Don't card frames — figma-extract-usage hard-stopped on this condition -->
<!-- REFERENCE PAGE: https://oxygen.8x8.com/components/tags/usage -->
<!-- REFERENCE IMAGES: tag-anatomy, tag-types, tag-state-icon, tag-placement-01 (card), tag-placement-02 (dropdown) -->
<!-- GROUNDING: full — props.md, examples.md, accessibility.md, tokens.md, Tag-figma.md, Tag-audit.md, oxygen.8x8.com/components/tags/usage -->
<!-- DRAFTED: 2026-05-15 -->
<!-- MODE: open -->
<!-- PAIRS: 6 -->
<!-- STATUS: editorial draft — replace with figma-extract-usage output when ✅ Do / ❌ Don't card frames are added to the Figma examples page -->

# Tag — Usage Guidelines

> **See also:** [props.md](./props.md) · [examples.md](./examples.md) · [tokens.md](./tokens.md) ·
> [accessibility.md](./accessibility.md) · [Tag-figma.md](./Tag-figma.md) · [Tag-audit.md](./Tag-audit.md)

> **Editorial guidance — not Figma-sourced.** The Figma examples page for Tag (`52829:11107`) contains anatomy and type documentation, **not** ✅ Do / ❌ Don't card frames, so `figma-extract-usage` cannot run (audit reference: [`Tag-audit.md`](./Tag-audit.md) — GAP-011). The Do/Don't pairs below are inferred from `props.md`, `examples.md`, `accessibility.md`, `tokens.md`, `Tag-figma.md`, and the public usage page at [oxygen.8x8.com/components/tags/usage](https://oxygen.8x8.com/components/tags/usage). Treat as provisional until a designer reviews them. Replace with `figma-extract-usage` output once Do/Don't card frames exist in Figma.

`Tag` is a pill-shaped component used to "label, categorize, or organize items using keywords that describe them" ([oxygen.8x8.com/components/tags/usage](https://oxygen.8x8.com/components/tags/usage)). It has two visual forms — **Standard Tag** (with an optional leading icon) and **Avatar Tag** (with a fixed avatar) — selected automatically by the presence of the `avatar` prop. Either form can be display-only or carry a remove (×) button, controlled by the `action` prop.

---

## When to use

- **Categorize content, display metadata, filter items, or indicate status** — the public usage page's primary purpose ("They help users quickly understand the attributes associated with different entities.").
- **As selected pills inside a multi-select Select** — Avatar Tags or Standard Tags representing each chosen value, each with its own remove (×) button. The Figma examples page documents this explicitly: "The tags used inside the select component when multiple selection is on." ([`Tag-figma.md`](./Tag-figma.md) line 311–314; [`examples.md`](./examples.md) lines 192–219.)
- **As a static status indicator on a card or list row** — e.g. the public usage page's "External" tag on a meeting card (placement image 01): a `blue` Standard Tag with a leading icon and no remove button. Display-only tags omit `action` entirely.
- **As a RAG (Red / Amber / Green) status group** — only on **Standard Tag**, where `variant="red" / "yellow" / "green"` produces the three status colours. The Figma examples page names this pattern explicitly ([`Tag-figma.md`](./Tag-figma.md) line 309 — "RAG tags: Red · Amber (yellow) · Green").

## When not to use

| Situation | Use instead |
|-----------|-------------|
| You need a **clickable affordance** that triggers an action | Use a [Button](../Button/) — Tag's only interactive part is the × button (`action`), not the tag body. The tag body has no `role` and no keyboard focus (see [`accessibility.md`](./accessibility.md) lines 34–44). |
| You want to convey **count or numeric magnitude** (e.g. "12 unread") | Use a [Badge](../Badge/) — counts belong in Badge, not Tag. |
| The content is a **long phrase or sentence** | Re-think the data shape; a Tag's label uses `label01` (12px / 16px line-height, single line) — long text wraps or truncates poorly. See [`tokens.md`](./tokens.md) lines 90–98. |
| You want **status colour on Avatar Tag** for RAG | Avatar Tag omits `yellow` and `green` variants — it supports only `default`, `blue`, `grey`, `red`, `yellow-emphasis` (see [`Tag-figma.md`](./Tag-figma.md) line 131 and audit GAP-008). Use Standard Tag for full RAG, or restrict Avatar Tag to user/group entities. |
| You want a **persistent emphasised warning** colour | Use `variant="yellow-emphasis"` (solid yellow) — distinct from `hasError`, which is a transient "this entity failed" state on Avatar Tag (see [`Tag-figma.md`](./Tag-figma.md) lines 130–132). |
| You need a **hover-styled** chip that changes on mouseover | Tag has **no hover or pressed state** modelled in Figma ([`Tag-figma.md`](./Tag-figma.md) lines 287–294 / audit GAP-009). Only `focus?` is modelled, and it sits on the × button, not the tag body. |

---

## Do / Don't

<!-- SCREENSHOTS UNAVAILABLE — the Figma examples page has anatomy/type sections only, not Do/Don't card frames -->

### Pair 1 — Use Tags for short keywords; only attach `action` when the user can actually remove the item

#### ✅ Do — Keep the label short and decide deliberately whether the tag should be removable

> A Tag is a single-line, 12 px `label01` pill — use it for keywords, metadata, status words, or entity names. Pass an `action` handler **only** when the user is meant to remove the item (e.g. a selected pill inside a Select, a filter chip the user added). For purely informational status (the "External" `blue` tag on the meeting card in the public usage page's placement-01 image), omit `action` entirely so no × button is rendered.

```tsx
import { Tag } from '@8x8/oxygen-tag';
import GroupIcon from '@8x8/oxygen-icons/Group';

// ✅ Display-only status tag — no action, no × button
<Tag variant="blue">
  <GroupIcon />
  External
</Tag>

// ✅ Removable filter chip — action + accessible label
<Tag
  action={() => removeFilter('happy')}
  actionProps={{ 'aria-label': 'Remove Happy filter' }}
>
  Happy
</Tag>
```

**Grounded in:** [`props.md`](./props.md) lines 79–87 (`children`, `action`, `actionProps`); [`Tag-figma.md`](./Tag-figma.md) lines 60–73 (Standard Tag anatomy — leading icon, label, **optional** remove button); [`accessibility.md`](./accessibility.md) lines 34–44 (dual-mode — display-only vs partially interactive); public usage page placement-01 image ("External" tag with no × button); [oxygen.8x8.com/components/tags/usage](https://oxygen.8x8.com/components/tags/usage) — "Tags are versatile components used to categorize content, display metadata, filter items, or indicate statuses."

#### ❌ Don't — Wrap long phrases in a Tag or attach `action` to a tag the user can't actually remove

> A long sentence in a Tag truncates or pushes the row width — the pill is shaped for one-or-two-word labels at 12 px. Attaching `action` to a display-only status tag (e.g. the "External" meeting tag) puts an × button next to information the user is not meant to delete — the affordance lies.

```tsx
// ❌ Sentence in a Tag — wraps awkwardly, blows out the row
<Tag>Customer has not responded in 48 hours</Tag>

// ❌ × on a static status — the user has no permission to remove "External"
<Tag variant="blue" action={() => {}}>
  External
</Tag>
```

---

### Pair 2 — Pick the right form for the entity

#### ✅ Do — Use **Avatar Tag** for people / groups and **Standard Tag** for keywords, metadata, and status

> Avatar Tag's canonical home is a **multi-select Select** where each selected pill represents a user or group — see the public usage page's placement-02 image (Avatar Tags "Josie Lu" and "Michael Jones" as selected pills with their own × buttons inside a To-field). Standard Tag covers everything else: filter chips, status badges, metadata labels.

```tsx
import { Tag } from '@8x8/oxygen-tag';

// ✅ Avatar Tag — people in a multi-select Select
<Tag
  avatar={{ name: 'Josephine Lu', src: '/avatars/jlu.jpg' }}
  action={() => removeUser('jlu')}
  actionProps={{ 'aria-label': 'Remove Josephine Lu' }}
>
  Josephine Lu
</Tag>

// ✅ Standard Tag — keyword / metadata
<Tag variant="grey">Engineering</Tag>
```

**Grounded in:** [`props.md`](./props.md) lines 81, 107–113 (`avatar` prop shape — switches form); [`examples.md`](./examples.md) lines 102–123 (Avatar Tag basics) and lines 192–219 (Avatar Tag inside a multi-select Select); [`Tag-figma.md`](./Tag-figma.md) lines 311–314 (examples page section: "Tags inside Select — used inside the select component when multiple selection is on"); public usage page placement-02 image (canonical multi-select pattern).

#### ❌ Don't — Use Avatar Tag for status or stuff a Standard Tag with an arbitrary leading photo

> Avatar Tag's leading slot is the `Avatar` sub-component (24×24 px, rounded-1000px) — it expects a person/group avatar, not an icon or product thumbnail. Using it for status colour ("Avatar Tag with `variant='red'` to mean Critical") confuses readers because the photo carries entity identity, not status meaning. For status, reach for Standard Tag.

```tsx
// ❌ Avatar Tag used for status — the photo competes with the status colour
<Tag avatar={{ name: 'Alert', src: '/icons/alert.png' }} variant="red">
  Critical
</Tag>
```

---

### Pair 3 — Use RAG colours on **Standard Tag only**; remember `yellow` is "Amber" in design conversation

#### ✅ Do — Build RAG status groups with Standard Tag using `variant="red" / "yellow" / "green"`

> The Figma examples page names this pattern explicitly: "RAG tags — Red · Amber (yellow) · Green" ([`Tag-figma.md`](./Tag-figma.md) line 309). The `variant` prop value is `"yellow"`, but designers and the Figma `color` axis label it "Amber" (audit `WARN-003`). When a spec or PR description says "Amber tag", the code is `variant="yellow"`.

```tsx
import { Tag } from '@8x8/oxygen-tag';

// ✅ RAG status group — Standard Tag, no `avatar` prop
<div style={{ display: 'flex', gap: 'var(--spacing/spacing02)' }}>
  <Tag variant="red">Critical</Tag>
  <Tag variant="yellow">Warning</Tag>  {/* aka "Amber" */}
  <Tag variant="green">Healthy</Tag>
</div>
```

**Grounded in:** [`examples.md`](./examples.md) lines 88–98 (RAG status pattern); [`props.md`](./props.md) lines 92–100 (variant value table — yellow / green available on **Standard only**); [`Tag-figma.md`](./Tag-figma.md) line 131 (Avatar Tag color axis omits yellow/green) and line 309 (examples page names the pattern); [`Tag-audit.md`](./Tag-audit.md) WARN-003 ("yellow" = "Amber" in Figma).

#### ❌ Don't — Apply RAG colours to Avatar Tag — `yellow` and `green` are not available there

> Avatar Tag's `color` axis only ships five values: `default`, `blue`, `grey`, `red`, `yellow-emphasis` — it has **no `yellow` or `green` variants** ([`Tag-figma.md`](./Tag-figma.md) line 131; audit GAP-008). Passing `variant="green"` on an Avatar Tag won't match any Figma component and may fall back to default in some renderers. If the status colour belongs on a person/group, render the entity in Avatar Tag and put the status colour on an adjacent Standard Tag.

```tsx
// ❌ Avatar Tag does not have a `green` variant
<Tag
  avatar={{ name: 'Josephine Lu', src: '/avatars/jlu.jpg' }}
  variant="green"   {/* not in Avatar Tag's color axis */}
>
  Josephine Lu
</Tag>
```

---

### Pair 4 — Label the × button, not the tag body; the tag itself never takes focus

#### ✅ Do — Pass `actionProps={{ 'aria-label': 'Remove [label]' }}` whenever `action` is set

> The tag body has no `role`, no `tabIndex`, and no keyboard interaction — only the × button is focusable, and Figma confirms this: the focus ring is rendered as a 2 px border + 4 px inset shadow around the **close button area only**, never the tag body (`Tag-figma.md` lines 217–222 + public usage page states image — the blue ring sits on the × icon, not the pill). The × is an icon-only button, so screen readers will announce it as just "button" unless an accessible label is provided via `actionProps`.

```tsx
import { Tag } from '@8x8/oxygen-tag';

<Tag
  avatar={{ name: 'Josephine Lu', src: '/avatars/jlu.jpg' }}
  action={() => removeUser('jlu')}
  actionProps={{ 'aria-label': 'Remove Josephine Lu' }}
>
  Josephine Lu
</Tag>
```

**Grounded in:** [`accessibility.md`](./accessibility.md) lines 56–66 (ARIA guidance — `aria-label` via `actionProps`), lines 86–95 (Keyboard interaction — only × button takes Tab), lines 162–166 (Common pitfalls — missing `aria-label` is the top failure); [`Tag-figma.md`](./Tag-figma.md) lines 70 + 84–86 + 217–222 (focus ring lives on the × button area, never the body); [`props.md`](./props.md) lines 82–83, 116–119 (`action`, `actionProps`); public usage page states image (focus ring rendered on the × only).

#### ❌ Don't — Set `aria-label` on the tag body or rely on the bare `action` with no label

> Putting `aria-label="Remove Josephine Lu"` on the Tag element itself does nothing — the element has no role or tab stop. And rendering `action={fn}` with no `actionProps` produces a screen-reader announcement of "Josephine Lu, button" or just "button" — the user can't tell what removing it does until they activate it.

```tsx
// ❌ aria-label on the tag body — ignored by AT, the body is not interactive
<Tag aria-label="Remove Josephine Lu" action={remove}>
  Josephine Lu
</Tag>

// ❌ Bare action with no accessible label on the × button
<Tag action={remove}>Josephine Lu</Tag>
```

---

### Pair 5 — Wrap tag lists in a flex row with `gap: var(--spacing/spacing02)` (4 px)

#### ✅ Do — Lay out adjacent tags with a 4 px gap

> The public usage page is explicit: "Tags should be 4px apart ($spacing02)." `spacing02` is the same token Tag uses internally between its leading visual, label, and × — so the rhythm carries across the row. Use a flex container with `gap`; do not put margins on individual tags.

```tsx
<div style={{
  display: 'flex',
  gap: 'var(--spacing/spacing02)',
  flexWrap: 'wrap'
}}>
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

**Grounded in:** [`examples.md`](./examples.md) lines 172–188 ("Tag list with proper spacing — tags should be spaced $spacing02 (4px) apart"); [`tokens.md`](./tokens.md) lines 114–120 (`spacing02 = 4px` — "internal gap between icon/avatar/label/close button. Also: spacing between adjacent tags."); [oxygen.8x8.com/components/tags/usage](https://oxygen.8x8.com/components/tags/usage) — Placement section: "Tags should be 4px apart ($spacing02)."

#### ❌ Don't — Set margins on individual tags or mix gap values across a row

> Per-tag margins fight `flex-wrap` and collapse unpredictably across rows. Using `gap: 8px` or `gap: 12px` looks "fine" but breaks the visual rhythm with anything Tag does internally — the row no longer reads as part of the same component family.

```tsx
// ❌ Per-tag margin + mixed gap
<div style={{ display: 'flex', gap: '12px' }}>
  <Tag style={{ marginRight: 8 }}>One</Tag>
  <Tag>Two</Tag>
</div>
```

---

### Pair 6 — `hasError` is a "retry this entity" signal on Avatar Tag; it's not a generic warning colour

#### ✅ Do — Use `hasError` + an `action={retry}` on **Avatar Tag** when an entity has failed and needs re-attempt

> `hasError` adds a red `error/error01` border (Figma `type=withActionError`) — it's the Avatar-Tag-only state for "this person/group failed to load/send/sync and the user can retry." Pair it with an `action` that retries (not removes) and announce the error in text, not colour alone.

```tsx
import { Tag } from '@8x8/oxygen-tag';

<Tag
  avatar={{ name: 'Failed user', src: '/avatars/failed.jpg' }}
  action={() => retry('failed')}
  actionProps={{ 'aria-label': 'Retry sending to Failed user' }}
  hasError
>
  Failed user
</Tag>
```

**Grounded in:** [`examples.md`](./examples.md) lines 128–141 (Avatar Tag — error state, `hasError` + `action`); [`props.md`](./props.md) lines 84, 121–125 (`hasError` description); [`Tag-figma.md`](./Tag-figma.md) lines 130–132 (Avatar Tag adds `withActionError` type, not in Standard Tag) and line 213–214 (`error/error01` border token); [`accessibility.md`](./accessibility.md) lines 66, 103, 166 ("error conveyed visually — surface in text via parent or live region; color alone is insufficient").

#### ❌ Don't — Use `hasError` as a generic "warning" colour or apply it on Standard Tag for emphasis

> A persistent warning colour belongs on `variant="yellow-emphasis"` (solid yellow). `hasError` is the **transient** "this Avatar Tag has failed" state — using it for emphasis colour on Standard Tag confuses readers (and per Tag-figma.md line 131–132, the `withActionError` type is only defined on Avatar Tag — Standard Tag's behaviour with `hasError` is implementation-dependent).

```tsx
// ❌ hasError as a generic warning — use yellow-emphasis instead
<Tag variant="default" hasError>
  Heads up
</Tag>

// ✅ For an emphasised warning, use the dedicated variant
<Tag variant="yellow-emphasis">Heads up</Tag>
```

---

## Gaps & open questions

| ID | Type | Description |
|----|------|-------------|
| — | Editorial | These Do/Don't pairs are authored from extracted artifacts and the public oxygen.8x8.com Tag usage page, not from Figma Do/Don't card frames. They should be reviewed by a designer and replaced with `figma-extract-usage` output once card frames exist on the Tag examples page (node `52829:11107`). |
| GAP-USAGE-001 | Source gap | The Figma examples page for Tag contains anatomy and type sections, but **no ✅ Do / ❌ Don't card frames** — inherited from [`Tag-audit.md`](./Tag-audit.md) GAP-011. The public usage page at [oxygen.8x8.com/components/tags/usage](https://oxygen.8x8.com/components/tags/usage) carries Anatomy, Overview, Variants, Behavior/States, and Placement but no Do/Don't and no "when not to use" content. |
| GAP-USAGE-002 | Source gap | The leading icon delivery mechanism is unverified — `props.md` notes "verify how an icon is supplied in code — it may be the first React element in children" (audit GAP-001). The Pair-1 code example assumes the icon goes via `children`; replace with the confirmed prop once `@8x8/oxygen-tag` source is inspected. |
| GAP-USAGE-003 | Source gap | Avatar Tag's omission of `yellow` and `green` variants (5 vs Standard's 7 colours) is unconfirmed — may be intentional (audit GAP-008). Pair 3's "Don't use RAG on Avatar Tag" rule should be re-confirmed against component-owner intent. |
| GAP-USAGE-004 | Source gap | No hover or pressed states are modelled in Figma (audit GAP-009). If a hover style is added in code, the usage rule about "the body is non-interactive" in Pair 4 may need to soften. |
| GAP-USAGE-005 | Source gap | The public usage page lists exactly one placement guideline (`4px apart, $spacing02`) and no maximum-tag-count, no overflow strategy, and no truncation guidance. A long list of Avatar Tags in a narrow Select field will wrap multi-row; designers should add explicit guidance for the "too many tags" case. |

---

_Source: editorial guidance authored from extracted artifacts (props.md, examples.md, accessibility.md, tokens.md, Tag-figma.md, Tag-audit.md) and the public usage page at oxygen.8x8.com/components/tags/usage · Figma examples page lacks Do/Don't card frames · 2026-05-15_
