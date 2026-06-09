---
component: Tabs
package: "@8x8/oxygen-tabs"
category: layout_overlay
role: usage
role_description: "Usage guidelines — editorial, drafted via usage-advisor from extracted MCP artifacts; Figma examples page exists at node 85697:271849 but no Do/Don't card frames are authored yet"
pipeline_stage: editorial
pipeline_note: "Pairs are editorial. The Figma 'Tabs — Examples' page (node 85697:271849) exists but contains no `✅ Do —` / `❌ Don't —` card frames. Replace this file wholesale with figma-extract-usage output once cards are authored. Tabs-audit.md GAP-003 is now resolved-editorial (file present; SOURCE_GAP for Figma cards remains)."
source_type: editorial
audit_verdict: null
siblings:
  - "[[Tabs/props]]"
  - "[[Tabs/examples]]"
  - "[[Tabs/tokens]]"
  - "[[Tabs/accessibility]]"
  - "[[Tabs/Tabs-figma]]"
  - "[[Tabs/Tabs-pui]]"
  - "[[Tabs/Tabs-audit]]"
  - "[[Tabs/Tabs-spec]]"
tags:
  - oxygen
  - component/Tabs
  - role/usage
  - stage/editorial
  - category/layout_overlay
---
<!-- SOURCE: editorial — drafted via usage-advisor (Open mode) from props.md + examples.md + accessibility.md + Tabs-figma.md + Tabs-audit.md + Tabs-spec.md -->
<!-- FIGMA EXAMPLES PAGE: exists (node 85697:271849) but has no `✅ Do — …` / `❌ Don't — …` card frames yet -->
<!-- GROUNDING: full — every sibling file is present in component-lib/Tabs/ -->
<!-- DRAFTED: 2026-05-15 -->
<!-- MODE: open -->
<!-- PAIRS: 7 -->
<!-- STATUS: editorial draft — replace with figma-extract-usage output once Do/Don't card frames are authored on the Figma examples page -->

# Tabs — Usage Guidelines

> **See also:** [props.md](./props.md) · [examples.md](./examples.md) · [tokens.md](./tokens.md) ·
> [accessibility.md](./accessibility.md) · [Tabs-figma.md](./Tabs-figma.md) · [Tabs-audit.md](./Tabs-audit.md) · [Tabs-spec.md](./Tabs-spec.md)

