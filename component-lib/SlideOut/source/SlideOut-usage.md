---
component: SlideOut
package: "@8x8/oxygen-slide-out"
category: layout_overlay
role: usage
role_description: "Usage guidelines — editorial, drafted via usage-advisor from extracted MCP artifacts; no Figma source exists"
pipeline_stage: editorial
pipeline_note: "Pairs are editorial. No Figma design exists for SlideOut (SlideOut-audit.md GAP-001 / GAP-002 are blocker SOURCE_GAPs). Replace with figma-extract-usage output if a Figma design with a `↳ SlideOut examples` card-frame page is eventually authored. Audit verdict remains PARTIAL until upstream Figma exists."
source_type: editorial
audit_verdict: null
siblings:
  - "[[SlideOut/props]]"
  - "[[SlideOut/examples]]"
  - "[[SlideOut/tokens]]"
  - "[[SlideOut/accessibility]]"
  - "[[SlideOut/SlideOut-audit]]"
tags:
  - oxygen
  - component/SlideOut
  - role/usage
  - stage/editorial
  - category/layout_overlay
---
<!-- SOURCE: editorial — drafted via usage-advisor from props.md + examples.md + accessibility.md + SlideOut-audit.md -->
<!-- FIGMA EXAMPLES PAGE: none — no Figma design exists for SlideOut (SlideOut-audit.md GAP-001) -->
<!-- GROUNDING: degraded — props.md, examples.md, accessibility.md present; tokens.md empty (SOURCE_GAP); no figma.md; no pui.md -->
<!-- DRAFTED: 2026-05-15 -->
<!-- MODE: open -->
<!-- PAIRS: 7 -->
<!-- STATUS: editorial draft — replace with figma-extract-usage output if Figma cards are ever authored -->

# SlideOut — Usage Guidelines

> **See also:** [props.md](./props.md) · [examples.md](./examples.md) · [tokens.md](./tokens.md) ·
> [accessibility.md](./accessibility.md) · [SlideOut-audit.md](./SlideOut-audit.md)

> **Editorial guidance — no Figma design exists for SlideOut.** This file was drafted via `usage-advisor` Open mode from [props.md](./props.md), [examples.md](./examples.md), and [accessibility.md](./accessibility.md). It does **not** resolve [SlideOut-audit.md](./SlideOut-audit.md) **GAP-001** (no `SlideOut-figma.md`) or **GAP-002** (no Figma examples page), which remain blocked on upstream Figma design work. Replace this file wholesale with `figma-extract-usage` output once a `↳ SlideOut examples` page with `✅ Do — …` / `❌ Don't — …` card frames is authored. The mirrored precedent is [PopoverMenu-usage.md](../PopoverMenu/PopoverMenu-usage.md).

`SlideOut` is a controlled side panel that animates in over the trailing edge of the page. Unlike a Modal, it does not block the rest of the UI; unlike a navigation Drawer, it is intended to be opened in response to a specific user intent and then dismissed. The component is deliberately thin — it renders a resizable container and a visibility flag, and **expects the consuming application to wire up dismissal, focus management, and accessible labelling itself** ([accessibility.md:45](./accessibility.md)).

---

## Anatomy

> **No Figma source exists.** Anatomy below is inferred from [props.md:55-65](./props.md) and the controlled-toggle example in [examples.md:30-58](./examples.md). When a Figma design is authored, replace this section with `figma-extract` output.

1. **Trigger** — any focusable element outside the panel that flips `isVisible`. The trigger owns the accessible name of the panel and should reflect open/closed state via `aria-expanded` ([accessibility.md:35](./accessibility.md)).
2. **Panel container** — the floating side surface, sized between `minWidth` and `maxWidth` and starting at `defaultWidth` ([props.md:61-63](./props.md)). Token bindings are not available — [tokens.md:28-30](./tokens.md) flags a SOURCE_GAP (MCP returned no theme tokens for SlideOut).
3. **Resize handle** _(optional, only when `isResizable=true`)_ — drag affordance on the leading edge that fires `onResize(newWidth)` ([examples.md:41-44](./examples.md), [props.md:73](./props.md)). Must have a programmatic name and be keyboard-operable ([accessibility.md:51](./accessibility.md)).
4. **Children** — arbitrary React content rendered inside the panel ([props.md:57](./props.md), [examples.md:48-55](./examples.md)). The component does **not** ship a header, footer, or close button; if the panel needs any of those, the consuming application composes them inside `children`.
5. **No backdrop / scrim** — SlideOut does not dim the rest of the page (this is the distinguishing trait against Modal). If the underlying surface needs to be unreachable, see Pair 1.

