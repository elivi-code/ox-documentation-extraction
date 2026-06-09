---
component: Spinner
package: "@8x8/oxygen-loaders"
category: feedback_status
role: usage
role_description: "Usage guidelines — editorial, drafted from the public Oxygen docs usage page (https://oxygen.8x8.com/components/spinner/usage) plus extracted MCP artifacts; no Figma examples page exists"
pipeline_stage: editorial
pipeline_note: "Pairs are editorial, grounded in the published Oxygen usage page. Audit verdict remains NO until GAP-010 (isInverted) and GAP-011 (large2x) CONFLICTs are resolved. Replace with figma-extract-usage output if a `↳ Spinner examples` page with Do/Don't card frames is ever authored."
source_type: editorial
audit_verdict: null
siblings:
  - "[[Spinner/props]]"
  - "[[Spinner/examples]]"
  - "[[Spinner/tokens]]"
  - "[[Spinner/accessibility]]"
  - "[[Spinner/Spinner-figma]]"
  - "[[Spinner/Spinner-audit]]"
tags:
  - oxygen
  - component/Spinner
  - role/usage
  - stage/editorial
  - category/feedback_status
---
<!-- SOURCE: editorial — drafted from https://oxygen.8x8.com/components/spinner/usage + props.md + examples.md + accessibility.md + Spinner-figma.md -->
<!-- FIGMA EXAMPLES PAGE: none — no `↳ Spinner examples` page exists in the UI-Components Figma file -->
<!-- GROUNDING: strong — published usage page mirrors OX MCP content; props.md, examples.md, accessibility.md, Spinner-figma.md all present -->
<!-- DRAFTED: 2026-05-15 -->
<!-- MODE: open -->
<!-- PAIRS: 6 -->
<!-- STATUS: editorial draft — replace with figma-extract-usage output if Figma cards are ever authored -->

# Spinner — Usage Guidelines

> **See also:** [props.md](./props.md) · [examples.md](./examples.md) · [tokens.md](./tokens.md) · [accessibility.md](./accessibility.md) · [Spinner-figma.md](./Spinner-figma.md) · [Spinner-audit.md](./Spinner-audit.md)

> **Editorial guidance — no Figma examples page exists for Spinner.** This file is drafted from the public Oxygen usage page at <https://oxygen.8x8.com/components/spinner/usage>, which mirrors the OX MCP content, together with the extracted sibling files. It does **not** clear [Spinner-audit.md](./Spinner-audit.md) **GAP-010** (`isInverted` CONFLICT) or **GAP-011** (`large2x` CONFLICT), which remain blocked on a human design/code decision. Replace this file wholesale with `figma-extract-usage` output once a `↳ Spinner examples` page with `✅ Do — …` / `❌ Don't — …` card frames is authored.

Spinner is a small loading indicator — a continuously rotating arc — used to signal that an indeterminate background task is in flight. Per the published Oxygen usage page, "Spinners are loading circles that are used for loading sections or areas such as a page or a dropdown menu," and "the spinner is a seamless and continuous animation that will stop once the page is loaded." It is passive, non-interactive, and not focusable ([accessibility.md:29](./accessibility.md)) — its only job is to tell the user "wait, something is happening."

---

## Anatomy

> **Source:** [Spinner-figma.md](./Spinner-figma.md) layer structure + the published anatomy on <https://oxygen.8x8.com/components/spinner/usage>.

1. **Spinner arc** — the rotating circular indicator itself. Renders at one of the named sizes (`"small"`, `"default"`, `"large2x"`) or a raw pixel number ([props.md:72](./props.md)). Stroke width is configurable via `strokeWidth` ([props.md:73](./props.md)).
2. **Supporting text** _(strongly recommended)_ — a short label rendered next to the spinner. The Oxygen usage page calls this out explicitly: "There should always be supporting text where space permits, as it is best practice to give clear expectations to the user." Passed via the `text` prop ([props.md:75](./props.md), [examples.md:62](./examples.md)).

The Spinner ships no header, footer, or container surface — consuming layouts compose it inside the area being loaded (a card, a dropdown body, a page-level placeholder).

---

## When to use

From the published usage page and the component examples:

- **A whole page or large section is loading and the structure isn't yet known** — use `size="default"` (the standard choice for "page is loading").
- **Modal content is being fetched** before the modal can be populated.
- **A menu, dropdown, or overflow menu** needs to populate from a network call — use `size="small"` so the spinner fits inline.
- **A card or row** is hydrating in place — small, inline contexts.

## When not to use

- **There is a determinate value to show.** The Oxygen usage page is explicit: "When there is a determinate value. Use a progress bar instead." If you can compute "47% done," use ProgressBar, not Spinner.
- **Content-shaped placeholders would communicate more.** When you can show the *shape* of the incoming content (rows in a list, a chart frame, a card grid), prefer Skeleton loaders over a generic spinner — they reduce perceived wait and prevent layout shift.
- **The wait is shorter than ~200 ms.** A spinner that flashes on and off feels janky; either omit it or use an optimistic UI update.
- **As decoration.** Spinner is for loading state only — not for "spinning visual interest."

---

## Do / Don't

### Pair 1 — Use Spinner for indeterminate waits; reach for ProgressBar when you can measure progress

#### ✅ Do — Pick Spinner when you cannot report a percentage

The Oxygen usage page draws this line directly: Spinner is for indeterminate background work — "loading sections or areas such as a page or a dropdown menu." If the task can be measured (file upload bytes transferred, multi-step wizard, batch import), use a progress bar so the user knows how long is left.

```tsx
{/* Right — fetching a record; duration unknown */}
{isLoading ? <Spinner size="default" text="Loading record" /> : <RecordView record={record} />}
```

#### ❌ Don't — Use Spinner where you have a real percentage

A spinner over a 4 GB upload tells the user nothing they didn't already know. They want to see progress.

```tsx
{/* Wrong — measurable progress shown as an indeterminate spinner */}
<Spinner size="default" text={`Uploading… ${bytesSent}/${totalBytes}`} />

{/* Right — use ProgressBar (or equivalent) for known-percentage work */}
<ProgressBar value={bytesSent} max={totalBytes} label="Uploading" />
```

**Source:** <https://oxygen.8x8.com/components/spinner/usage> ("When there is a determinate value. Use a progress bar instead.") · [examples.md:30-58](./examples.md).

---

### Pair 2 — Match `size` to the area being loaded

#### ✅ Do — Use `size="small"` for inline contexts and `size="default"` for page/section loads

The Oxygen usage page defines two clear roles: *default* "used typically when a whole page is being loaded" and *small* "may also be used for inline loading when only a small part of the UI is being loaded (e.g. cards or overflow menus)." Pick the size from the area, not from the aesthetic.

```tsx
{/* Inline — a dropdown is hydrating */}
<DropdownMenu>
  {options.length === 0
    ? <Spinner size="small" text="Loading options" />
    : options.map(renderOption)}
</DropdownMenu>

{/* Page / large section — content is being fetched */}
<main>
  {isLoading
    ? <Spinner size="default" text="Loading conversation" />
    : <Conversation thread={thread} />}
</main>
```

#### ❌ Don't — Use an oversized spinner inside a small container or a tiny spinner for a page load

A `size="default"` spinner inside an overflow menu eats the dropdown; a `size="small"` spinner on an empty page looks lost and reads as a bug rather than a loading state.

```tsx
{/* Wrong — page-sized spinner inside a 32px-tall dropdown row */}
<DropdownMenu><Spinner size="default" /></DropdownMenu>

{/* Wrong — tiny spinner on a full-page loading state */}
<main style={{ minHeight: '80vh' }}><Spinner size="small" /></main>
```

**Source:** <https://oxygen.8x8.com/components/spinner/usage> (Variants — default / small) · [props.md:80-87](./props.md) · [examples.md:35-57](./examples.md).

> ⚠️ A third size key — `"large2x"` — is documented in [props.md:86](./props.md) (sourced from Storybook) but **does not exist in the Figma component set** ([Spinner-audit.md](./Spinner-audit.md) GAP-011). Until that CONFLICT is resolved, prefer `"default"` and `"small"` for new work and treat `"large2x"` as code-only.

---

### Pair 3 — Always pair the spinner with supporting text where space permits

#### ✅ Do — Use the `text` prop so the user knows what is loading

