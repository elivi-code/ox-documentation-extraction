---
component: PopoverMenu
parent: "[[PopoverMenu]]"
section: usage
pipeline_stage: draft
audit_verdict: "NO"
source_type: editorial
siblings:
  - "[[PopoverMenu]]"
  - "[[PopoverMenu.props]]"
  - "[[PopoverMenu.anatomy]]"
  - "[[PopoverMenu.tokens]]"
  - "[[PopoverMenu.accessibility]]"
  - "[[PopoverMenu.platform]]"
  - "[[PopoverMenu.composition]]"
tags:
  - oxygen
  - component/PopoverMenu
  - role/usage
  - stage/draft
  - category/overlays_contextual
---

<!-- STUB:GAP-007 source="Ask designer to author Do/Don't card frames on the ↳ Popover examples Figma page (node 49969:10533); re-run figma-extract-usage after cards are added. Current pairs are editorial — replace with figma-extract-usage output once card frames exist." -->

> **Editorial guidance.** The Figma `↳ Popover examples` page contains prose guidelines only — no `✅ Do —` / `❌ Don't —` card frames have been authored. The 8 pairs below are drafted from extracted artifacts. Replace with `figma-extract-usage` output once Figma cards are created.

Popovers display rich, dismissible content anchored to a trigger — between a tooltip (too small) and a modal (too disruptive). `PopoverMenu` is the menu-shaped specialisation: a list of items that lets a user pick one (or several), wrapped in the same floating panel.

---

## When to use

- Choosing one or many options from a structured list (filter facets, sort orders, view picks)
- Contextual command menus anchored to a trigger ("…" overflow, row actions in a table)
- Rich helper content that's too long for a tooltip but doesn't justify a Modal
- Forms or interactive controls that should sit inline next to their trigger

## When not to use

- **Single-sentence labels or hints** — use a Tooltip
- **Critical, workflow-blocking decisions** — use a Modal (Popovers dismiss too easily)
- **Multi-step workflows** — use a dedicated page or Modal
- **Mobile-first surfaces with very limited width** — the panel is 320px wide and hardcoded

---

## Do / Don't

### Pair 1 — Pick `PopoverMenu` for menus, `Popover` for custom floating content

#### ✅ Do — Use `PopoverMenu` with the `items` array for list-shaped menus

`PopoverMenu` manages open state, keyboard navigation, and item rendering for you.

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

Re-implementing menu rendering, open-state, and keyboard handling on top of `Popover` rebuilds what `PopoverMenu` already gives you.

```tsx
{/* Wrong — manually rebuilding the menu on the primitive */}
const [isOpen, setIsOpen] = useState(false);
<Popover isOpen={isOpen} setIsOpen={setIsOpen}
  floatingContent={<ul><li onClick={...}>Edit</li></ul>}
>
  <button onClick={() => setIsOpen(!isOpen)}>Actions</button>
</Popover>
```

Reserve `Popover` for cases where the floating content is genuinely not a list — e.g. a tiny inline form, a chart, or a preview card.

---

### Pair 2 — Use Popover for rich content, Tooltip for labels, Modal for blocking decisions

#### ✅ Do — Match the affordance to content density and dismissibility

Popovers are interactive, persistent, and dismissible. They host rich content without taking over the page.

```tsx
<PopoverMenu
  header={<>Filter results</>}
  footer={<ApplyCancel onApply={apply} onCancel={cancel} />}
  items={facets}
>
  <DropdownButton>Filters</DropdownButton>
</PopoverMenu>
```

#### ❌ Don't — Use Popover for tooltips or blocking confirmations

A Popover for a one-line hint is overkill. A Popover for "Are you sure?" is dangerous — users routinely dismiss popovers by clicking outside.

---

### Pair 3 — Trigger PopoverMenu on click, not on hover

#### ✅ Do — Open on click / `Enter` / `Space`

A click-triggered menu is reachable by keyboard, touch, and pointer users alike.

```tsx
<PopoverMenu items={items}>
  <DropdownButton>Sort by</DropdownButton>
</PopoverMenu>
```

#### ❌ Don't — Open the menu on hover

Hover triggers are easy to activate by accident on desktop, unavailable on touch, and not reachable for keyboard or screen-reader users.

---

### Pair 4 — Make dismissal predictable: outside click, `Escape`, plus explicit close when there's a header

#### ✅ Do — Provide all three dismissal paths and return focus to the trigger

