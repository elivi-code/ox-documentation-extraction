---
component: List
package: "@8x8/oxygen-list"
category: data_display
role: pui
role_description: "Platform UI integration notes — notifications, navigation, session, event bus"
pipeline_stage: blocked
pipeline_note: "Audit verdict NO — CONFLICTs must be resolved first"
audit_verdict: "NO"
siblings:
  - "[[List/props]]"
  - "[[List/examples]]"
  - "[[List/tokens]]"
  - "[[List/accessibility]]"
  - "[[List/List-figma]]"
  - "[[List/List-audit]]"
tags:
  - oxygen
  - component/List
  - role/pui
  - stage/blocked
  - category/data_display
---

<!-- SOURCE: platform-ui-mcp snapshotId: mcpVersion 0.6.1 / buildDate 2026-02-24 -->
<!-- EXTRACTED: 2026-05-08 -->
<!-- COMPONENT: List -->
<!-- CONFIRMED BY: auto-mode — single candidate rejected as false positive (see below) -->

# List — Platform UI Context

<!-- NO RELEVANT PUI CONTEXT -->

The `List` / `ListItem` component (`@8x8/oxygen-list`) is a pure display/layout component with no application-layer infrastructure concerns in Platform UI. Searches for "list" and "list item" returned no semantically relevant PUI packages.

## Hooks

<!-- NONE IDENTIFIED -->

## Events

<!-- NONE IDENTIFIED -->

## Related MFEs

<!-- NONE IDENTIFIED -->

## Usage examples

<!-- NONE IN CONFIRMED DOCS -->

## Candidates rejected

| Package | Relevance score | Reason for rejection |
|---------|----------------|----------------------|
| `@8x8/pui-mfe-registry-api` | 20 | Matched the generic word "list" in the phrase "a given **list** of MFEs" — unrelated to the List UI component |

_Source: platform-ui-mcp · Extracted 2026-05-08_
