---
parent: "[[Spinner]]"
section: usage
component: Spinner
pipeline_stage: draft
siblings:
  - "[[Spinner]]"
  - "[[Spinner.props]]"
  - "[[Spinner.anatomy]]"
  - "[[Spinner.tokens]]"
  - "[[Spinner.accessibility]]"
  - "[[Spinner.platform]]"
  - "[[Spinner.composition]]"
tags:
  - oxygen
  - component/Spinner
  - role/usage
---
<!-- STUB:GAP-012 source="Run figma-extract-usage for Spinner and replace this file wholesale once a Figma examples page with Do/Don't card frames (↳ Spinner examples) is authored in the UI-Components file" -->

> **Editorial guidance** — no Figma examples page exists for Spinner. Pairs below are drafted from the public Oxygen usage page at <https://oxygen.8x8.com/components/spinner/usage> plus extracted MCP artifacts. Replace this file with `figma-extract-usage` output if a card-frame examples page is ever authored.

Spinner is a small loading indicator — a continuously rotating arc — used to signal that an indeterminate background task is in flight. Per the published Oxygen usage page, "Spinners are loading circles that are used for loading sections or areas such as a page or a dropdown menu," and "the spinner is a seamless and continuous animation that will stop once the page is loaded." It is passive, non-interactive, and not focusable — its only job is to tell the user "wait, something is happening."

---

## Anatomy

1. **Spinner arc** — the rotating circular indicator itself. Renders at one of the named sizes (`"small"`, `"default"`, `"large2x"`) or a raw pixel number. Stroke width is configurable via `strokeWidth`.
2. **Supporting text** _(strongly recommended)_ — a short label rendered next to the spinner. The Oxygen usage page is explicit: "There should always be supporting text where space permits, as it is best practice to give clear expectations to the user." Passed via the `text` prop.

The Spinner ships no header, footer, or container surface — consuming layouts compose it inside the area being loaded.

---

## When to use

- **A whole page or large section is loading** and the structure isn't yet known — use `size="default"`.
- **Modal content is being fetched** before the modal can be populated.
- **A menu, dropdown, or overflow menu** needs to populate from a network call — use `size="small"`.
- **A card or row** is hydrating in place — small, inline contexts.

## When not to use

- **There is a determinate value to show.** The Oxygen usage page is explicit: "When there is a determinate value. Use a progress bar instead."
- **Content-shaped placeholders would communicate more.** When you can show the *shape* of the incoming content, prefer Skeleton loaders over a generic spinner.
- **The wait is shorter than ~200 ms.** A spinner that flashes on and off feels janky.
- **As decoration.** Spinner is for loading state only.

---

## Do / Don't

### Pair 1 — Use Spinner for indeterminate waits; reach for ProgressBar when you can measure progress

#### ✅ Do — Pick Spinner when you cannot report a percentage

```tsx
{/* Right — fetching a record; duration unknown */}
{isLoading ? <Spinner size="default" text="Loading record" /> : <RecordView record={record} />}
```

#### ❌ Don't — Use Spinner where you have a real percentage

```tsx
{/* Wrong — measurable progress shown as an indeterminate spinner */}
<Spinner size="default" text={`Uploading… ${bytesSent}/${totalBytes}`} />

{/* Right — use ProgressBar for known-percentage work */}
<ProgressBar value={bytesSent} max={totalBytes} label="Uploading" />
```

**Source:** <https://oxygen.8x8.com/components/spinner/usage> ("When there is a determinate value. Use a progress bar instead.")

---

### Pair 2 — Match `size` to the area being loaded

#### ✅ Do — Use `size="small"` for inline contexts and `size="default"` for page/section loads

```tsx
{/* Inline — a dropdown is hydrating */}
<DropdownMenu>
  {options.length === 0
    ? <Spinner size="small" text="Loading options" />
    : options.map(renderOption)}
</DropdownMenu>

{/* Page / large section */}
<main>
  {isLoading
    ? <Spinner size="default" text="Loading conversation" />
    : <Conversation thread={thread} />}
</main>
```

#### ❌ Don't — Use an oversized spinner inside a small container or a tiny spinner for a page load

```tsx
{/* Wrong — page-sized spinner inside a 32px dropdown row */}
<DropdownMenu><Spinner size="default" /></DropdownMenu>

{/* Wrong — tiny spinner on a full-page loading state */}
<main style={{ minHeight: '80vh' }}><Spinner size="small" /></main>
```

