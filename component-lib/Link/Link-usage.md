---
component: Link
package: "@8x8/oxygen-link"
category: navigation
role: usage
role_description: "Usage guidelines — editorial merge of narrative extraction (2026-05-01) and usage-advisor Do/Don't pairs (2026-05-13)"
pipeline_stage: editorial
pipeline_note: "Do/Don't cards drafted by usage-advisor and pushed to Figma node 91658:1132 on ↳ Link examples (58394:123). Re-run figma-extract-usage once component instances are dropped into the preview frames. Audit verdict remains NO — resolve CONFLICTs GAP-003 and GAP-012 before doc-rewrite."
audit_verdict: NO
source_type: editorial
siblings:
  - "[[Link/props]]"
  - "[[Link/examples]]"
  - "[[Link/tokens]]"
  - "[[Link/accessibility]]"
  - "[[Link/Link-figma]]"
  - "[[Link/Link-audit]]"
tags:
  - oxygen
  - component/Link
  - role/usage
  - stage/editorial
  - category/navigation
---
<!-- SOURCE: editorial merge — narrative extraction (Figma node 58394:123, 2026-05-01) + usage-advisor Do/Don't pairs (2026-05-13) -->
<!-- FIGMA EXAMPLES PAGE: 58394:123 — ✅❌ Usage Guidelines section drawn at node 91658:1132 -->
<!-- PAIRS: 5 — awaiting component instances in preview frames before figma-extract-usage can run -->
<!-- GROUNDING: full — props.md, examples.md, tokens.md, accessibility.md, Link-figma.md, Link-audit.md -->

# Link — Usage Guidelines

> **See also:** [props.md](./props.md) · [tokens.md](./tokens.md) ·
> [examples.md](./examples.md) · [Link-figma.md](./Link-figma.md)

> **Editorial note:** Narrative sections extracted from Figma node 58394:123 (2026-05-01). Do/Don't pairs
> drafted by `usage-advisor` (Open mode, 2026-05-13) and pushed to the `↳ Link examples` page as card
> frames. Replace this file with `figma-extract-usage` output once component instances are in the frames.

---

## When to use

- When the user needs to navigate to a different page within the application.
- When the user needs to navigate to a different application.
- When the user needs to navigate to an entirely different site.

## When not to use

- When an action changes the state of the page or application — use a **Button** instead.

---

## Types of text links

| Type | Description |
|------|-------------|
| **Standalone** | Separated from body content; uses `$body02` typography; has explicit size (Small / Large) |
| **Inline** | Embedded within a sentence or paragraph; inherits the surrounding typography size |

---

## Sizing

- **Inline** — matches the surrounding text size; no explicit size control.
- **Standalone** — uses the `$body02` token; available in Small (14px / 20px lh) and Large (16px / 24px lh). Match the size to neighbouring body type — Small for 14px contexts, Large for 16px.

---

## Do / Don't

### Pair 1 — Link vs Button

#### ✅ Do — Use Link to navigate; use Button to act

If activating the affordance changes the URL or opens a new page/tab, use Link. If it submits, opens a modal, toggles a setting, or otherwise changes app state without navigating, use Button. The native HTML — `<a href>` vs `<button>` — is what screen readers and keyboard users rely on.

#### ❌ Don't — Use a Button (styled or otherwise) to navigate

A "button that goes to a page" announces as "button", suggests an in-place action, and breaks Cmd-click / right-click "open in new tab". A Link styled like a button is fine; a Button used for navigation is not.

**Grounded in:** [Link-usage.md — When not to use](./Link-usage.md) · [accessibility.md:30–33](./accessibility.md) · [Button-usage.md:152](../Button/Button-usage.md)

---

### Pair 2 — Make external links self-describing

#### ✅ Do — Name the destination, and say when it opens externally

Screen readers can list every link on a page out of context. "Read the 8x8 security whitepaper (opens in new tab)" tells the user where they are going and what to expect; "click here" tells them nothing. Add the "(opens in new tab)" affordance — either as visible text or visually-hidden text — whenever `target="_blank"`.

#### ❌ Don't — Use "click here", "read more", or open a new tab silently

Three failure modes in one card: vague label, no destination, no new-tab announcement. The user hears "link, click here" and has no way to decide whether to follow it.

**Grounded in:** [accessibility.md:53–54](./accessibility.md) · [Link-usage.md — Content guidelines](./Link-usage.md)

---

### Pair 3 — Chat surface

#### ✅ Do — Set `isChat` on every Link rendered inside a chat bubble

Let the component pick the right token for the bubble surface. Sent bubbles resolve to `$action07`; received bubbles resolve to `$action05`. Set `isChat`, render inside the right bubble, and the surface token does the rest.

