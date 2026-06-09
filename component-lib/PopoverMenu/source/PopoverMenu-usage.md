---
component: PopoverMenu
package: "@8x8/oxygen-popover"
category: overlays_contextual
role: usage
role_description: "Usage guidelines — editorial, drafted via usage-advisor from extracted MCP/Figma artifacts and the prior prose-only Figma examples page"
pipeline_stage: editorial
pipeline_note: "Pairs are editorial. The Figma `↳ Popover examples` page contains prose guidelines only — no Do/Don't card frames exist. Replace with figma-extract-usage output when a Figma examples page with cards is created. Audit verdict for the component (PopoverMenu-audit.md) remains NO until GAP-001 / GAP-002 / GAP-003 are resolved — those CONFLICTs are surfaced inline in this doc but do not block the usage layer."
source_type: editorial
audit_verdict: null
siblings:
  - "[[PopoverMenu/props]]"
  - "[[PopoverMenu/examples]]"
  - "[[PopoverMenu/tokens]]"
  - "[[PopoverMenu/accessibility]]"
  - "[[PopoverMenu/PopoverMenu-figma]]"
  - "[[PopoverMenu/PopoverMenu-audit]]"
tags:
  - oxygen
  - component/PopoverMenu
  - role/usage
  - stage/editorial
  - category/overlays_contextual
---
<!-- SOURCE: editorial — drafted via usage-advisor from PopoverMenu-figma.md + props.md + examples.md + accessibility.md + the prior prose-only PopoverMenu-usage.md -->
<!-- FIGMA EXAMPLES PAGE: `↳ Popover examples` (node 49969:10533) — prose-only, no ✅ Do / ❌ Don't card frames -->
<!-- GROUNDING: full — props.md, examples.md, tokens.md, accessibility.md, PopoverMenu-figma.md, PopoverMenu-audit.md all present and read -->
<!-- DRAFTED: 2026-05-13 -->
<!-- MODE: open -->
<!-- PAIRS: 8 -->
<!-- STATUS: editorial draft — replace with figma-extract-usage output if Figma cards are later authored -->

# PopoverMenu — Usage Guidelines

> **See also:** [props.md](./props.md) · [examples.md](./examples.md) · [tokens.md](./tokens.md) ·
> [accessibility.md](./accessibility.md) · [PopoverMenu-figma.md](./PopoverMenu-figma.md) · [PopoverMenu-audit.md](./PopoverMenu-audit.md)

> **Editorial guidance — mirrors `Button-usage.md`.** No `↳ Popover examples` Figma page with Do/Don't card frames exists yet ([PopoverMenu-figma.md](./PopoverMenu-figma.md) and the prior version of this file confirm prose-only content). The guidance below is drafted from the extracted artifacts and is intended to be replaced by `figma-extract-usage` output once card frames are authored in Figma.

Popovers display rich, dismissible content anchored to a trigger — somewhere between a tooltip (too small) and a modal (too disruptive). `PopoverMenu` is the menu-shaped specialisation: a list of items that lets a user pick one (or several), wrapped in the same floating panel. Use it for dropdown menus, multi-select filters, and contextual command lists.

---

## Anatomy

Element structure of the Popover window from [PopoverMenu-figma.md:46-67](./PopoverMenu-figma.md):

1. **Trigger** — any focusable element (typically a `DropdownButton`, [examples.md:30](./examples.md)). Owns the accessible name of the menu — see [accessibility.md:74](./accessibility.md).
2. **Container (`Popover window`)** — the floating panel shell ([PopoverMenu-figma.md:52](./PopoverMenu-figma.md)). Carries the surface tokens (`--ui/ui06` background, `--ui/ui01` border, `--ui/shadow01`) and a hardcoded `6px` radius / `320px` width — flagged in [PopoverMenu-figma.md:291-293](./PopoverMenu-figma.md).
3. **`_header` slot** _(optional, `header={...}`)_ — Title row + close icon + search input + bottom divider ([PopoverMenu-figma.md:60-63](./PopoverMenu-figma.md)). Shown only when `header` is provided ([props.md:105](./props.md)).
4. **`Content`** — always present; wraps the `Slot` (the actual list of items) and an optional `Scrollbar_Mac OS` when `scroll=true` ([PopoverMenu-figma.md:62-64](./PopoverMenu-figma.md)).
5. **`_footer` slot** _(optional, `footer={...}`)_ — Top divider + `Buttons` row (Clear / Cancel / Apply) ([PopoverMenu-figma.md:65-67](./PopoverMenu-figma.md)). Shown only when `footer` is provided ([props.md:106](./props.md)).
6. **List items** — eight variants populate `items` ([PopoverMenu-figma.md:75-82](./PopoverMenu-figma.md)). See the Overview matrix.
7. **Focus ring** — visible focus indicator on the focused list item, applied via the keyboard arrow / `Tab` flow. Required by WCAG 2.4.7 — see [accessibility.md:89](./accessibility.md).