> **Editorial guidance — Figma Do/Don't cards have not been authored yet.** This file was drafted via `usage-advisor` Open mode from the extracted MCP artifacts (see header comments). It does **not** fully resolve [Tabs-audit.md](./Tabs-audit.md) **GAP-003** — that gap remains a SOURCE_GAP for the upstream Figma cards on page [`85697:271849`](https://www.figma.com/design/5YihJ5WuDvnvrlrRMC4sBp/UI-components?node-id=85697-271849). When designers add `✅ Do — …` / `❌ Don't — …` card frames there, run `figma-extract-usage Tabs` and replace this file wholesale. The structural precedent is [SlideOut-usage.md](../SlideOut/SlideOut-usage.md).

`Tabs` switches the user between **sibling content sections that live within the same page** ([examples.md:33](./examples.md), [Tabs-spec.md:38](./Tabs-spec.md)). The active tab is always preserved when the container narrows: trailing tabs collapse into a disclosure popover from right to left, and once only one tab fits, it transforms into a popover trigger ([examples.md:119-146](./examples.md), [Tabs-spec.md:291-311](./Tabs-spec.md)). The component is **controlled** — the consuming application owns `isActive` and the click handler ([props.md:87](./props.md), [examples.md:42-71](./examples.md)).

---

## Anatomy

> Anatomy below is grounded in [Tabs-figma.md](./Tabs-figma.md) (component set `85651:78740`, disclosure `85651:78793`, popover atom `86115:3520`) and [props.md](./props.md). Replace with `figma-extract` output if the design is restructured.

1. **`<Tabs>` container** — auto-layout row that holds one or more `<Tab>` children and (when needed) renders the disclosure button at the trailing edge ([props.md:66-74](./props.md), [Tabs-figma.md:60-67](./Tabs-figma.md)).
2. **`<Tab>` item** — interactive cell, ~68×52px at default density with 16px padding, with a 1px bottom border in rest/hover/disabled states and a **2px** `actions/action01` underline + `bodyBold01` label when selected ([Tabs-figma.md:50-67](./Tabs-figma.md), [Tabs-figma.md:157-180](./Tabs-figma.md)).
3. **Optional icon slot** — decorative cue paired with the label ([Tabs-figma.md:77-80](./Tabs-figma.md), [examples.md:108-110](./examples.md)).
4. **Optional badge** — small turquoise indicator for unread/notification counts ([Tabs-figma.md:79](./Tabs-figma.md), [examples.md:111-112](./examples.md)).
5. **`tabsDisclosure` overflow button** — 52×52 chevron trigger that appears when not all tabs fit; opens the `.Tabs Popover` to expose hidden tabs ([Tabs-figma.md:85-108](./Tabs-figma.md), [examples.md:119-146](./examples.md)).
6. **Last-visible-tab popover (`hasDropdown`)** — when the container collapses to a single tab, that tab itself becomes the popover trigger and the separate disclosure button is removed ([examples.md:114-116](./examples.md), [examples.md:131-133](./examples.md)).

---

## Behaviour

### Active state is controlled externally

`<Tab isActive={…}>` is a presentational flag — the component does not track its own selection. The consuming application stores the active value and sets `isActive` on whichever child matches ([props.md:87](./props.md), [examples.md:42-71](./examples.md)).

### Progressive overflow protects the active tab, not popular tabs

As the container narrows, tabs collapse right-to-left into the disclosure popover. The **currently active tab is always swapped into the visible row**; the system has no notion of which other tabs are used most often ([examples.md:134-136](./examples.md), [Tabs-spec.md:302](./Tabs-spec.md)).

### Keyboard contract today is `Tab` / `Shift+Tab` / `Enter` / `Space` / `Escape`

The current accessibility documentation does **not** confirm Left/Right arrow navigation inside the tablist ([accessibility.md:60-72](./accessibility.md), [Tabs-audit.md GAP-009](./Tabs-audit.md)). Until that is confirmed in the rendered DOM, treat arrow-key roving focus as something you must add yourself if you assert `role="tablist"` on the container.

### Selected state has two indicators, not one

The selected tab is differentiated by both a 2px blue underline (`actions/action01`) **and** a bold label (`typography/bodyBold01`) — two non-color signals, which satisfies WCAG 1.4.1 ([Tabs-figma.md:157-180](./Tabs-figma.md), [Tabs-audit.md GAP-010](./Tabs-audit.md)). Don't override the bold weight in custom styling.

---

## When to use

- Switching between **2–7 peer sections of the same record or screen** — settings panes, profile/activity/files for a user, summary/details/history for a ticket.
- The sections are **siblings of equal weight** and the user expects to flip between them without leaving the page.
- All sections share enough surrounding chrome (header, primary action, breadcrumbs) that a route change would feel heavy.

## When not to use

- **Primary site or app navigation.** Tabs explicitly target "content within a page" ([examples.md:33](./examples.md), [Tabs-spec.md:38](./Tabs-spec.md)). For moving between distinct destinations or routes, use the application shell's nav (see rejected PUI candidate `@8x8/pui-use-navigation` in [Tabs-pui.md](./Tabs-pui.md)).
- **A linear workflow** (step 1 → step 2 → step 3). Use a Stepper or wizard; Tabs lets the user skip steps in any order, which is the wrong affordance for required progression.
- **A mutually-exclusive choice that commits a value** (think "Monthly / Yearly" pricing toggle, or a filter). Use a SegmentedControl or Radio group — `<Tab>`'s `onClick` is fire-and-forget on a content switch, not a value selector for a form.
- **More than ~7 sections.** The progressive overflow keeps you running, but routinely pushing tabs into the disclosure popover signals that the structure should be flatter (split the page) or deeper (Accordion / nested nav).
- **Containers that are reliably narrow.** If you're routinely in the "single-tab `hasDropdown`" stage ([examples.md:131-133](./examples.md)), you've reduced Tabs to a Select with extra steps — use a Select.

---

## Do / Don't

### Pair 1 — Use Tabs for sibling content within one page; don't use Tabs as primary navigation or as a wizard

#### ✅ Do — Switch between peer views of the same record on the same page

```tsx
{/* Right — three peer views of one user record, no route change */}
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
{/* Wrong — these are app-level destinations, each with their own URL and chrome.
    This belongs in the application shell nav, not in Tabs. */}