---

## Behaviour

### Visibility is fully external

`isVisible` is the single source of truth; the component does not manage its own open/closed state ([props.md:58](./props.md), [examples.md:62](./examples.md)). The consuming application owns the toggle, the keyboard escape hatch, the outside-click handler, and the focus return — none of those ship with the component.

### Resize is opt-in and uncontrolled

When `isResizable=true`, the user can drag the panel between `minWidth` and `maxWidth`. The component reports each new width via `onResize(newWidth)` ([examples.md:41-44](./examples.md)). The width itself is not a controlled prop — the application can persist the value but cannot set it back through props beyond `defaultWidth`.

### Keyboard contract

From [accessibility.md:39-43](./accessibility.md):

| Key | Behaviour |
|---|---|
| `Tab` / `Shift+Tab` | Move focus through interactive elements inside the panel when visible |
| `Escape` | **Must be wired by the consuming application** via `isVisible` state — the component does not implement it |

Focus management — moving focus into the panel on open, returning it to the trigger on close — is explicitly the consuming application's responsibility ([accessibility.md:45](./accessibility.md)).

---

## When to use

- **Supplementary detail next to the main task** — record details, conversation transcripts, configuration that complements (not replaces) the current view
- **Inspectors / property panels** that the user opens, scans, and dismisses without leaving the page
- **Side-by-side editing** where the main canvas needs to remain visible and interactive
- **Long content the user dismisses on their own schedule** — help articles, audit logs, debug consoles

## When not to use

- **Blocking decisions** ("Are you sure you want to delete?") — use a Modal. SlideOut does not dim the page or trap focus by default and is too easy to ignore.
- **Persistent primary navigation** — use a Drawer or sidebar. SlideOut is intended to be opened with intent and dismissed; it is not a permanent layout region.
- **Single-line hints or tips** — use a Tooltip.
- **Multi-step workflows** that need their own URL or back-navigation — use a dedicated page or Modal route.
- **Mobile-first surfaces at very narrow viewports** — the panel reserves a substantial horizontal slice ([props.md:61-63](./props.md): `defaultWidth` / `minWidth` / `maxWidth`); on small screens a Bottom Sheet or full-screen view will fit content better.

---

## Do / Don't

### Pair 1 — Pick SlideOut for supplementary side content; pick Modal or Drawer for everything else

#### ✅ Do — Use SlideOut when the page behind it should stay visible and interactive

SlideOut renders no backdrop and does not trap focus, so the main view remains live. That is exactly right for *companion* content — an inspector, a help panel, a detail flyout — and exactly wrong for blocking decisions or permanent nav.

```tsx
{/* Right — inspector that opens beside the current record without blocking it */}
<>
  <Button onClick={() => setInspectorOpen(true)}>View details</Button>
  <SlideOut isVisible={inspectorOpen} isResizable>
    <RecordInspector recordId={selectedId} onClose={() => setInspectorOpen(false)} />
  </SlideOut>
</>
```

#### ❌ Don't — Use SlideOut for blocking confirmations or persistent navigation

A confirmation that needs an explicit choice belongs in a Modal — SlideOut has no backdrop and no built-in dismissal, so users can ignore it indefinitely. Persistent app navigation belongs in a Drawer — SlideOut is meant to be opened on intent and closed, not parked open as part of the layout.

```tsx
{/* Wrong — destructive confirmation in a panel users can ignore */}
<SlideOut isVisible={confirmDeleteOpen}>
  <h2>Delete account?</h2>
  <Button onClick={deleteAccount}>Delete</Button>
</SlideOut>

{/* Wrong — primary nav lives in a Drawer, not a SlideOut */}
<SlideOut isVisible>
  <PrimaryNavLinks />
</SlideOut>
```

**Source:** [props.md:55-65](./props.md) (no built-in scrim / focus-trap / close prop) · [accessibility.md:30-35](./accessibility.md) (role choice — see Pair 3).

---

### Pair 2 — Control `isVisible` from application state and reflect it on the trigger with `aria-expanded`

#### ✅ Do — Drive open/closed from external state and mirror it on the trigger

