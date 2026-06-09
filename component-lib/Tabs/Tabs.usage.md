---
parent: "[[Tabs]]"
section: usage
pipeline_stage: doc_rewrite
tags:
  - oxygen
  - component/Tabs
  - role/spoke
  - section/usage
---

<!-- STUB:GAP-003 source="Author Do/Don't card frames on Figma examples page 85697:271849, then run figma-extract-usage Tabs to replace this editorial draft wholesale." -->
<!-- source: editorial — drafted via usage-advisor (Open mode) from props.md + examples.md + accessibility.md + Tabs-figma.md. Replace wholesale with figma-extract-usage output once Figma Do/Don't cards are authored on page 85697:271849. -->

## Usage Guidelines

`Tabs` switches the user between **sibling content sections that live within the same page**. The active tab is always preserved when the container narrows: trailing tabs collapse into a disclosure popover from right to left, and once only one tab fits, it transforms into a popover trigger. The component is **controlled** — the consuming application owns `isActive` and the click handler.

---

## Anatomy

1. **`<Tabs>` container** — auto-layout row holding one or more `<Tab>` children; renders the disclosure button at the trailing edge when overflow occurs.
2. **`<Tab>` item** — interactive cell, ~68×52px at default density with 16px padding; 1px bottom border at rest/hover/disabled, **2px** `actions/action01` underline + `bodyBold01` label when selected.
3. **Optional icon slot** — decorative cue paired with the label (use to reinforce section meaning, not for branding decoration).
4. **Optional badge** — small turquoise indicator for unread/notification counts.
5. **`tabsDisclosure` overflow button** — 52×52 chevron trigger; appears when not all tabs fit; opens `.Tabs Popover` to expose hidden tabs.
6. **Last-visible-tab popover (`hasDropdown`)** — when the container collapses to a single tab, that tab becomes the popover trigger and the separate disclosure button is removed.

---

## Behaviour

### Active state is controlled externally

`<Tab isActive={…}>` is a presentational flag — the component does not track its own selection. The consuming application stores the active value and sets `isActive` on whichever child matches.

### Progressive overflow protects the active tab

As the container narrows, tabs collapse right-to-left into the disclosure popover. The **currently active tab is always swapped into the visible row**; the system has no notion of which other tabs are used most often.

### Keyboard contract

The current keyboard contract is `Tab` / `Shift+Tab` / `Enter` / `Space` / `Escape`. Arrow-key navigation inside the tablist is documented as the WAI-ARIA tablist pattern but **has not been confirmed in the OX implementation** — see GAP-009 in [[Tabs-audit]] and Pair 7 below.

### Selected state has two indicators

The selected tab is differentiated by both a 2px blue underline (`actions/action01`) **and** a bold label (`typography/bodyBold01`) — two non-color signals, satisfying WCAG 1.4.1. Don't override the bold weight in custom styling.

---

## When to use

- Switching between **2–7 peer sections of the same record or screen** — settings panes, profile/activity/files for a user, summary/details/history for a ticket.
- The sections are **siblings of equal weight** and the user expects to flip between them without leaving the page.
- All sections share enough surrounding chrome (header, primary action, breadcrumbs) that a route change would feel heavy.

## When not to use

- **Primary site or app navigation.** Tabs explicitly target "content within a page". For moving between distinct destinations or routes, use the application shell's nav.
- **A linear workflow** (step 1 → step 2 → step 3). Use a Stepper or wizard; Tabs lets the user skip steps in any order.
- **A mutually-exclusive choice that commits a value** (think "Monthly / Yearly" pricing toggle, or a filter). Use a [[SegmentedControl]] or [[Radio]] group.
- **More than ~7 sections.** If you're routinely pushing tabs into the disclosure popover, the structure should be flatter (split the page) or deeper ([[Accordion]] / nested nav).
- **Containers that are reliably narrow.** If you're routinely in the "single-tab `hasDropdown`" stage, use a [[Select]].