---

## Overview

The `@8x8/oxygen-popover` package ships two distinct components ([props.md:48-55](./props.md)):

| Component | When to use | Notes |
|---|---|---|
| `PopoverMenu` | Standard dropdown menus — the floating panel renders a structured list driven by `items`. Open state is managed for you. | **Default choice.** See Pair 1. |
| `Popover` | Custom floating content that doesn't fit a list — forms, previews, controlled programmatic open. | Fully controlled (`isOpen` / `setIsOpen`); requires you to pass `floatingContent`. See Pair 1. |

### List-item type matrix

Eight list-item variants are defined on the canvas ([PopoverMenu-figma.md:75-82](./PopoverMenu-figma.md)). Pick by selection semantics, not by appearance:

| Variant | Selection model | Use for | Notes |
|---|---|---|---|
| `List item/Single Action or Select` | None / single-select | One-shot commands ("Edit", "Duplicate") or single-select picks | Most common. See Pair 7. |
| `List item/Sub Menu` | Navigation | Branching into a nested menu | Trailing chevron; opens a child PopoverMenu. |
| `List item/Checkbox` | Multi-select | Filter facets, tag pickers — committed in batch | Pair with `footer` (Clear / Cancel / Apply). See Pair 6, Pair 7. |
| `List item/Radio` | Single-select from N | Pick exactly one value from a known set | Commits on click — no Apply step. See Pair 7. |
| `List item/Add Item` | Action | Append a new entry to a list | Leading `+` icon. |
| `List item/Remove Item` | Destructive | Remove an entry from a list | Trailing trash icon; treat like Destructive. See Pair 8. |
| `List item/Destructive` | Destructive | Irreversible commands ("Delete", "Sign out") | Always last, always separated. See Pair 8. |
| `List item/Collapsible` | Group disclosure | Reveal a nested sub-group inline (108px tall when open) | Section grouping alternative. |

> ⚠️ **Token / data conflicts** flagged in [PopoverMenu-audit.md](./PopoverMenu-audit.md):
> - **GAP-001 (CONFLICT):** The MCP story `Popover.documentation.stories.tsx` renders the canonical example using `<Popover items={...}>` — but `items` belongs to `PopoverMenu`, not `Popover` ([examples.md:48](./examples.md)). Treat the snippets in this doc as **`PopoverMenu`-correct**; verify against source before copying from the published story.
> - **GAP-002 (CONFLICT):** Footer button row padding differs between light (`8px 8px 0 8px`) and dark (`8px 12px 0 12px`) — Figma source inconsistency. See Pair 6.
> - **GAP-003 (CONFLICT):** `--text/textcolor09` (black) on `--actions/action09` (`#4687ed`) in dark mode is approximately 3.4:1 contrast — below WCAG 4.5:1. See Pair 6.

**Source:** [props.md:48-55](./props.md) · [PopoverMenu-figma.md:75-82](./PopoverMenu-figma.md) · [PopoverMenu-audit.md](./PopoverMenu-audit.md).

---

## Behaviour

### List-item states

States live on the list items, not on the container ([PopoverMenu-figma.md:255-265](./PopoverMenu-figma.md)):

| # | State | Trigger | Visual change |
|---|-------|---------|---------------|
| 1 | Rest | Default | Item at its base surface; no tint |
| 2 | Hover | Pointer over item | Background tint shifts (hover surface) |
| 3 | Active | Pointer pressed / `Enter` / `Space` | Pressed visual feedback |
| 4 | Focus | Keyboard `Tab` / `ArrowDown` / `ArrowUp` | Visible focus ring on the focused item |
| 5 | Disabled | `isDisabled=true` on the item | Reduced opacity; non-interactive, still focusable, `aria-disabled="true"` ([accessibility.md:76](./accessibility.md)) |