#### ❌ Don't — Leave a default Link inside a chat bubble

Default Link uses `$action08` — the same blue that works on `$ui01`. On a filled sent bubble (`$ui13` / `$ui14`) it fails 4.5:1 contrast and the link becomes harder to spot against the bubble background.

**Grounded in:** [tokens.md:48–56](./tokens.md) · [props.md:69](./props.md)

---

### Pair 4 — Inline vs Standalone

#### ✅ Do — Use Inline inside a sentence, Standalone when the link sits alone

Inline links flow with the type around them and inherit size and weight from context. Standalone lives in lists, table cells, card actions, free-standing CTAs; pick the size that matches the body type next to it — Small for 14px contexts, Large for 16px.

#### ❌ Don't — Put Standalone in a paragraph, or use Inline as a free-floating CTA

Standalone inside a paragraph breaks the reading rhythm — its forced size jumps out of the surrounding type. Inline as a standalone CTA inherits whatever size is in scope and ends up too small or oddly weighted next to a Button or card.

**Grounded in:** [props.md:56–61](./props.md) · [Link-figma.md:210](./Link-figma.md) ·
⚠️ Prop signature is unresolved — see CONFLICT GAP-003 in [Link-audit.md](./Link-audit.md). This card describes the visual decision only.

---

### Pair 5 — Icon usage

#### ✅ Do — Add the pop-out icon when the link leaves the current app or site

The icon is the visual partner to the "(opens in new tab)" affordance — together they tell sighted and assistive-tech users the same thing. Use it on links to external sites, external docs, or another 8x8 product that opens in a new tab.

#### ❌ Don't — Add icons to inline links inside body text, or to internal navigation

Inline links inherit the surrounding type and an icon mid-sentence fragments the reading rhythm. Internal route changes do not need the "you are leaving" signal — the icon adds visual noise without adding information.

**Grounded in:** [Link-figma.md:50–55](./Link-figma.md) · [props.md:68](./props.md)

---

## States

| State | Visual behaviour |
|-------|-----------------|
| Rest | `$action08` color, no decoration |
| Hover | `$hover15` color + underline |
| Focus | `$action08` color + underline + focus ring |
| Active | `$active14` color + underline + focus ring |
| Visited | `$textColor08` color (violet / white in dark) |

> ⚠️ Hover token identity conflict — see CONFLICT GAP-012 in [Link-audit.md](./Link-audit.md). `$hover07` (tokens.md) and `$hover15` (Figma) may refer to the same token. Resolve before doc-rewrite.

See [tokens.md](./tokens.md) for full token values per mode/inverted surface.

---

## On surfaces

Links adapt their color tokens based on the surface they sit on:

| Surface | Link token |
|---------|-----------|
| Default (`$ui01`) | `$action08` |
| Inverted surface | `$action10` |
| Sent chat bubble (`$ui13` / `$ui14`) | `$action07` |
| Received chat bubble (`$ui02`) | `$action05` |

---

## Content guidelines

- Avoid vague labels like "click here" — use accurate, descriptive words that describe the destination.
- Keep labels concise. Avoid labels that wrap over multiple lines.
- For external links that open in a new tab, add "(opens in new tab)" as visible text or `aria-label` — see Pair 2.

---

## Related components

- **Button** — use when the action changes application state rather than navigating.
- **Forms** pattern — links are often used within form layouts.
- **Typography** foundation — inline links inherit from surrounding type styles.

---

## Gaps

| Gap | Type | Status |
|-----|------|--------|
| No ✅ Do / ❌ Don't cards | SOURCE_GAP | **Closed** — 5 pairs drafted (2026-05-13) and pushed to Figma node 91658:1132. Add component instances to preview frames, then re-run `figma-extract-usage`. |
| "Accessible external link" section text | SOURCE_GAP | Text too small in original screenshot; covered editorially in Pair 2 above. Verify against live Figma page once Desktop Bridge is running. |
| Inline link visual example | SOURCE_GAP | No captured screenshot of inline link in running text. Add to Pair 4 preview frame. |
| `$action05` token value | DOC_GAP | Token value not returned in oxygen-mcp token search; need separate lookup. |
| Standalone/size prop signature | CONFLICT (GAP-003) | Discriminated-union type unresolved. Pair 4 describes visual decision only. Resolve before doc-rewrite. |
| Hover token identity | CONFLICT (GAP-012) | `$hover07` (tokens.md) vs `$hover15` (Figma). Resolve before doc-rewrite. |

---

_Source: Figma screenshot (node 58394:123) · Oxygen MCP · usage-advisor Open mode · Merged 2026-05-13_
