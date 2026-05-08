---
component: TextField
package: "@8x8/oxygen-textField"
category: form_inputs
role: pui
role_description: "Platform UI context — infrastructure hooks (navigation, notifications, session, event bus)"
pipeline_stage: spec_ready
pipeline_note: "Audit verdict YES/PARTIAL — doc-rewrite can run"
audit_verdict: YES
siblings:
  - "[[TextField/props]]"
  - "[[TextField/examples]]"
  - "[[TextField/tokens]]"
  - "[[TextField/accessibility]]"
  - "[[TextField/figma]]"
  - "[[TextField/TextField-audit]]"
tags:
  - oxygen
  - component/TextField
  - role/pui
  - stage/spec_ready
  - category/form_inputs
---
<!-- SOURCE: platform-ui-mcp snapshotId: build-2026-02-24 -->
<!-- EXTRACTED: 2026-04-29 -->
<!-- COMPONENT: TextField -->
<!-- CONFIRMED BY: auto-mode (no relevant candidates returned by search) -->

# TextField — Platform UI Context

## Hooks
<!-- NONE IDENTIFIED -->

## Events
<!-- NONE IDENTIFIED -->

## Related MFEs
<!-- NONE IDENTIFIED -->

## Usage examples
<!-- NONE IN CONFIRMED DOCS -->

## Candidates rejected

Search for "textField" → 0 results.
Search for "input" → 1 result:

- `@8x8/pui-use-navigation` (score 20, matched in readme)
  Excerpt: `...form > <input type="text" onChange={() => blockNavigation(true)} />`
  **Rejected** — this is a navigation-blocking hook that incidentally uses a bare HTML `<input>` in its usage example. It has no relationship to the Oxygen TextField UI component.

Platform UI packages are infrastructure-focused (MFE composition, event bus, observability, hooks for navigation/config/session) and contain no TextField-specific integration context.
