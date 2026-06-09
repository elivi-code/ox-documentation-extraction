---
parent: "[[Tabs]]"
section: platform
pipeline_stage: doc_rewrite
tags:
  - oxygen
  - component/Tabs
  - role/spoke
  - section/platform
---

<!-- NO RELEVANT PUI CONTEXT -->

## Platform UI Context

No Platform UI packages are relevant to the Tabs component. The component is self-contained within `@8x8/oxygen-tabs` and has no application-layer concerns (no navigation hooks, notification infrastructure, session management, or event bus integration required).

### Candidates rejected

| Package | Relevance score | Reason |
|---------|----------------|--------|
| `@8x8/pui-use-navigation` | 90 | General shell navigation hook — not Tabs-specific; routing belongs in the application shell, not the component |
| `@8x8/pui-use-navigate-to-base-path` | 20 | Keywords match only — not Tabs-specific |
| `@8x8/pui-observability-react-router` | 20 | Routing analytics — not Tabs-specific |

_Source: Platform UI MCP · Confirmed by engineer 2026-04-30_