Token coverage is roughly 60% with several hardcoded values (radius, width, padding) — see [PopoverMenu-figma.md:140-152](./PopoverMenu-figma.md). The container itself does not expose state variants — open / closed is purely a render decision driven by `isOpen` (`Popover`) or internal state (`PopoverMenu`).

### Keyboard contract

From [accessibility.md:49-58](./accessibility.md) (inferred from the ARIA Menu Button pattern — explicit annotation is a `SOURCE_GAP`):

| Key | Behaviour |
|---|---|
| `Enter` / `Space` on trigger | Opens menu, focus moves to first item |
| `ArrowDown` / `ArrowUp` | Move focus through items |
| `Home` / `End` | Jump to first / last item |
| `Escape` | Close menu, return focus to trigger |
| `Tab` | Close menu, advance focus to next focusable element |
| `Enter` on focused item | Activate the item |

**Source:** [PopoverMenu-figma.md:255-265](./PopoverMenu-figma.md) · [accessibility.md:49-67](./accessibility.md).

---

## When to use

- Choosing one or many options from a structured list (filter facets, sort orders, view picks)
- Contextual command menus anchored to a trigger ("…" overflow, row actions in a table)
- Rich helper content that's too long for a tooltip but doesn't justify a Modal — supplementary explanations, previews, profile cards
- Forms or interactive controls that should sit inline next to their trigger

## When not to use

- **Single-sentence labels or hints** — use a Tooltip
- **Critical, workflow-blocking decisions** — use a Modal (Popovers dismiss too easily)
- **Multi-step workflows** — use a dedicated page or Modal
- **Mobile-first surfaces with very limited width** — the panel is 320px wide and hardcoded ([PopoverMenu-figma.md:220-223](./PopoverMenu-figma.md)); consider a Bottom Sheet pattern instead

---

## Do / Don't

### Pair 1 — Pick `PopoverMenu` for menus, `Popover` for custom floating content

#### ✅ Do — Use `PopoverMenu` with the `items` array for list-shaped menus

`PopoverMenu` manages open state, keyboard navigation, and item rendering for you. It's the right answer ~90% of the time.

```tsx
import { PopoverMenu } from '@8x8/oxygen-popover';
import { DropdownButton } from '@8x8/oxygen-button';

<PopoverMenu
  items={[
    { key: 'edit', children: 'Edit' },
    { key: 'duplicate', children: 'Duplicate' },
    { key: 'archive', children: 'Archive' },
  ]}
  onMenuItemClick={(event) => handleAction(event)}
>
  <DropdownButton>Actions</DropdownButton>
</PopoverMenu>
```

#### ❌ Don't — Reach for the low-level `Popover` just to render a list

Re-implementing menu rendering, open-state, and keyboard handling on top of `Popover` rebuilds what `PopoverMenu` already gives you — and it skips the standard list-item variants from Figma.

```tsx
{/* Wrong — manually rebuilding the menu on the primitive */}
const [isOpen, setIsOpen] = useState(false);
<Popover
  isOpen={isOpen}
  setIsOpen={setIsOpen}
  floatingContent={
    <ul>
      <li onClick={...}>Edit</li>
      <li onClick={...}>Duplicate</li>
    </ul>
  }
>
  <button onClick={() => setIsOpen(!isOpen)}>Actions</button>
</Popover>
```

Reserve `Popover` for cases where the floating content is genuinely not a list — e.g. a tiny inline form, a chart, or a preview card.

**Source:** [props.md:48-112](./props.md) · [examples.md:30-69](./examples.md).

---

### Pair 2 — Use Popover for rich content, Tooltip for labels, Modal for blocking decisions

#### ✅ Do — Match the affordance to content density and dismissibility

Popovers are **interactive, persistent, and dismissible**. They host rich content (lists, forms, previews) without taking over the page.

```tsx
{/* Right — filter facets in a dismissible panel; doesn't block the page */}
<PopoverMenu
  header={<>Filter results</>}
  footer={<ApplyCancel onApply={apply} onCancel={cancel} />}
  items={facets}
>
  <DropdownButton>Filters</DropdownButton>
</PopoverMenu>
```

#### ❌ Don't — Use Popover for tooltips or blocking confirmations

A Popover for a one-line hint is overkill (and forces a click). A Popover for "Are you sure you want to delete this account?" is dangerous — users routinely dismiss popovers by clicking outside, and `Escape` cancels them with no commit.

