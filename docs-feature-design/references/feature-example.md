# Saved Filters Example

Use `../assets/doc-starters/feature-doc.md` as the baseline, then adapt it to the user-facing feature you are documenting.

## Overview

Saved Filters let users store frequently used query settings and reapply them quickly across sessions.

## User Problem

**Background:** Users repeatedly rebuild the same filter combinations when triaging long result sets. That repetition slows the workflow and increases the chance of filter mistakes.

## Goals

**Goals:**
- Let users reapply common filter sets quickly
- Reduce repeated setup work across sessions
- Keep the behavior understandable on both desktop and mobile

## Non-Goals

- Team-wide sharing of saved filters in the initial release
- Redesigning the underlying filtering model

## Audience / Actors

- Returning users who revisit the same filtered views
- Users triaging long result sets with repeated workflows

## Primary Flows

### Flow 1: Save the current filter setup
1. The user configures filters on a list view
2. The user saves the current filter setup with a name
3. The saved filter becomes available for later reuse

### Flow 2: Reapply a saved filter
1. The user opens the saved filters menu
2. The user picks a previously saved filter
3. The list updates to the saved filtering state

### Flow 3: Manage saved filters
1. The user views existing saved filters
2. The user renames or deletes a saved filter
3. The updated list reflects the change immediately

## Key Behaviors and Rules

- Saved filters are private to the user who created them
- Applying a saved filter restores the named filter configuration as a single action
- Users can rename or delete saved filters after creation
- The feature should remain optional for users who prefer standard filter controls

## User Impact

- Returning users can resume common workflows faster
- Repeated triage tasks require fewer manual filter adjustments
- The feature adds convenience without changing the default filtering experience

## Dependencies & Linked Design Docs

- [Web App](../designs/web.md)
- [Web Architecture](../designs/web-architecture.md)

If technical design is needed, document it separately in `docs/designs/`.

## Open Questions

- [ ] Should saved filters support team sharing in a future release?
- [ ] Do we cap the number of saved filters per user?

## References

- [Related feature docs]
- [Product requirements]