---

## Do / Don't

### Pair 1 — Use Tabs for sibling content within one page; don't use Tabs as primary navigation or as a wizard

#### ✅ Do — Switch between peer views of the same record on the same page

```tsx
function UserRecord({ userId }: { userId: string }) {
  const [active, setActive] = React.useState<'profile' | 'activity' | 'files'>('profile');

  return (
    <>
      <Tabs>
        <Tab value="profile"  isActive={active === 'profile'}  onClick={(_, v) => setActive(v)}>Profile</Tab>
        <Tab value="activity" isActive={active === 'activity'} onClick={(_, v) => setActive(v)}>Activity</Tab>
        <Tab value="files"    isActive={active === 'files'}    onClick={(_, v) => setActive(v)}>Files</Tab>
      </Tabs>

      {active === 'profile'  && <ProfilePane userId={userId} />}
      {active === 'activity' && <ActivityPane userId={userId} />}
      {active === 'files'    && <FilesPane userId={userId} />}
    </>
  );
}
```

#### ❌ Don't — Use Tabs to navigate between app destinations or to gate a step-by-step flow

```tsx
{/* Wrong — app-level destinations with their own URLs belong in the application shell nav */}
<Tabs>
  <Tab value="dashboard" isActive={pathname === '/dashboard'} onClick={() => router.push('/dashboard')}>Dashboard</Tab>
  <Tab value="contacts"  isActive={pathname === '/contacts'}  onClick={() => router.push('/contacts')}>Contacts</Tab>
</Tabs>

{/* Wrong — a linear wizard belongs in a Stepper; Tabs lets users skip steps */}
<Tabs>
  <Tab value="details" isActive={step === 'details'}>1. Details</Tab>
  <Tab value="billing" isActive={step === 'billing'}>2. Billing</Tab>
  <Tab value="review"  isActive={step === 'review'}>3. Review</Tab>
</Tabs>
```

**Why it matters:** Tabs is in-page section switching, not app navigation. The rejection of `@8x8/pui-use-navigation` in [[Tabs.platform]] converges on this same point.

---

### Pair 2 — Hold active state in a single source of truth; give every Tab a unique `value`

#### ✅ Do — Drive `isActive` from one state variable; mirror it back via `onClick(ev, value)`

```tsx
const [active, setActive] = React.useState('overview');

<Tabs>
  <Tab value="overview"  isActive={active === 'overview'}  onClick={(_, v) => setActive(v)}>Overview</Tab>
  <Tab value="metrics"   isActive={active === 'metrics'}   onClick={(_, v) => setActive(v)}>Metrics</Tab>
  <Tab value="audit-log" isActive={active === 'audit-log'} onClick={(_, v) => setActive(v)}>Audit log</Tab>
</Tabs>
```

#### ❌ Don't — Run independent booleans, omit `value`, or reuse the same `value` on more than one Tab

```tsx
{/* Wrong — three independent booleans drift out of sync if two are ever true simultaneously */}
const [overview, setOverview] = React.useState(true);
const [metrics, setMetrics]   = React.useState(false);

<Tabs>
  <Tab isActive={overview} onClick={() => { setOverview(true); setMetrics(false); }}>Overview</Tab>
  <Tab isActive={metrics}  onClick={() => { setOverview(false); setMetrics(true); }}>Metrics</Tab>
</Tabs>

{/* Wrong — duplicate value makes the active state non-deterministic */}
<Tab value="view" isActive={active === 'view'}>Overview</Tab>
<Tab value="view" isActive={active === 'view'}>Metrics</Tab>
```

**Why it matters:** the component is controlled but does not validate uniqueness — drift, duplication, and "no current selection" states are all silent bugs the API permits.

---

### Pair 3 — Keep the tab count manageable; let progressive overflow be the safety net, not the default state

#### ✅ Do — Aim for 2–7 visible tabs; pre-empt overflow with structure changes when you exceed it