The Oxygen usage page is unambiguous: "There should always be supporting text where space permits, as it is best practice to give clear expectations to the user." A label answers the user's actual question — "is the system frozen, or is *this specific thing* loading?"

```tsx
{/* Right — text scopes the wait to a concrete thing */}
<Spinner size="default" text="Loading conversation history" />

{/* Right — small inline contexts where the surrounding label is enough */}
<DropdownLabel>Contacts <Spinner size="small" aria-label="Loading contacts" /></DropdownLabel>
```

When you use `text`, that string is the accessible label — you do **not** need to also set `aria-label` ([accessibility.md:37](./accessibility.md)). When space genuinely doesn't permit visible text (a 16px inline spinner), fall back to `aria-label` so screen readers still announce the loading state.

#### ❌ Don't — Render a bare spinner with no label of any kind

A spinner with neither `text` nor `aria-label` is silent to screen readers ([accessibility.md:45](./accessibility.md)) and ambiguous to sighted users ("loading… *what*?"). Generic strings like `"Loading"` are technically passing but lose the opportunity to scope the wait.

```tsx
{/* Wrong — no label at all; invisible to screen readers, ambiguous to sighted users */}
<Spinner size="default" />

{/* Weaker — passes a11y but doesn't tell the user what is loading */}
<Spinner size="default" aria-label="Loading" />
```

**Source:** <https://oxygen.8x8.com/components/spinner/usage> (anatomy — "There should always be supporting text where space permits") · [props.md:75](./props.md) · [accessibility.md:36-37](./accessibility.md) · [accessibility.md:45-47](./accessibility.md).

---

### Pair 4 — Respect `prefers-reduced-motion` by toggling `hasAnimation`

#### ✅ Do — Disable the rotation animation for users who have asked for less motion

Spinner's rotation is a continuous animation. For users with `prefers-reduced-motion: reduce`, the responsible default is to stop the rotation and rely on the supporting text (and any surrounding state) to communicate "loading" — preserving meaning while removing the motion.

```tsx
const prefersReducedMotion = useMediaQuery('(prefers-reduced-motion: reduce)');

<Spinner
  size="default"
  text="Loading record"
  hasAnimation={!prefersReducedMotion}
/>
```

#### ❌ Don't — Leave a continuous rotation running for users who opt out of motion

Spinning indicators are one of the patterns motion-sensitive users explicitly opt out of. Ignoring `prefers-reduced-motion` is a WCAG 2.3.3 failure for animated UI.

```tsx
{/* Wrong — rotation runs regardless of the OS preference */}
<Spinner size="default" text="Loading record" />
```

**Source:** [accessibility.md:50-52](./accessibility.md) (motion sensitivity) · [accessibility.md:60](./accessibility.md) (WCAG 2.3.1) · [Spinner-audit.md](./Spinner-audit.md) GAP-004 (WCAG 2.3.3 currently missing from the checklist — adding the row is queued).

> ⚠️ It is currently **unconfirmed** whether the Spinner reads the OS `prefers-reduced-motion` setting automatically or requires the consuming app to wire `hasAnimation={false}` manually ([Spinner-audit.md](./Spinner-audit.md) WARN-002). Until verified against `@8x8/oxygen-loaders` source, do the wiring yourself.

---

### Pair 5 — Reach for Skeleton loaders when the content shape is known; Spinner is for shapeless waits

#### ✅ Do — Use Spinner only when the structure of the incoming content is unknown or trivial

The Oxygen usage page lists Skeleton loader as a related component for a reason: when you can communicate the *shape* of what's coming (rows, cards, a chart), skeletons reduce perceived wait, prevent layout shift, and read as more polished than a centred spinner.

```tsx
{/* Right — content shape is unknown (raw page bootstrap, a modal pulling unknown content) */}
{isBootstrapping
  ? <Spinner size="default" text="Loading workspace" />
  : <Workspace />}

{/* Right — content shape is known: prefer skeletons */}
{isLoading
  ? <ConversationListSkeleton rowCount={10} />
  : <ConversationList items={items} />}
```

#### ❌ Don't — Drop a Spinner into a structured surface where Skeleton would carry more meaning