<Tabs>
  <Tab value="dashboard" isActive={pathname === '/dashboard'} onClick={() => router.push('/dashboard')}>Dashboard</Tab>
  <Tab value="contacts"  isActive={pathname === '/contacts'}  onClick={() => router.push('/contacts')}>Contacts</Tab>
  <Tab value="reports"   isActive={pathname === '/reports'}   onClick={() => router.push('/reports')}>Reports</Tab>
  <Tab value="settings"  isActive={pathname === '/settings'}  onClick={() => router.push('/settings')}>Settings</Tab>
</Tabs>

{/* Wrong — a linear wizard belongs in a Stepper. Tabs lets the user skip
    to step 3 before completing step 1, which breaks the flow's contract. */}
<Tabs>
  <Tab value="details"  isActive={step === 'details'}>1. Details</Tab>
  <Tab value="billing"  isActive={step === 'billing'}>2. Billing</Tab>
  <Tab value="review"   isActive={step === 'review'}>3. Review</Tab>
</Tabs>
```

**Why it matters:** the Oxygen Tabs surface, the documented intent ([examples.md:33](./examples.md), [Tabs-spec.md:38](./Tabs-spec.md)), and the rejection of `@8x8/pui-use-navigation` in [Tabs-pui.md](./Tabs-pui.md) all converge on the same point — Tabs is in-page section switching, not app navigation.

**Source:** [examples.md:33](./examples.md) · [Tabs-spec.md:38](./Tabs-spec.md) · [Tabs-pui.md](./Tabs-pui.md).

---

### Pair 2 — Hold active state in a single source of truth and give every Tab a unique `value`

#### ✅ Do — Drive `isActive` from one state variable and mirror it back via `onClick(ev, value)`

`isActive` is presentational ([props.md:87](./props.md)); `value` is what gets passed to your handler ([props.md:86](./props.md), [props.md:90](./props.md)). One state value, one `setActive`, one comparison per Tab.

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
{/* Wrong — three independent booleans drift out of sync the moment two are true at once */}
const [overview, setOverview] = React.useState(true);
const [metrics, setMetrics]   = React.useState(false);
const [audit, setAudit]       = React.useState(false);

<Tabs>
  <Tab isActive={overview} onClick={() => { setOverview(true);  setMetrics(false); setAudit(false); }}>Overview</Tab>
  <Tab isActive={metrics}  onClick={() => { setOverview(false); setMetrics(true);  setAudit(false); }}>Metrics</Tab>
  <Tab isActive={audit}    onClick={() => { setOverview(false); setMetrics(false); setAudit(true);  }}>Audit</Tab>
</Tabs>

{/* Wrong — no `value`, so onClick can't tell which tab fired */}
<Tab isActive={active === 'overview'} onClick={() => setActive('overview')}>Overview</Tab>

{/* Wrong — duplicate `value` makes the active state non-deterministic */}
<Tab value="view" isActive={active === 'view'} onClick={(_, v) => setActive(v)}>Overview</Tab>
<Tab value="view" isActive={active === 'view'} onClick={(_, v) => setActive(v)}>Metrics</Tab>
```

**Why it matters:** the component is controlled but does not validate uniqueness — drift, duplication, and "no current selection" states are all silent bugs the API permits.

**Source:** [props.md:86-90](./props.md) · [examples.md:42-71](./examples.md).

---

### Pair 3 — Keep the tab count manageable; let progressive overflow be the safety net, not the default state

#### ✅ Do — Aim for 2–7 visible tabs and pre-empt overflow with structure changes when you exceed it