All Oxygen popovers should dismiss on outside click and on `Escape`. When `header` is shown, also include a visible close `×`.

```tsx
<PopoverMenu
  header={<PanelHeader title="User profile" onClose={closeMenu} />}
  items={profileItems}
  onCancel={closeMenu}
>
  <DropdownButton>Profile</DropdownButton>
</PopoverMenu>
```

#### ❌ Don't — Replace the standard dismissal model or hide every dismissal affordance

Suppressing `Escape` or swallowing outside clicks breaks the predictability users rely on.

---

### Pair 5 — Use the `header` slot only when a title or search adds real value

#### ✅ Do — Add `header` when the menu has enough items to need a search field

```tsx
<PopoverMenu
  header={<MenuHeader title="Assign to" onClose={close} showSearch />}
  items={teammates}
  maxHeight={400}
>
  <DropdownButton>Assignee</DropdownButton>
</PopoverMenu>
```

#### ❌ Don't — Add a header to a three-item menu

A title row on a short, well-labelled menu adds vertical weight and restates the trigger label redundantly.

---

### Pair 6 — Use the `footer` (Clear / Cancel / Apply) for batch commits — and only for batch commits

#### ✅ Do — Pair `footer` with multi-select (Checkbox) lists where the user assembles a selection then commits

```tsx
<PopoverMenu
  items={facets.map((f) => ({ key: f.id, children: f.label, type: 'checkbox', checked: draft.includes(f.id) }))}
  footer={<FilterFooter onClear={() => setDraft([])} onCancel={cancel} onApply={() => apply(draft)} />}
>
  <DropdownButton>Filters</DropdownButton>
</PopoverMenu>
```

#### ❌ Don't — Add a footer to a single-action or single-select menu

For command menus or Radio-lists, the click is the commit — Apply adds a redundant step.

> ⚠️ **Audit conflicts apply:**
> - **GAP-002 (CONFLICT):** Footer button row padding differs between light (`8px 8px 0 8px`) and dark (`8px 12px 0 12px`) modes — Figma source inconsistency. Treat the light-mode value as authoritative until a designer confirms.
> - **GAP-003 (CONFLICT):** The Apply button's text token (`--text/textcolor09` → black) on its dark-mode background token (`--actions/action09` → `#4687ed`) is roughly 3.4:1 — below WCAG 4.5:1. Don't hand-restyle; wait for the token decision.

---

### Pair 7 — Match the list-item variant to the selection model

#### ✅ Do — Pick Single Action, Radio, or Checkbox by what the data needs

```tsx
{/* One-shot commands → Single Action */}
<PopoverMenu items={[{ key: 'edit', children: 'Edit' }, { key: 'dup', children: 'Duplicate' }]}>...</PopoverMenu>

{/* Pick exactly one → Radio; commits on click */}
<PopoverMenu items={[
  { key: 'name', children: 'Name', type: 'radio', checked: sort === 'name' },
  { key: 'date', children: 'Date', type: 'radio', checked: sort === 'date' },
]}>...</PopoverMenu>

{/* Pick many → Checkbox; commit via footer */}
<PopoverMenu items={facets.map((f) => ({ key: f.id, children: f.label, type: 'checkbox', checked: draft.includes(f.id) }))}
  footer={<FilterFooter ... />}>...</PopoverMenu>
```

#### ❌ Don't — Use Checkbox for a single-select choice, or Radio for a multi-select filter

Checkbox tells users "you can pick more than one." Radio tells users "exactly one." Swapping them lies about the data model.

---

### Pair 8 — Place destructive items last, separate them with a Divider, and confirm the irreversible ones

#### ✅ Do — Group destructive items at the end, preceded by a Divider, and pair with a confirmation step

```tsx
<PopoverMenu
  items={[
    { key: 'edit', children: 'Edit' },
    { key: 'duplicate', children: 'Duplicate' },
    '---',
    { key: 'delete', children: 'Delete', isDestructive: true, onClick: () => openConfirmModal('delete') },
  ]}
>
  <DropdownButton>Actions</DropdownButton>
</PopoverMenu>
```

#### ❌ Don't — Sprinkle destructive items among neutral actions, or treat outside-click as undo

Without separation, a destructive item is one accidental click away. Popovers dismiss on `Escape` and outside click with no confirmation — they cannot be the undo path for a destructive command.

---

_Source: Editorial draft via usage-advisor · Drafted 2026-05-13_
