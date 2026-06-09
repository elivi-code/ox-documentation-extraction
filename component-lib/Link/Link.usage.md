---
component: Link
parent: "[[Link]]"
section: usage
pipeline_stage: draft
siblings:
  - "[[Link.props]]"
  - "[[Link.anatomy]]"
  - "[[Link.tokens]]"
  - "[[Link.accessibility]]"
  - "[[Link.platform]]"
  - "[[Link.composition]]"
tags:
  - oxygen
  - component/Link
  - role/spoke-usage
---

<!-- STUB:GAP-017 source="Request designer to create ✅ Do / ❌ Don't card frames in the Figma examples page (node 58394:123) following the standard template. Re-run figma-extract-usage once component instances are dropped into preview frames." -->

## When to use

- When the user needs to navigate to a different page within the application.
- When the user needs to navigate to a different application or external site.

## When not to use

- When an action changes the state of the page or application — use [[Button]] instead.

## Types

| Type | Description |
|------|-------------|
| **Standalone** | Separated from body content; uses `$body02` typography; available in Small (14px) and Large (16px) |
| **Inline** | Embedded within a sentence or paragraph; inherits the surrounding typography size |

## Sizing

- **Inline** — matches the surrounding text size; no explicit size control.
- **Standalone** — Small for 14px contexts, Large for 16px contexts. Match size to neighbouring body type.

## Do / Don't

### Pair 1 — Link vs Button

**✅ Do — Use Link to navigate; use Button to act**

If activating the affordance changes the URL or opens a new page/tab, use Link. If it submits, opens a modal, toggles a setting, or otherwise changes app state without navigating, use Button. The native HTML — `<a href>` vs `<button>` — is what screen readers and keyboard users rely on.

**❌ Don't — Use a Button to navigate**

A button styled or used for navigation announces as "button", breaks Cmd-click / right-click "open in new tab", and misleads keyboard and screen reader users.

---

### Pair 2 — External links

**✅ Do — Name the destination, and say when it opens externally**

"Read the 8x8 security whitepaper (opens in new tab)" tells the user where they are going and what to expect. Add the "(opens in new tab)" affordance — visible text or `aria-label` — whenever `target="_blank"`.

**❌ Don't — Use "click here", "read more", or open a new tab silently**

Vague labels and silent new-tab opens fail sighted users and screen reader users alike. Screen readers list links out of context; "click here" tells them nothing.

<!-- STUB:GAP-018 source="Extract verbatim text from the 'Accessible external link' guidance section using Desktop Bridge or by requesting content from the designer. Verify against live Figma page (node 58394:123) once Desktop Bridge is running." -->

---

### Pair 3 — Chat surface

**✅ Do — Set `isChat` on every Link rendered inside a chat bubble**

Sent bubbles resolve to `$action07`; received bubbles resolve to `$action05`. Set `isChat` and the surface token does the rest.

**❌ Don't — Leave a default Link inside a chat bubble**

Default Link uses `$action08` — the correct blue for `$ui01` surfaces. On a filled sent bubble (`$ui13`/`$ui14`) it fails 4.5:1 contrast.

---

### Pair 4 — Inline vs Standalone

**✅ Do — Use Inline inside a sentence, Standalone when the link sits alone**

Inline links flow with surrounding type. Standalone lives in lists, table cells, card actions, free-standing CTAs; pick Small or Large to match the body type next to it.

**❌ Don't — Put Standalone in a paragraph, or use Inline as a free-floating CTA**

Standalone inside a paragraph breaks the reading rhythm. Inline as a standalone CTA inherits whatever size is in scope and ends up too small or oddly weighted.

<!-- STUB:GAP-003 source="Storybook exports inline-only shape (standalone: false, size: never). These pairs describe the visual/UX decision; the standalone prop shape should be confirmed against @8x8/oxygen-link source before implementation guidance is final." -->

---

### Pair 5 — Icon usage

**✅ Do — Add the pop-out icon when the link leaves the current app or site**

The icon is the visual partner to the "(opens in new tab)" affordance. Use it on links to external sites, external docs, or another 8x8 product that opens in a new tab.

**❌ Don't — Add icons to inline links inside body text, or to internal navigation**

Inline links mid-sentence fragment the reading rhythm. Internal navigation does not need the "you are leaving" signal.

---

## States

| State | Visual behaviour |
|-------|-----------------|
| Rest | `$action08` color, no decoration |
| Hover | `$hover07` color + underline |
| Focus | `$action08` color + underline + focus ring |
| Active | `$active14` color + underline + focus ring |
| Visited | `$textColor08` color |

## On surfaces

| Surface | Link token |
|---------|-----------|
| Default (`$ui01`) | `$action08` |
| Inverted surface | `$action10` |
| Sent chat bubble (`$ui13` / `$ui14`) | `$action07` |
| Received chat bubble (`$ui02`) | `$action05` |

## Content guidelines

- Avoid vague labels like "click here" — use words that describe the destination.
- Keep labels concise; avoid labels that wrap over multiple lines.
- For external links that open in a new tab, add "(opens in new tab)" as visible text or `aria-label`.