The progressive-overflow behaviour ([examples.md:119-146](./examples.md)) is designed to *gracefully degrade* at narrow widths, not to absorb a long inventory of sections. If you can't fit your tabs at typical container widths, that's a structural signal — split the page, nest content, or use Accordion.

```tsx
{/* Right — five peer sections, all visible at typical widths.
    Overflow only triggers if the panel itself is resized very small. */}
<Tabs>
  <Tab value="overview"      isActive={active === 'overview'}>Overview</Tab>
  <Tab value="participants"  isActive={active === 'participants'}>Participants</Tab>
  <Tab value="recordings"    isActive={active === 'recordings'}>Recordings</Tab>
  <Tab value="transcripts"   isActive={active === 'transcripts'}>Transcripts</Tab>
  <Tab value="permissions"   isActive={active === 'permissions'}>Permissions</Tab>
</Tabs>
```

#### ❌ Don't — Ship twelve tabs and rely on the disclosure to "handle it"

```tsx
{/* Wrong — most users will see half of this row land in the overflow popover.
    The progressive overflow only guarantees the *active* tab stays visible,
    not the most-used ones. Split the page or use a side nav instead. */}
<Tabs>
  <Tab value="overview">Overview</Tab>
  <Tab value="participants">Participants</Tab>
  <Tab value="recordings">Recordings</Tab>
  <Tab value="transcripts">Transcripts</Tab>
  <Tab value="permissions">Permissions</Tab>
  <Tab value="integrations">Integrations</Tab>
  <Tab value="webhooks">Webhooks</Tab>
  <Tab value="audit">Audit log</Tab>
  <Tab value="billing">Billing</Tab>
  <Tab value="security">Security</Tab>
  <Tab value="api-keys">API keys</Tab>
  <Tab value="danger">Danger zone</Tab>
</Tabs>
```

**Why it matters:** the overflow algorithm prioritises the *current* selection, not the *important* ones ([Tabs-spec.md:302](./Tabs-spec.md)). A frequently-used "Permissions" tab will routinely sit in the popover behind a chevron whenever it isn't the user's current view.

**Source:** [examples.md:119-146](./examples.md) · [Tabs-spec.md:291-311](./Tabs-spec.md).

---

### Pair 4 — Use `icon` to reinforce meaning and `badge` for notification counts; never use color or icon alone as the only signal

#### ✅ Do — Pair icon/badge with a clear text label and rely on Oxygen's two-indicator selected state

Per Figma guidance, `icon` is a "decorative element… to reinforce the meaning of the tab" and `badge` is "when the content of a tab includes a list of notifications" ([examples.md:108-112](./examples.md)). The selected state itself already carries two indicators (2px underline + bold weight, see [Tabs-figma.md:157-180](./Tabs-figma.md)) — keep both.

```tsx
{/* Right — icon reinforces the section's identity; badge counts unread items;
    the text label stays the primary signal */}
<Tabs>
  <Tab value="inbox" isActive={active === 'inbox'} onClick={(_, v) => setActive(v)}>
    <MailIcon /> Inbox <Badge count={3} />
  </Tab>
  <Tab value="sent"     isActive={active === 'sent'}     onClick={(_, v) => setActive(v)}>Sent</Tab>
  <Tab value="archived" isActive={active === 'archived'} onClick={(_, v) => setActive(v)}>Archived</Tab>
</Tabs>
```

#### ❌ Don't — Drop the label, decorate every tab with an icon for "balance," or override the bold-weight selected state

```tsx
{/* Wrong — icon-only tabs strip the accessible name and force users to memorise glyphs.
    Compact view is the place where labels collapse, not a default for desktop widths
    (see examples.md:108-110 — icon-only is for "compact view when the label is hidden
    due to space constraints", not a default). */}
<Tabs>
  <Tab value="inbox"><MailIcon /></Tab>
  <Tab value="sent"><SendIcon /></Tab>
  <Tab value="archived"><ArchiveIcon /></Tab>
</Tabs>

{/* Wrong — a "New" badge that never counts anything is decoration, not notification.
    Use a different affordance (Tag, label suffix) for marketing tags. */}
<Tab value="ai-summary" isActive={active === 'ai-summary'}>AI summary <Badge label="New" /></Tab>

{/* Wrong — overriding the bold selected-state weight back to regular weight
    leaves the underline as the *only* differentiator and risks failing WCAG 1.4.1
    (Tabs-audit.md GAP-010, Tabs-figma.md Color & token bindings). */}
<Tabs className="my-tabs--no-bold-selected">…</Tabs>
```