```tsx
{/* Wrong — should be a Tooltip */}
<PopoverMenu items={[{ key: 'i', children: 'Open in new tab' }]}>
  <IconButton icon={<InfoIcon />} aria-label="Info" />
</PopoverMenu>

{/* Wrong — should be a Modal; outside-click dismisses without confirmation */}
<PopoverMenu items={[{ key: 'd', children: 'Delete account permanently', isDestructive: true }]}>
  <Button variant="primary">Settings</Button>
</PopoverMenu>
```

**Source:** "When to use" / "When not to use" sections above · [accessibility.md:52](./accessibility.md) (Escape closes without commit).

---

### Pair 3 — Trigger PopoverMenu on click, not on hover

#### ✅ Do — Open on click / `Enter` / `Space`

A click-triggered menu is reachable by keyboard, touch, and pointer users alike. It's the default behaviour when you pair `PopoverMenu` with a focusable trigger ([accessibility.md:51](./accessibility.md)).

```tsx
<PopoverMenu items={items}>
  <DropdownButton>Sort by</DropdownButton>
</PopoverMenu>
```

#### ❌ Don't — Open the menu on hover

Hover triggers are easy to activate by accident on desktop, are unavailable on touch devices, and (most importantly) are not reachable for keyboard or screen-reader users. The trigger's accessible name still has to invite a click — see [accessibility.md:74](./accessibility.md).

```tsx
{/* Wrong — re-implementing hover-to-open on the primitive */}
<Popover
  isOpen={isHovered}
  setIsOpen={setIsHovered}
  floatingContent={<Menu />}
>
  <span onMouseEnter={() => setIsHovered(true)}>Sort by ▾</span>
</Popover>
```

**Source:** [accessibility.md:51](./accessibility.md) (Enter / Space activation) · [accessibility.md:74-77](./accessibility.md) (screen-reader expectations).

---

### Pair 4 — Make dismissal predictable: outside click, `Escape`, plus an explicit close affordance when there's a header

#### ✅ Do — Provide all three dismissal paths and return focus to the trigger

All Oxygen popovers should dismiss on outside click and on `Escape` ([accessibility.md:52](./accessibility.md), [accessibility.md:66-67](./accessibility.md)). When `header` is shown, also include a visible close `×` so the dismissal is discoverable for pointer users.

```tsx
<PopoverMenu
  header={
    <PanelHeader title="User profile" onClose={closeMenu} /* ← visible × */ />
  }
  items={profileItems}
  onCancel={closeMenu} // fires on Escape / outside click
>
  <DropdownButton>Profile</DropdownButton>
</PopoverMenu>
```

#### ❌ Don't — Replace the standard dismissal model with auto-dismiss-on-mouseleave, or hide every dismissal affordance

Suppressing `Escape`, swallowing the outside click, or auto-closing the panel when the pointer leaves it all break the predictability users rely on — and the `Escape`/focus-return behaviour is a hard a11y requirement.

```tsx
{/* Wrong — Escape and outside-click silently disabled; panel only closes on mouseleave */}
<Popover
  isOpen={isOpen}
  setIsOpen={() => { /* ignore Escape & outside click */ }}
>
  <div onMouseLeave={() => setIsOpen(false)}>{menuBody}</div>
</Popover>
```

**Source:** [accessibility.md:52](./accessibility.md) · [accessibility.md:66-67](./accessibility.md) · [props.md:110](./props.md) (`onCancel`).

---

### Pair 5 — Use the `header` slot only when a title or search adds real value

#### ✅ Do — Add `header` when the menu has enough items to need a search field, or when the menu is decoupled enough from the trigger to need a title

The `_header` frame is built specifically around a title row plus a search input ([PopoverMenu-figma.md:60-61](./PopoverMenu-figma.md)). It pays for itself when the list is long ("Assign to user") or when the trigger doesn't fully name the menu's purpose.

```tsx
<PopoverMenu
  header={<MenuHeader title="Assign to" onClose={close} showSearch />}
  items={teammates}        // ~40 entries
  maxHeight={400}
  scroll
>
  <DropdownButton>Assignee</DropdownButton>
</PopoverMenu>
```

#### ❌ Don't — Add a header to a three-item menu

A title row on a short, well-labelled menu just adds vertical weight and a redundant restatement of the trigger label. The trigger already names the menu — let the items do the talking.