```tsx
{/* Right — five peer sections, all visible at typical widths */}
<Tabs>
  <Tab value="overview"     isActive={active === 'overview'}>Overview</Tab>
  <Tab value="participants" isActive={active === 'participants'}>Participants</Tab>
  <Tab value="recordings"   isActive={active === 'recordings'}>Recordings</Tab>
  <Tab value="transcripts"  isActive={active === 'transcripts'}>Transcripts</Tab>
  <Tab value="permissions"  isActive={active === 'permissions'}>Permissions</Tab>
</Tabs>
```

#### ❌ Don't — Ship twelve tabs and rely on the disclosure to "handle it"

```tsx
{/* Wrong — most users will routinely see half this row in the overflow popover.
    Progressive overflow only guarantees the *active* tab stays visible, not the most-used ones. */}
<Tabs>
  <Tab value="overview">Overview</Tab>
  <Tab value="participants">Participants</Tab>
  {/* …8 more tabs… */}
  <Tab value="danger">Danger zone</Tab>
</Tabs>
```

**Why it matters:** the overflow algorithm prioritises the *current* selection, not the *important* ones. A frequently-used tab will routinely hide behind the chevron whenever it isn't the user's current view.

---

### Pair 4 — Use `icon` to reinforce meaning and `badge` for notification counts; never use color or icon alone as the only signal

#### ✅ Do — Pair icon/badge with a clear text label; rely on Oxygen's two-indicator selected state

Per Figma guidance, `icon` is a "decorative element… to reinforce the meaning of the tab" and `badge` is "when the content of a tab includes a list of notifications".

```tsx
<Tabs>
  <Tab value="inbox" isActive={active === 'inbox'} onClick={(_, v) => setActive(v)}>
    <MailIcon /> Inbox <Badge count={3} />
  </Tab>
  <Tab value="sent"     isActive={active === 'sent'}     onClick={(_, v) => setActive(v)}>Sent</Tab>
  <Tab value="archived" isActive={active === 'archived'} onClick={(_, v) => setActive(v)}>Archived</Tab>
</Tabs>
```

#### ❌ Don't — Drop the label, decorate every tab with an icon "for balance," or override the bold-weight selected state

```tsx
{/* Wrong — icon-only tabs strip the accessible name and force users to memorise glyphs */}
<Tabs>
  <Tab value="inbox"><MailIcon /></Tab>
  <Tab value="sent"><SendIcon /></Tab>
</Tabs>

{/* Wrong — overriding the bold selected-state weight leaves the underline as the *only*
    differentiator, risking WCAG 1.4.1 failure */}
<Tabs className="my-tabs--no-bold-selected">…</Tabs>
```

**Why it matters:** the component ships with two non-color indicators for the selected state (underline + bold). Overriding the bold weight reduces it to one indicator.

---

### Pair 5 — Decide `isStretched` at the row level: apply it to every tab or to none

#### ✅ Do — Stretch every tab in a small, fixed-count row that should claim the full container width

```tsx
{/* Right — equal-width columns, full container */}
<Tabs>
  <Tab value="grid"  isActive={view === 'grid'}  isStretched onClick={(_, v) => setView(v)}>Grid view</Tab>
  <Tab value="table" isActive={view === 'table'} isStretched onClick={(_, v) => setView(v)}>Table view</Tab>
</Tabs>
```

#### ❌ Don't — Mix stretched and natural-width tabs in the same row

```tsx
{/* Wrong — the stretched tab claims all leftover space while the others hug content,
    producing a lopsided row that re-flows unpredictably */}
<Tabs>
  <Tab value="overview"   isActive={active === 'overview'}>Overview</Tab>
  <Tab value="details"    isActive={active === 'details'}  isStretched>Details</Tab>
  <Tab value="references" isActive={active === 'references'}>References</Tab>
</Tabs>
```

**Why it matters:** `isStretched` is implemented as flex-grow on a single child — mixing it with hug-content siblings produces inconsistent visual hierarchy.