`isVisible` is a controlled prop ([props.md:58](./props.md), [examples.md:62](./examples.md)): the consuming application holds the boolean. The trigger that opens the panel should advertise the current state to assistive tech via `aria-expanded` ([accessibility.md:35](./accessibility.md)).

```tsx
const [isVisible, setIsVisible] = useState(false);

return (
  <>
    <Button
      aria-expanded={isVisible}
      aria-controls="details-panel"
      onClick={() => setIsVisible(true)}
    >
      Show details
    </Button>
    <SlideOut id="details-panel" isVisible={isVisible}>
      …
    </SlideOut>
  </>
);
```

#### ❌ Don't — Try to make SlideOut self-managing, or open it without a stateful trigger

There is no uncontrolled / `defaultIsVisible` mode. Hard-coding `isVisible={true}` (or always-on rendering) leaves the user with no obvious dismissal path, and a trigger with no `aria-expanded` lies to screen readers about the panel's state.

```tsx
{/* Wrong — panel is always open, with no way to close it */}
<SlideOut isVisible>
  <RecordInspector recordId={selectedId} />
</SlideOut>

{/* Wrong — trigger doesn't reflect state, so assistive tech can't tell it's open */}
<Button onClick={() => setIsVisible(true)}>Show details</Button>
<SlideOut isVisible={isVisible}>…</SlideOut>
```

**Source:** [props.md:58](./props.md) · [examples.md:62](./examples.md) · [accessibility.md:35](./accessibility.md).

---

### Pair 3 — Set `role` to match the panel's intent: `dialog` for interaction, `complementary` for information

#### ✅ Do — Pick the role from the content's purpose, and pair `dialog` with `aria-labelledby`

[accessibility.md:30-35](./accessibility.md) gives two valid roles. `role="dialog"` (with `aria-labelledby` or `aria-label`) is right when the panel exists to gather input or confirm an action; `role="complementary"` is right when the panel is supplementary reference content the user can leave open while continuing to work.

```tsx
{/* Interactive form-like content → dialog + accessible name */}
<SlideOut isVisible={isVisible}>
  <section role="dialog" aria-labelledby="contact-form-title">
    <h2 id="contact-form-title">Add contact</h2>
    <ContactForm onSubmit={save} onCancel={close} />
  </section>
</SlideOut>

{/* Informational helper → complementary */}
<SlideOut isVisible={isVisible}>
  <aside role="complementary" aria-label="Field reference">
    <FieldReference fieldId={focusedFieldId} />
  </aside>
</SlideOut>
```

#### ❌ Don't — Use `dialog` for passive reference content, or use `complementary` for a form that demands a decision

Mis-roling the panel tells assistive tech the wrong story: a `dialog` implies the user must interact before continuing, and `complementary` implies the content is optional reading. Either mismatch confuses screen-reader users about whether they need to engage.

```tsx
{/* Wrong — role="dialog" on a passive help panel forces dialog-flow expectations */}
<SlideOut isVisible={helpOpen}>
  <section role="dialog">
    <HelpArticle slug={topic} />
  </section>
</SlideOut>

{/* Wrong — role="complementary" on a form that must be submitted or cancelled */}
<SlideOut isVisible={formOpen}>
  <aside role="complementary">
    <DeleteAccountForm />
  </aside>
</SlideOut>
```

**Source:** [accessibility.md:30-35](./accessibility.md) · [accessibility.md:49-50](./accessibility.md) (trigger label clarity).

---

### Pair 4 — Wire `Escape`, outside click, and focus return yourself — the component doesn't ship them

#### ✅ Do — Implement the three dismissal paths in the consuming application

[accessibility.md:43](./accessibility.md) is explicit: `Escape` "Should close the panel (**must be implemented by the consuming application** via `isVisible` state)." Same for focus return on close ([accessibility.md:45](./accessibility.md)). Provide a keyboard handler, an outside-click handler, and a visible close affordance — and store the trigger so focus can return to it.

