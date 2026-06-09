---
parent: "[[SlideOut]]"
section: usage
pipeline_stage: editorial
tags:
  - oxygen
  - component/SlideOut
  - role/usage
---

<!-- STUB:GAP-002 source="This usage doc is editorial (usage-advisor Open mode, 2026-05-15). To convert to canonical source: clear GAP-001 (Figma design created), author a '↳ SlideOut examples' page with ✅ Do / ❌ Don't card frames, then run figma-extract-usage to overwrite source/SlideOut-usage.md." -->

> **Editorial guidance — no Figma design exists for SlideOut.** This spoke was produced from [source/SlideOut-usage.md](source/SlideOut-usage.md), which was drafted via `usage-advisor` Open mode from extracted MCP artifacts. It does not resolve GAP-001 (no `SlideOut-figma.md`) or GAP-002 (no Figma examples page). Replace this spoke with `figma-extract-usage` output once a `↳ SlideOut examples` Figma page with `✅ Do — …` / `❌ Don't — …` card frames is authored.

## When to use

- Supplementary detail next to the main task — record details, configuration, conversation transcripts that complement (not replace) the current view
- Inspectors / property panels that the user opens, scans, and dismisses without leaving the page
- Side-by-side editing where the main canvas must remain visible and interactive
- Long content the user dismisses on their own schedule — help articles, audit logs, debug consoles

## When not to use

- **Blocking decisions** — use a Modal. SlideOut has no backdrop and no built-in dismissal; it is too easy to ignore.
- **Persistent primary navigation** — use a Drawer or sidebar. SlideOut is opened on intent and dismissed; it is not a permanent layout region.
- **Single-line hints or tips** — use a Tooltip.
- **Multi-step workflows** that need their own URL or back-navigation — use a dedicated page or Modal route.
- **Mobile-first surfaces at very narrow viewports** — the panel reserves a substantial horizontal slice; on small screens a Bottom Sheet or full-screen view fits content better.

---

## Do / Don't

### Pair 1 — Pick SlideOut for supplementary side content; pick Modal or Drawer for everything else

#### ✅ Do — Use SlideOut when the page behind it should stay visible and interactive

SlideOut renders no backdrop and does not trap focus, so the main view remains live. That is exactly right for companion content — an inspector, a help panel, a detail flyout — and exactly wrong for blocking decisions or permanent navigation.

```tsx
<>
  <Button onClick={() => setInspectorOpen(true)}>View details</Button>
  <SlideOut isVisible={inspectorOpen} isResizable>
    <RecordInspector recordId={selectedId} onClose={() => setInspectorOpen(false)} />
  </SlideOut>
</>
```

#### ❌ Don't — Use SlideOut for blocking confirmations or persistent navigation

```tsx
{/* Wrong — destructive confirmation users can ignore */}
<SlideOut isVisible={confirmDeleteOpen}>
  <h2>Delete account?</h2>
  <Button onClick={deleteAccount}>Delete</Button>
</SlideOut>

{/* Wrong — primary nav lives in a Drawer */}
<SlideOut isVisible>
  <PrimaryNavLinks />
</SlideOut>
```

**Source:** source/props.md (no built-in scrim / focus-trap / close prop) · source/accessibility.md (role choice).

---

### Pair 2 — Control `isVisible` from application state and reflect it on the trigger with `aria-expanded`

#### ✅ Do — Drive open/closed from external state and mirror it on the trigger

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

#### ❌ Don't — Hard-code `isVisible={true}` or open without a stateful trigger

```tsx
{/* Wrong — always open, no dismissal path */}
<SlideOut isVisible>
  <RecordInspector recordId={selectedId} />
</SlideOut>
```

**Source:** source/props.md · source/examples.md · source/accessibility.md.

---

### Pair 3 — Set `role` to match the panel's intent: `dialog` for interaction, `complementary` for information

#### ✅ Do — Pick the role from the content's purpose; pair `dialog` with `aria-labelledby`

```tsx
{/* Interactive form → dialog + accessible name */}
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

#### ❌ Don't — Use `dialog` for passive reference content, or `complementary` for a form requiring a decision

**Source:** source/accessibility.md.

---

### Pair 4 — Wire `Escape`, outside click, and focus return yourself — the component doesn't ship them

#### ✅ Do — Implement all three dismissal paths in the consuming application

```tsx
const triggerRef = useRef<HTMLButtonElement>(null);
const panelRef = useRef<HTMLDivElement>(null);
const [isVisible, setIsVisible] = useState(false);

const close = useCallback(() => {
  setIsVisible(false);
  triggerRef.current?.focus();
}, []);

useEffect(() => {
  if (!isVisible) return;
  const onKey = (e: KeyboardEvent) => { if (e.key === 'Escape') close(); };
  const onClick = (e: MouseEvent) => {
    if (panelRef.current && !panelRef.current.contains(e.target as Node)) close();
  };
  panelRef.current?.querySelector<HTMLElement>('[data-autofocus]')?.focus();
  document.addEventListener('keydown', onKey);
  document.addEventListener('mousedown', onClick);
  return () => {
    document.removeEventListener('keydown', onKey);
    document.removeEventListener('mousedown', onClick);
  };
}, [isVisible, close]);
```

#### ❌ Don't — Assume the component handles dismissal, or omit a visible close affordance

**Source:** source/accessibility.md (Escape is consumer's responsibility; focus management is consumer's responsibility; WCAG 2.1.2 — no keyboard trap).

---

### Pair 5 — Toggle `aria-hidden` in lockstep with `isVisible` so the closed panel isn't announced

#### ✅ Do — Mirror `aria-hidden` on the panel when `isVisible` is false

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

If SlideOut does not forward `aria-hidden` to its root, wrap children in `<div aria-hidden={!isVisible || undefined}>` instead.

#### ❌ Don't — Render the panel without an `aria-hidden` strategy

**Source:** source/accessibility.md (`aria-hidden="true"` when `isVisible=false`; panel content stays in DOM regardless of visibility).

---

### Pair 6 — Enable `isResizable` only for width-sensitive content; set `minWidth`/`maxWidth` when you do

#### ✅ Do — Enable resize for tables, code diffs, or canvas content; constrain with min/max

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

#### ❌ Don't — Enable resize on a short-form panel or omit min/max constraints

```tsx
{/* Wrong — short form, no width sensitivity, unbounded */}
<SlideOut isVisible={isVisible} isResizable>
  <CommentForm onSubmit={save} onCancel={close} />
</SlideOut>
```

**Source:** source/props.md · source/examples.md · source/accessibility.md (resize handle must be keyboard-operable).

---

### Pair 7 — Scope content to a single concern and scroll inside the panel; if it needs more, go to a page

#### ✅ Do — Keep the panel focused on one task; let the panel body scroll vertically

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

```tsx
{/* Wrong — multi-step wizard belongs on a real route */}
<SlideOut isVisible={wizardOpen}>
  <OnboardingWizard steps={ALL_STEPS} />
</SlideOut>

{/* Wrong — nested SlideOuts; focus return becomes ambiguous */}
<SlideOut isVisible={outerOpen}>
  <RecordInspector />
  <SlideOut isVisible={innerOpen}>
    <EditField fieldId={focusedFieldId} />
  </SlideOut>
</SlideOut>
```

**Source:** When-not-to-use above · source/accessibility.md (focus management is consumer's responsibility — nesting compounds it).