---

### Pair 6 — Use `onClick` to switch the displayed section; don't commit values, fire side effects, or navigate away

#### ✅ Do — Treat `onClick` as a pure setState of the active section

```tsx
<Tabs>
  <Tab value="metrics" isActive={active === 'metrics'} onClick={(_, v) => setActive(v)}>Metrics</Tab>
  <Tab value="logs"    isActive={active === 'logs'}    onClick={(_, v) => setActive(v)}>Logs</Tab>
</Tabs>
```

#### ❌ Don't — Fire mutations, open dialogs, or change the route inside the tab handler

```tsx
{/* Wrong — committing a destructive action on tab click; no confirmation, no undo */}
<Tab value="delete" isActive={active === 'delete'} onClick={() => deleteAccount()}>Delete account</Tab>

{/* Wrong — opening a Modal on a content-switch component conflates two affordances */}
<Tab value="invite" onClick={() => setInviteModalOpen(true)}>Invite teammate</Tab>
```

**Why it matters:** Tabs has no built-in cancellation, confirmation, or focus-restore for side effects. Irreversible actions need a dedicated trigger that carries its own semantics.

---

### Pair 7 — Layer the ARIA contract on the rendered output and add Left/Right arrow handling for the tablist

#### ✅ Do — Apply the recommended ARIA roles and wire roving focus with arrow keys

The accessibility doc lists these roles as **recommended enhancements not yet in OX baseline** (WARN-002). The current keyboard contract does **not confirm Left/Right arrow nav** (GAP-009) — if you assert `role="tablist"`, you must implement the arrow-key roving focus the WAI-ARIA tablist pattern requires.

```tsx
<div role="tablist" aria-label="User record sections" onKeyDown={handleTablistArrows}>
  <Tabs>
    <Tab
      value="profile"
      isActive={active === 'profile'}
      onClick={(_, v) => setActive(v)}
      role="tab"
      aria-selected={active === 'profile'}
      aria-controls="panel-profile"
      id="tab-profile"
      tabIndex={active === 'profile' ? 0 : -1}
    >
      Profile
    </Tab>
  </Tabs>
</div>

<section role="tabpanel" id="panel-profile" aria-labelledby="tab-profile" hidden={active !== 'profile'}>
  <ProfilePane />
</section>
```

#### ❌ Don't — Assert `role="tablist"` without implementing the keyboard contract that role requires

```tsx
{/* Wrong — declaring role="tablist" but leaving only Tab/Shift+Tab navigation
    breaks the WAI-ARIA tablist contract; screen-reader users expect Left/Right arrow roaming */}
<div role="tablist">
  <Tabs>
    <Tab role="tab" aria-selected={active === 'profile'} value="profile">Profile</Tab>
  </Tabs>
</div>

{/* Wrong — when a tab label truncates in narrow widths, dropping the full label
    from aria-label / tooltip strips the accessible name */}
<Tab value="long-section-name" isActive={true}>{label.slice(0, 8) + '…'}</Tab>
```

**Why it matters:** a partial ARIA implementation (role without the matching keyboard behaviour) is worse than no role at all because it lies to assistive tech. Truncated labels must keep their full accessible name.

---

## Open items

- **GAP-003** — This file is an editorial draft. Replace wholesale with `figma-extract-usage Tabs` output once `✅ Do — …` / `❌ Don't — …` card frames are authored on Figma examples page `85697:271849`.
- **GAP-009** — Pair 7 is written defensively. If a future verification confirms OX ships Left/Right arrow navigation in the tablist, soften the "you must implement it" language to "the component handles it."
- **WARN-002** — Pair 7's `role="tab"` / `aria-selected` / `aria-controls` assumes `<Tab>` either renders these natively or accepts them as forwarded props. Verify against the rendered DOM.

_Drafted via `usage-advisor` Open mode · 2026-05-15 · Assembled into spoke 2026-06-09_
