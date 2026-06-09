---
parent: "[[ProgressBar]]"
section: composition
component: ProgressBar
pipeline_stage: spec_ready
tags:
  - oxygen
  - component/ProgressBar
  - role/spoke
  - section/composition
---

## Subcomponents

ProgressBar has no subcomponents. All structural elements (track background, loading fill, complete fill, text label) are internal to the component and not independently instantiable.

## Common combinations

| Component | Relationship | When |
|-----------|-------------|------|
| [[Spinner]] | Peer — swap when progress is indeterminate | Replacing or alternating with ProgressBar when a percentage is unavailable |
| [[SkeletonBlock]] | Peer — swap when placeholder content is needed | Content-loading states where a horizontal fill would be misleading |
| [[Toast]] | Successor — show on completion or error events | After `value` reaches 100 to confirm success, or on failure to communicate an error |
| [[AlertBanner]] | Successor — show on failure | When a long-running process fails and inline page-level feedback is needed |

## Internal Figma structure

The Figma `Bar` component set (node `30880:55942`) contains 4 variants (2 `status` × 2 `mode`). Internal optional slots:

| Slot | Layer name | Visibility |
|------|-----------|-----------|
| Loading fill | `linear-bar-indicator` | Visible when `status=loading` |
| Complete fill | `linear-bar-bg-complete` | Visible when `status=complete` |
| Text label | text layer | Toggled by `text?` boolean |

## Usage patterns

- **Upload / download flow:** ProgressBar is placed in a card or modal alongside a filename and cancel action. On completion, it transitions to a [[Toast]] confirmation or in-place success state.
- **Multi-step job monitor:** ProgressBar displays job progress in a sidebar or status panel. Completion swaps text label and optionally triggers a [[Toast]].