```tsx
{/* Wrong — header bigger than the menu itself */}
<PopoverMenu
  header={<MenuHeader title="Sort by" />}
  items={[
    { key: 'name', children: 'Name' },
    { key: 'date', children: 'Date modified' },
    { key: 'size', children: 'Size' },
  ]}
>
  <DropdownButton>Sort by</DropdownButton>
</PopoverMenu>
```

**Source:** [PopoverMenu-figma.md:60-63](./PopoverMenu-figma.md) (header anatomy) · [props.md:105](./props.md).

---

### Pair 6 — Use the `footer` (Clear / Cancel / Apply) for batch commits — and only for batch commits

#### ✅ Do — Pair `footer` with multi-select (Checkbox) lists where the user assembles a selection then commits

The footer's button row is shaped for batch operations: **Clear** (reset the selection), **Cancel** (discard and close), **Apply** (commit the selection) ([PopoverMenu-figma.md:65-67](./PopoverMenu-figma.md)). It only earns its real estate when there's something to commit.

```tsx
<PopoverMenu
  items={facets.map((f) => ({
    key: f.id,
    children: f.label,
    type: 'checkbox',
    checked: draftSelection.includes(f.id),
  }))}
  footer={
    <FilterFooter
      onClear={() => setDraftSelection([])}
      onCancel={cancel}
      onApply={() => applyFilters(draftSelection)}
    />
  }
>
  <DropdownButton>Filters ({applied.length})</DropdownButton>
</PopoverMenu>
```

#### ❌ Don't — Add a footer to a single-action or single-select menu

For "Edit / Duplicate / Delete" or a Radio-list "pick one", the click is the commit — there's nothing for Apply to commit. A footer on these surfaces forces an extra click and confuses Radio's "click commits" semantics.

```tsx
{/* Wrong — footer on a Single Action menu */}
<PopoverMenu
  items={[
    { key: 'edit', children: 'Edit' },
    { key: 'duplicate', children: 'Duplicate' },
  ]}
  footer={<FilterFooter onApply={...} onCancel={...} />}
>
  <DropdownButton>Actions</DropdownButton>
</PopoverMenu>
```

> ⚠️ **Audit warnings apply to this pair** — flagged in [PopoverMenu-audit.md](./PopoverMenu-audit.md):
> - **GAP-002 (CONFLICT):** Footer button row padding differs between light (`8px 8px 0 8px`) and dark (`8px 12px 0 12px`) modes — Figma source inconsistency. Treat the light-mode value as authoritative until a designer confirms.
> - **GAP-003 (CONFLICT):** The Apply button's text token (`--text/textcolor09` → black) on its background token (`--actions/action09` → `#4687ed`) in dark mode is roughly 3.4:1 — below WCAG 4.5:1. Don't hand-restyle around it; wait for the token decision.

**Source:** [PopoverMenu-figma.md:65-67](./PopoverMenu-figma.md) · [PopoverMenu-figma.md:194-202](./PopoverMenu-figma.md) · [PopoverMenu-audit.md](./PopoverMenu-audit.md) GAP-002, GAP-003.

---

### Pair 7 — Match the list-item variant to the selection model

#### ✅ Do — Pick Single Action, Radio, or Checkbox by what the data needs

Three different list-item variants exist for three different selection models ([PopoverMenu-figma.md:75-82](./PopoverMenu-figma.md)). Mapping the variant to the underlying data model is the single biggest signal users have about what clicking will do.

```tsx
{/* One-shot commands → Single Action */}
<PopoverMenu items={[
  { key: 'edit',      children: 'Edit' },
  { key: 'duplicate', children: 'Duplicate' },
]}>...</PopoverMenu>

{/* Pick exactly one → Radio; commits on click */}
<PopoverMenu items={[
  { key: 'name', children: 'Name',          type: 'radio', checked: sort === 'name' },
  { key: 'date', children: 'Date modified', type: 'radio', checked: sort === 'date' },
  { key: 'size', children: 'Size',          type: 'radio', checked: sort === 'size' },
]}>...</PopoverMenu>

{/* Pick many → Checkbox; commit in batch via footer (see Pair 6) */}
<PopoverMenu items={facets.map((f) => ({
  key: f.id, children: f.label, type: 'checkbox', checked: draft.includes(f.id),
}))} footer={<FilterFooter ... />}>...</PopoverMenu>
```

#### ❌ Don't — Use Checkbox for a single-select choice, or Radio for a multi-select filter