```tsx
const triggerRef = useRef<HTMLButtonElement>(null);
const panelRef = useRef<HTMLDivElement>(null);
const [isVisible, setIsVisible] = useState(false);

const close = useCallback(() => {
  setIsVisible(false);
  triggerRef.current?.focus(); // return focus to the trigger
}, []);

useEffect(() => {
  if (!isVisible) return;
  const onKey = (e: KeyboardEvent) => { if (e.key === 'Escape') close(); };
  const onClick = (e: MouseEvent) => {
    if (panelRef.current && !panelRef.current.contains(e.target as Node)) close();
  };
  // Move focus into the panel on open
  panelRef.current?.querySelector<HTMLElement>('[data-autofocus]')?.focus();
  document.addEventListener('keydown', onKey);
  document.addEventListener('mousedown', onClick);
  return () => {
    document.removeEventListener('keydown', onKey);
    document.removeEventListener('mousedown', onClick);
  };
}, [isVisible, close]);

return (
  <>
    <Button ref={triggerRef} onClick={() => setIsVisible(true)}>Open</Button>
    <SlideOut isVisible={isVisible}>
      <div ref={panelRef}>
        <CloseButton onClick={close} data-autofocus />
        …
      </div>
    </SlideOut>
  </>
);
```

#### ❌ Don't — Assume the component handles dismissal, or omit a visible close affordance

Leaving `Escape` and outside-click unhandled traps keyboard users with no way to close the panel. Skipping a visible close button leaves pointer users guessing. Failing to return focus to the trigger drops the user at the top of the document on close.

```tsx
{/* Wrong — Escape, outside click, and focus return all missing; close path is invisible */}
<>
  <Button onClick={() => setIsVisible(true)}>Open</Button>
  <SlideOut isVisible={isVisible}>
    <RecordInspector />
  </SlideOut>
</>
```

**Source:** [accessibility.md:39-43](./accessibility.md) · [accessibility.md:45](./accessibility.md) (focus management is the consumer's responsibility) · [accessibility.md:58](./accessibility.md) (WCAG 2.1.2 — no keyboard trap).

---

### Pair 5 — Toggle `aria-hidden` in lockstep with `isVisible` so the closed panel isn't announced

#### ✅ Do — Mirror `aria-hidden` on the panel when `isVisible` is false

The panel renders in the DOM regardless of visibility ([accessibility.md:49](./accessibility.md)). Without `aria-hidden`, screen readers will announce the hidden panel's contents and may navigate into it via the rotor.

```tsx
<SlideOut
  isVisible={isVisible}
  aria-hidden={!isVisible || undefined}
>
  <section role="dialog" aria-labelledby="filters-title">
    <h2 id="filters-title">Filters</h2>
    …
  </section>
</SlideOut>
```

If the SlideOut surface itself does not forward `aria-hidden` to its rendered root, wrap the content in a `<div aria-hidden={!isVisible || undefined}>` inside `children` instead.

#### ❌ Don't — Render the panel without an `aria-hidden` strategy

The panel's children stay reachable to assistive tech and to `Tab` order even when the panel is collapsed off-screen, which both surfaces phantom content and creates a "where did my focus go?" moment for keyboard users.

```tsx
{/* Wrong — closed panel still announced and tab-reachable */}
<SlideOut isVisible={isVisible}>
  <RecordInspector recordId={selectedId} />
</SlideOut>
```

**Source:** [accessibility.md:34](./accessibility.md) (`aria-hidden="true"` when `isVisible=false`) · [accessibility.md:49](./accessibility.md) (panel content rendered regardless of `isVisible`).

---

### Pair 6 — Turn on `isResizable` only when the panel hosts width-sensitive content; otherwise lock the width

#### ✅ Do — Enable resize for tabular, code, or canvas-shaped content where width is the user's lever

[props.md:59](./props.md) gates resizing behind `isResizable`, and [examples.md:41-44](./examples.md) shows the canonical `onResize(newWidth)` callback. Resize earns its complexity when the user genuinely needs to control the panel's width — wide tables, code diffs, side-by-side previews — and is otherwise visual noise.

```tsx
<SlideOut
  isVisible={isVisible}
  isResizable
  defaultWidth={520}
  minWidth={360}
  maxWidth={960}
  onResize={(width) => persistPanelWidth(width)}
>
  <DiffView leftRef={baseRef} rightRef={headRef} />
</SlideOut>
```

When you ship resize, set `minWidth` and `maxWidth` so the panel cannot drag into a state that breaks the underlying layout, persist the new width on `onResize` so it survives reload, and make sure the resize handle is keyboard-operable and has an accessible label ([accessibility.md:51](./accessibility.md)).

#### ❌ Don't — Ship resize on a panel where the width isn't a user concern, or ship it without min/max

A resize handle on a short-form panel ("Add comment") adds an affordance no user will reach for and a drag target keyboard users have to step past. Worse, omitting `minWidth`/`maxWidth` lets users drag the panel into states that obscure the main view or collapse the panel to unusable widths.

```tsx
{/* Wrong — short form, no width sensitivity, unbounded resize */}
<SlideOut isVisible={isVisible} isResizable>
  <CommentForm onSubmit={save} onCancel={close} />
</SlideOut>
```

**Source:** [props.md:59](./props.md) (`isResizable`) · [props.md:61-63](./props.md) (`defaultWidth` / `minWidth` / `maxWidth`) · [props.md:73](./props.md) (`onResize` — observed but not in the props registry; treat with caution per [SlideOut-audit.md](./SlideOut-audit.md) GAP-005) · [examples.md:41-44](./examples.md) · [accessibility.md:51](./accessibility.md).

---

### Pair 7 — Scope content to a single concern and scroll inside the panel; if it needs more, go to a page

#### ✅ Do — Keep the panel focused on one task and let internal scroll handle long content

A SlideOut works because it's narrow, dismissible, and parallel to the main task. Put one job in it (a record's details, one form, one document) and let the panel body scroll vertically when content overflows.

