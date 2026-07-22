# Saved Triage Views PRD Example

This example is illustrative. Its product, evidence, and measurements are fictional and demonstrate structure only. Never reuse them as real evidence.

Use `../assets/doc-starters/product-requirements-doc.md` as the baseline, then adapt the depth to the decision being made.

## Summary

Support specialists repeatedly rebuild the same ticket filters during daily queue triage. Saved Triage Views would let returning specialists reopen a named filter configuration, with the intended outcome of reducing setup time without changing the shared queue model.

## Problem and Why Now

Support specialists use the same combinations of queue, severity, region, and assignment filters several times per shift. The current product resets those filters between sessions. The support organization is adding regional queues next quarter, which is expected to increase the number of combinations specialists manage.

## Strategic Fit

- **Objective:** Increase the number of tickets resolved per specialist without reducing response quality
- **Contribution:** Remove repeated queue setup from common triage workflows
- **Decision:** Whether to validate and scope private saved views for the next product cycle

## Target Users

| Segment / Actor | Context and need | Current behavior or workaround | Excluded users |
|---|---|---|---|
| Support specialists handling multiple queues | Reopen recurring triage configurations quickly | Rebuild filters manually or keep browser tabs open | Administrators configuring shared routing rules |

## Evidence

| Claim | Type | Source and date | Strength / limitation |
|---|---|---|---|
| Repeated filter setup appears in most observed triage sessions | Fact | Illustrative synthesis of 6 workflow observations, 2026-06-10 | Small sample from one support team |
| Regional queue expansion is likely to increase the number of recurring filter combinations | Inference | Illustrative regional-queue planning brief, 2026-06-12 | Expected workflow impact has not been observed |

## Desired Outcomes

| Outcome | Metric | Baseline | Target | Population and window | Data source | Guardrail |
|---|---|---|---|---|---|---|
| Specialists begin recurring triage work faster | Median time from queue open to first ticket action | Illustrative baseline: 95 seconds | Under 45 seconds | Pilot specialists during the first 30 days | Product event instrumentation | No increase in tickets handled with unintended filters |

## Scope

### In Scope

- Save the current supported ticket-filter configuration under a user-provided name
- Reapply, rename, and delete private saved views
- Make the active saved view and later manual changes distinguishable

### Non-Goals

- Sharing views across a team
- Changing ticket routing or queue permissions
- Saving sort order, table columns, or dashboard layout in the first release

## User Journeys and Requirements

### Reopen a recurring triage view

1. A returning specialist opens a ticket queue
2. The specialist selects one of their saved views
3. The queue applies the stored filter configuration and identifies the active view
4. If the specialist changes a filter, the product shows that the active configuration differs from the saved view

| ID | Requirement | Rationale / linked outcome | Acceptance evidence |
|---|---|---|---|
| PR-1 | A specialist can save a valid current filter configuration with a unique name in their private view list | Reduce repeated setup | A saved view can be selected in a later session and restores the supported filters |
| PR-2 | Applying a saved view never grants access to queues or tickets the specialist cannot otherwise access | Preserve authorization boundaries | Permission tests show inaccessible records remain excluded |
| PR-3 | The interface distinguishes a stored view from unsaved filter changes | Prevent mistaken triage context | Usability test participants can identify whether current filters match the saved view |

## Technology Considerations

The product requires durable user-scoped storage, authorization through existing queue permissions, and low-latency application of a small filter payload. Storage shape and API design remain technical-design decisions. No new datastore is justified by the product requirements alone.

## Risks and Assumptions

| Item | Type | Criticality | Evidence | Validation / resolution | Owner |
|---|---|---|---|---|---|
| Specialists will create a small reusable set rather than many disposable views | Assumption | Medium | No usage evidence yet | Pilot with a soft limit and review creation patterns | Product |
| Users understand when manual filter changes diverge from a saved view | Assumption | High | Existing UI has no equivalent state | Test two state treatments with five representative specialists | Design |

## Validation and Rollout

- Test a clickable prototype with specialists from two regions
- Instrument view creation, application, divergence, deletion, and first ticket action
- Pilot with one support group before broader availability
- Review outcome and guardrail metrics after 30 days before considering shared views

## Decision Log

| Date | Decision | Rationale and evidence | Decision maker |
|---|---|---|---|
| 2026-06-14 | Limit initial scope to private saved views | Keeps the test focused on repeated setup and avoids unresolved team ownership rules | Illustrative product review |