**Source:** <https://oxygen.8x8.com/components/spinner/usage> (Variants — default / small)

> ⚠️ A third size key — `"large2x"` — is documented in code (sourced from Storybook) but **does not exist in the Figma component set** (GAP-011). Until that CONFLICT is resolved, prefer `"default"` and `"small"` for new work.

---

### Pair 3 — Always pair the spinner with supporting text where space permits

#### ✅ Do — Use the `text` prop so the user knows what is loading

```tsx
{/* Right — text scopes the wait to a concrete thing */}
<Spinner size="default" text="Loading conversation history" />

{/* Right — small inline context; surrounding label is enough */}
<DropdownLabel>Contacts <Spinner size="small" aria-label="Loading contacts" /></DropdownLabel>
```

When you use `text`, that string is the accessible label — you do **not** need to also set `aria-label`.

#### ❌ Don't — Render a bare spinner with no label of any kind

```tsx
{/* Wrong — no label; invisible to screen readers, ambiguous to sighted users */}
<Spinner size="default" />

{/* Weaker — passes a11y but doesn't tell the user what is loading */}
<Spinner size="default" aria-label="Loading" />
```

**Source:** <https://oxygen.8x8.com/components/spinner/usage> ("There should always be supporting text where space permits")

---

### Pair 4 — Respect `prefers-reduced-motion` by toggling `hasAnimation`

#### ✅ Do — Disable the rotation animation for users who have asked for less motion

```tsx
const prefersReducedMotion = useMediaQuery('(prefers-reduced-motion: reduce)');

<Spinner
  size="default"
  text="Loading record"
  hasAnimation={!prefersReducedMotion}
/>
```

#### ❌ Don't — Leave a continuous rotation running for users who opt out of motion

```tsx
{/* Wrong — rotation runs regardless of the OS preference */}
<Spinner size="default" text="Loading record" />
```

**Source:** accessibility.md (motion sensitivity · WCAG 2.3.3)

> ⚠️ It is currently **unconfirmed** whether the Spinner reads the OS `prefers-reduced-motion` setting automatically or requires the consuming app to wire `hasAnimation={false}` manually (WARN-002). Until verified, wire it yourself.

---

### Pair 5 — Reach for Skeleton loaders when the content shape is known

#### ✅ Do — Use Spinner only when the structure of the incoming content is unknown or trivial

```tsx
{/* Right — content shape unknown */}
{isBootstrapping
  ? <Spinner size="default" text="Loading workspace" />
  : <Workspace />}

{/* Right — content shape is known: prefer skeletons */}
{isLoading
  ? <ConversationListSkeleton rowCount={10} />
  : <ConversationList items={items} />}
```

#### ❌ Don't — Drop a Spinner into a structured surface where Skeleton would carry more meaning

```tsx
{/* Wrong — known list shape, spinner discards structure; layout jumps on load */}
{isLoading
  ? <div style={{ display: 'grid', placeItems: 'center', minHeight: 400 }}>
      <Spinner size="default" text="Loading conversations" />
    </div>
  : <ConversationList items={items} />}
```

**Source:** <https://oxygen.8x8.com/components/spinner/usage> (Related components — Skeleton loader)

---

### Pair 6 — Don't stack spinners or use Spinner as decoration

#### ✅ Do — Show one spinner per loading region

```tsx
{/* Right — one spinner anchored to the active loading scope */}
{pageLoading
  ? <Spinner size="default" text="Loading workspace" />
  : <Workspace>
      {cardLoading
        ? <Spinner size="small" text="Loading metrics" />
        : <MetricsCard metrics={metrics} />}
    </Workspace>}
```

#### ❌ Don't — Layer spinners or use Spinner where no loading is happening

```tsx
{/* Wrong — multiple competing spinners; user can't tell what they're waiting on */}
<Spinner size="default" text="Loading" />
<Spinner size="small" text="Loading metrics" />
<Spinner size="small" text="Loading recents" />

{/* Wrong — decorative use; nothing is loading */}
<EmptyState
  illustration={<Spinner size="large2x" />}
  title="No conversations yet"
/>
```

**Source:** <https://oxygen.8x8.com/components/spinner/usage> ("seamless and continuous animation that will stop once the page is loaded")

---

_Source: Editorial draft from <https://oxygen.8x8.com/components/spinner/usage> + extracted MCP artifacts · Drafted 2026-05-15_