**Why it matters:** the component already passes WCAG 1.4.1 because it ships two non-color indicators ([Tabs-audit.md GAP-010](./Tabs-audit.md), [Tabs-figma.md:157-180](./Tabs-figma.md)). Decorative-only icons and label-stripping break both the documented intent and the a11y guarantee.

**Source:** [examples.md:108-112](./examples.md) · [Tabs-figma.md:157-180](./Tabs-figma.md) · [Tabs-audit.md GAP-010](./Tabs-audit.md).

---

### Pair 5 — Decide `isStretched` at the row level: apply it to every tab or to none

#### ✅ Do — Stretch every tab in a small, fixed-count row that should claim the full container width

`isStretched` makes a `<Tab>` fill available space inside `<Tabs>` ([props.md:89](./props.md), [examples.md:91-100](./examples.md)). It's a per-tab boolean, but the *layout intent* is row-wide — equal-width columns.

```tsx
{/* Right — two peer modes, equal width, full container */}
<Tabs>
  <Tab value="grid"  isActive={view === 'grid'}  isStretched onClick={(_, v) => setView(v)}>Grid view</Tab>
  <Tab value="table" isActive={view === 'table'} isStretched onClick={(_, v) => setView(v)}>Table view</Tab>
</Tabs>
```

#### ❌ Don't — Mix stretched and natural-width tabs in the same row

```tsx
{/* Wrong — the stretched tab claims all leftover space while the others hug content,
    producing a lopsided row whose proportions shift with the container width */}
<Tabs>
  <Tab value="overview"   isActive={active === 'overview'}                  >Overview</Tab>
  <Tab value="details"    isActive={active === 'details'}    isStretched    >Details</Tab>
  <Tab value="references" isActive={active === 'references'}                >References</Tab>
</Tabs>
```

**Why it matters:** `isStretched` is implemented as flex-grow on a single child — mixing it with hug-content siblings produces inconsistent visual hierarchy and re-flows unpredictably between breakpoints.

**Source:** [props.md:89](./props.md) · [examples.md:91-100](./examples.md).

---

### Pair 6 — Use `onClick` to switch the displayed section; don't commit values, fire side effects, or navigate away

#### ✅ Do — Treat `onClick` as a pure setState of the active section

```tsx
{/* Right — selecting a tab only changes what's rendered; nothing is saved, sent, or routed */}
<Tabs>
  <Tab value="metrics" isActive={active === 'metrics'} onClick={(_, v) => setActive(v)}>Metrics</Tab>
  <Tab value="logs"    isActive={active === 'logs'}    onClick={(_, v) => setActive(v)}>Logs</Tab>
  <Tab value="traces"  isActive={active === 'traces'}  onClick={(_, v) => setActive(v)}>Traces</Tab>
</Tabs>
```

#### ❌ Don't — Fire mutations, open dialogs, or change the route inside the tab handler

```tsx
{/* Wrong — committing a destructive action on tab click; the user has no
    confirmation step and no way to undo the change by switching tabs back */}
<Tab value="delete" isActive={active === 'delete'} onClick={() => deleteAccount()}>Delete account</Tab>

{/* Wrong — opening a Modal on a content-switch component conflates two
    affordances; users expect tabs to *show* a section, not to launch a flow */}
<Tab value="invite" onClick={() => setInviteModalOpen(true)}>Invite teammate</Tab>

{/* Wrong — `router.push` on tab click makes the tab a navigation control;
    see Pair 1 — that belongs in the application shell nav */}
<Tab value="billing" onClick={() => router.push('/billing')}>Billing</Tab>
```