A spinner centred over a known list shape throws away the chance to anchor the user — the page jumps when content arrives, and the user has no sense of "how many?" or "how big?" until it lands.

```tsx
{/* Wrong — known list shape, but no skeleton; layout jumps on load */}
{isLoading
  ? <div style={{ display: 'grid', placeItems: 'center', minHeight: 400 }}>
      <Spinner size="default" text="Loading conversations" />
    </div>
  : <ConversationList items={items} />}
```

**Source:** <https://oxygen.8x8.com/components/spinner/usage> (Related components — Progress bar, Skeleton loader) · ["When not to use" above](#when-not-to-use).

---

### Pair 6 — Don't stack spinners or use Spinner as decoration

#### ✅ Do — Show one spinner per loading region

If a page is loading, show one page-level spinner; if a card inside that page is independently loading, show one card-level spinner *instead of* the page-level one (whichever scope the user is actually waiting on). Multiple competing spinners on one screen create noise without telling the user anything new.

```tsx
{/* Right — exactly one spinner anchored to the active loading scope */}
{pageLoading
  ? <Spinner size="default" text="Loading workspace" />
  : <Workspace>
      {cardLoading
        ? <Spinner size="small" text="Loading metrics" />
        : <MetricsCard metrics={metrics} />}
    </Workspace>}
```

#### ❌ Don't — Layer spinners or use Spinner where no loading is happening

Multiple spinners on one screen, a spinner that never stops, or a spinner used purely for visual flair all dilute the signal "something is loading." Per the Oxygen usage page the animation is "a seamless and continuous animation that will stop once the page is loaded" — a spinner that never resolves is a UI bug.

```tsx
{/* Wrong — page spinner running while sub-region spinners also run; user can't tell what they're waiting on */}
<Spinner size="default" text="Loading" />
<Spinner size="small" text="Loading metrics" />
<Spinner size="small" text="Loading recents" />

{/* Wrong — decorative use; nothing is actually loading */}
<EmptyState
  illustration={<Spinner size="large2x" />}
  title="No conversations yet"
/>
```

**Source:** <https://oxygen.8x8.com/components/spinner/usage> (Behavior — "seamless and continuous animation that will stop once the page is loaded") · ["When not to use" above](#when-not-to-use).

---

## Gaps

| Item | Description |
|------|-------------|
| Pairs are editorial | No Figma examples page exists for Spinner. Pairs above were drafted from the published Oxygen usage page (<https://oxygen.8x8.com/components/spinner/usage>) plus the extracted MCP files. Replace this file with `figma-extract-usage` output if a `↳ Spinner examples` card-frame page is ever authored. |
| `large2x` size remains in CONFLICT | [Spinner-audit.md](./Spinner-audit.md) GAP-011: `"large2x"` exists in code but not in the Figma component set. Pair 2 warns against new usage until the conflict is resolved; Pair 6 cites it only as a "wrong" example. |
| `isInverted` variant is not addressed | [Spinner-audit.md](./Spinner-audit.md) GAP-010: the Figma `isInverted` variant has no React-prop equivalent. Until the human decision is made — auto-handled by theme, missing prop, or design-only — no Do/Don't pair can responsibly guide its use. |
| `prefers-reduced-motion` behaviour unconfirmed | Pair 4 instructs the consuming app to wire `hasAnimation={false}` manually, per [Spinner-audit.md](./Spinner-audit.md) WARN-002. If `@8x8/oxygen-loaders` is later found to honour the OS preference automatically, Pair 4 should be revised. |
| `role="status"` is inferred | [Spinner-audit.md](./Spinner-audit.md) WARN-001: the live-region role is inferred, not confirmed against rendered DOM. None of the pairs above depend on it directly, but if the rendered role differs the accessibility wording should be reconfirmed. |
| Audit verdict remains `NO` | Producing this editorial doc closes [Spinner-audit.md](./Spinner-audit.md) GAP-005 (usage SOURCE_GAP) but does **not** clear the two CONFLICTs (GAP-010, GAP-011) that block `doc-rewrite`. |

---

_Source: Editorial draft from <https://oxygen.8x8.com/components/spinner/usage> + extracted MCP artifacts · Drafted 2026-05-15_