```tsx
<SlideOut isVisible={isVisible}>
  <section role="dialog" aria-labelledby="record-title">
    <PanelHeader id="record-title" title="Order #4821" onClose={close} />
    <div style={{ overflowY: 'auto', flex: 1 }}>
      <OrderSummary order={order} />
      <OrderTimeline events={order.events} />
    </div>
  </section>
</SlideOut>
```

#### ❌ Don't — Nest a multi-step workflow, scroll the page behind the panel, or stack SlideOuts

A SlideOut hosting a four-step wizard breaks back-navigation and bookmarking — that flow wants a dedicated page or a Modal route. Letting the page behind the panel scroll loses the user's place. Opening a second SlideOut over the first compounds dismissal and focus-management work the component does not help with — see Pair 4.

```tsx
{/* Wrong — multi-step wizard in a side panel; needs a real route */}
<SlideOut isVisible={wizardOpen}>
  <OnboardingWizard steps={ALL_STEPS} />
</SlideOut>

{/* Wrong — nested SlideOuts; dismissal and focus return become ambiguous */}
<SlideOut isVisible={outerOpen}>
  <RecordInspector />
  <SlideOut isVisible={innerOpen}>
    <EditField fieldId={focusedFieldId} />
  </SlideOut>
</SlideOut>
```

**Source:** "When not to use" above · [accessibility.md:45](./accessibility.md) (focus management is the consumer's responsibility — nesting compounds it).

---

## Gaps

| Item | Description |
|------|-------------|
| Pairs are editorial | No Figma design exists for SlideOut ([SlideOut-audit.md](./SlideOut-audit.md) GAP-001 / GAP-002). Pairs above were authored via `usage-advisor` Open mode, mirroring [PopoverMenu-usage.md](../PopoverMenu/PopoverMenu-usage.md). Replace this file with `figma-extract-usage` output if a `↳ SlideOut examples` page is ever authored. |
| Audit verdict remains `PARTIAL` | Producing this editorial doc does **not** clear GAP-001 (no `SlideOut-figma.md`) or GAP-002 (no usage page from Figma). Those gaps remain blocked on upstream design work. |
| No anatomy / token references | [tokens.md](./tokens.md) is empty (MCP returned 0 tokens — SOURCE_GAP), and no `SlideOut-figma.md` exists. The Anatomy section above is inferred from `props.md` and `examples.md` and should be replaced when a Figma source lands. |
| All accessibility guidance inferred | [accessibility.md:26](./accessibility.md) declares the entire a11y file is inferred from component nature and WCAG — no explicit a11y data was returned by the MCP. Pairs 3 / 4 / 5 lean on this inferred guidance. |
| `onResize` undocumented in props registry | [props.md:67-75](./props.md) notes `onResize` is observed in the Storybook example but absent from the props registry. Pair 6's signature should be reconfirmed against the component source. |
| Header / footer / close affordances are not component-provided | Unlike PopoverMenu's `header` / `footer` slots, SlideOut exposes no equivalent props ([props.md:55-65](./props.md)). Pair 4 and Pair 7 compose these inside `children`, which is the current correct pattern but should be reconfirmed once a Figma design exists. |

---

_Source: Editorial draft via usage-advisor · Drafted 2026-05-15_