**Why it matters:** Tabs has no built-in cancellation, confirmation, or focus-restore for side-effects. Anything irreversible needs a dedicated trigger (Button → Modal, link → router) that carries its own semantics.

**Source:** [props.md:90](./props.md) · [examples.md:33](./examples.md) · Pair 1 above.

---

### Pair 7 — Layer the ARIA contract on the rendered output and add Left/Right arrow handling for the tablist

#### ✅ Do — Apply the recommended ARIA roles and wire roving focus with arrow keys

The accessibility doc lists these roles as **recommended** rather than **shipped** ([accessibility.md:97-110](./accessibility.md), [WARN-002 in Tabs-audit.md](./Tabs-audit.md)). The current keyboard contract documents `Tab` / `Shift+Tab` / `Enter` / `Space` / `Escape` but **does not confirm Left/Right arrow nav** ([accessibility.md:60-72](./accessibility.md), [Tabs-audit.md GAP-009](./Tabs-audit.md)) — so if you assert `role="tablist"`, you must implement the arrow-key roving focus the WAI-ARIA tablist pattern requires.

```tsx
{/* Right — explicit ARIA contract, paired with arrow-key roving focus and aria-controls */}
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
    {/* …other tabs follow the same shape… */}
  </Tabs>
</div>

<section role="tabpanel" id="panel-profile" aria-labelledby="tab-profile" hidden={active !== 'profile'}>
  <ProfilePane />
</section>
```

#### ❌ Don't — Assert `role="tablist"` without implementing the keyboard contract that role requires

```tsx
{/* Wrong — declaring role="tablist" but leaving only Tab/Shift+Tab navigation
    silently breaks the WAI-ARIA tablist contract; screen-reader users will
    expect Left/Right arrow keys to roam between tabs and they won't work */}
<div role="tablist">
  <Tabs>
    <Tab role="tab" aria-selected={active === 'profile'} value="profile">Profile</Tab>
    <Tab role="tab" aria-selected={active === 'activity'} value="activity">Activity</Tab>
  </Tabs>
</div>

{/* Wrong — omitting aria-selected entirely leaves screen readers without a way
    to communicate which section is current */}
<Tab value="profile" isActive={active === 'profile'}>Profile</Tab>

{/* Wrong — when a tab label truncates in narrow widths, dropping the full label
    from aria-label / tooltip text strips the accessible name */}
<Tab value="long-section-name" isActive={true}>{label.slice(0, 8) + '…'}</Tab>
```

**Why it matters:** [accessibility.md](./accessibility.md) makes the ARIA roles "recommended enhancements (not yet in OX baseline)" — they're your responsibility to wire on, and the partial implementation (role without keys) is worse than no role at all because it lies to assistive tech. Truncated labels must keep their full accessible name ([accessibility.md:117](./accessibility.md)).

**Source:** [accessibility.md:60-72](./accessibility.md) · [accessibility.md:88-110](./accessibility.md) · [accessibility.md:117](./accessibility.md) · [Tabs-audit.md GAP-009](./Tabs-audit.md) · [Tabs-audit.md WARN-002](./Tabs-audit.md).

---

## Gaps & open questions

- **GAP-003 partial resolution** — this file now satisfies the "Tabs-usage.md present" half of [Tabs-audit.md GAP-003](./Tabs-audit.md). The other half — Figma `✅ Do —` / `❌ Don't —` card frames on page `85697:271849` — remains a SOURCE_GAP. When those cards are authored, run `figma-extract-usage Tabs` and replace this file wholesale.
- **GAP-009 (arrow-key nav)** — Pair 7 is written defensively because the OX implementation has not been confirmed to ship Left/Right arrow navigation inside the tablist. If a future verification confirms arrow-key support, soften the "you must implement it" language to "the component handles it."
- **WARN-002 (inferred ARIA roles)** — Pair 7's `role="tab"` / `aria-selected` / `aria-controls` assumes the Oxygen `<Tab>` either renders these natively or accepts them as forwarded props. Verify against the rendered DOM before relying on the snippet as-is.

_Drafted via `usage-advisor` Open mode · 2026-05-15_