Checkbox tells users "you can pick more than one." Radio tells users "exactly one." Swapping them lies about the data model and leads to immediate confusion — users tick a second Checkbox expecting both to apply, or click a second Radio expecting it to add (and watch the first one quietly clear).

```tsx
{/* Wrong — Checkbox for a single-select sort */}
<PopoverMenu items={[
  { key: 'name', children: 'Name', type: 'checkbox' },
  { key: 'date', children: 'Date', type: 'checkbox' },
]}>...</PopoverMenu>
```

**Source:** [PopoverMenu-figma.md:75-78](./PopoverMenu-figma.md) (Single Action, Checkbox, Radio variants with `selection: true / false / indeterminate`).

---

### Pair 8 — Place destructive items last, separate them with a Divider, and confirm the irreversible ones

#### ✅ Do — Group destructive items at the end of the menu, preceded by a `Section header and divider/Divider`, and pair irreversible ones with a confirmation step

The Figma library ships dedicated `List item/Destructive` and `List item/Remove Item` variants ([PopoverMenu-figma.md:76,82](./PopoverMenu-figma.md)) with the destructive red treatment, and a separate `Divider` atom ([PopoverMenu-figma.md:89](./PopoverMenu-figma.md)). Use them — and follow the Button precedent of confirming any irreversible action in a Modal ([Button-usage.md:221](../Button/Button-usage.md), Pair 3).

```tsx
<PopoverMenu
  items={[
    { key: 'edit',      children: 'Edit' },
    { key: 'duplicate', children: 'Duplicate' },
    { key: 'archive',   children: 'Archive' },
    '---', // divider
    { key: 'delete',    children: 'Delete', isDestructive: true,
      onClick: () => openConfirmModal('delete') },
  ]}
>
  <DropdownButton>Actions</DropdownButton>
</PopoverMenu>
```

#### ❌ Don't — Sprinkle destructive items among neutral actions, or treat outside-click as undo

Without separation, a destructive item is one accidental click away from the user's pointer. And because Popovers dismiss on `Escape` and outside click with no confirmation ([accessibility.md:52](./accessibility.md)), the popover itself can never be the undo path for a destructive command.

```tsx
{/* Wrong — destructive Delete sits between neutral commands, no divider, no confirmation */}
<PopoverMenu items={[
  { key: 'edit',      children: 'Edit' },
  { key: 'delete',    children: 'Delete', isDestructive: true,
    onClick: () => deleteImmediately() }, // no confirmation modal
  { key: 'duplicate', children: 'Duplicate' },
]}>
  <DropdownButton>Actions</DropdownButton>
</PopoverMenu>
```

**Source:** [PopoverMenu-figma.md:76](./PopoverMenu-figma.md) (List item/Destructive) · [PopoverMenu-figma.md:82](./PopoverMenu-figma.md) (List item/Remove Item) · [PopoverMenu-figma.md:89](./PopoverMenu-figma.md) (Divider atom) · [accessibility.md:52](./accessibility.md) · Button-usage.md Pair 3 precedent.

---

## Gaps

| Item | Description |
|------|-------------|
| Pairs are editorial | The Figma `↳ Popover examples` page contains prose guidelines only — no `✅ Do —` / `❌ Don't —` card frames exist. Pairs above were authored via `usage-advisor`. Replace this file with `figma-extract-usage` output once card frames are authored in Figma. |
| Audit verdict still `NO` | [PopoverMenu-audit.md](./PopoverMenu-audit.md) holds 3 unresolved CONFLICTs (GAP-001 example naming, GAP-002 footer padding light/dark, GAP-003 Apply-button contrast). These are surfaced inline above where they affect specific pairs, but resolving them is the audit team's job, not this doc's. |
| `Divider` / `SectionHeader` / `ListItem` sub-component props | Not registered in the Oxygen MCP ([props.md:117](./props.md)) — the `items` shapes in the code snippets above (`isDestructive`, `type: 'radio' | 'checkbox'`, `checked`, `'---'` divider sentinel) are illustrative and should be replaced with the real API once the MCP surfaces it. |
| Desktop Bridge not connected during extraction | `figma_get_selection` returned a WebSocket error during the original prose extraction — see prior pipeline notes. Any future `figma-extract-usage` run will need the bridge connected to capture actual card frames. |

---

_Source: Editorial draft via usage-advisor · Drafted 2026-05-13_
