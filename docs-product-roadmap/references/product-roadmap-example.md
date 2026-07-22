# Support Operations Roadmap Example

This example is illustrative. Its product, evidence, priorities, and measurements are fictional and demonstrate structure only. Never reuse them as real commitments or evidence.

Use `../assets/doc-starters/product-roadmap-doc.md` as the baseline, then adapt it to the roadmap's audience and uncertainty.

## Product Direction

Help support specialists resolve the right customer problems with less queue administration while preserving response quality and access controls.

## Strategic Objectives

| Objective | Target users / market | Success measure | Strategy source |
|---|---|---|---|
| Reduce avoidable triage work | Specialists handling multiple regional queues | Illustrative target: reduce median setup time before first ticket action by 50% | Fictional 2026 support-product strategy |
| Improve routing confidence | Support leads and specialists | Illustrative target: reduce incorrectly reassigned tickets without increasing first-response time | Fictional support-quality objective |

## Horizon Definitions

| Horizon | Meaning | Entry / exit criteria |
|---|---|---|
| Now | Active work with an evidenced problem, approved PRD, and measurable outcome | Complete when the outcome readout supports expand, iterate, or stop |
| Next | Important problems with evidence but unresolved solution or feasibility questions | Moves to Now after discovery, dependency review, and capacity decision |
| Later | Directionally important problem areas that need stronger evidence or strategy decisions | Reconsidered when named evidence or strategy triggers occur |

## Roadmap Overview

| Horizon | Outcome / problem | Strategic objective | Success signal | Confidence | Owner |
|---|---|---|---|---|---|
| Now | Specialists begin recurring triage work faster | Reduce avoidable triage work | Time from queue open to first ticket action | High: observed workflow problem and approved pilot | Product triad |
| Next | Fewer tickets require manual reassignment | Improve routing confidence | Reassignment rate with response-time guardrail | Medium: quantitative signal, causes still under study | Product |
| Later | Leads understand queue health before service degrades | Improve routing confidence | To be defined after opportunity research | Low: stakeholder request without user evidence | Unknown |

## Now

### Faster recurring triage setup

- **Target outcome:** Cut median setup time before the first ticket action from an illustrative 95 seconds to under 45 seconds during a 30-day pilot
- **Problem / opportunity:** Specialists repeatedly rebuild the same filter configurations across sessions
- **Why now:** Regional queue expansion is expected to increase configuration complexity
- **Evidence:** Illustrative workflow observations, 2026-06-10, covering six specialists from one support team; approved Saved Triage Views PRD, 2026-06-14
- **Candidate bets / committed initiatives:** Committed pilot of private saved views; candidate onboarding prompt for first-time setup
- **Success and guardrails:** Setup-time target; no increase in tickets handled with unintended filters
- **Dependencies:** Event instrumentation and existing permission checks
- **Risks / assumptions:** Specialists may create disposable views rather than a reusable set
- **Confidence:** High in the problem, medium in the proposed solution's impact
- **Owner:** Product triad
- **Completion criteria:** Pilot readout supports an explicit expand, iterate, or stop decision

## Next

### Fewer manual ticket reassignments

- **Target outcome:** Reduce avoidable reassignments without increasing first-response time
- **Problem / opportunity:** Reassignment appears concentrated in three queues, but the causes are not yet separated
- **Why prioritized:** Reassignment adds handling time and obscures queue ownership
- **Evidence:** Illustrative analytics review, 2026-06-18, covering three regional queues; reassignment causes were not instrumented
- **Candidate bets:** Queue-entry guidance, routing-rule feedback, or clearer ownership indicators; none is committed
- **Success signal:** Reassignment rate segmented by cause and queue, with first-response time as a guardrail
- **Dependencies:** Cause taxonomy and reliable reassignment instrumentation
- **Risks / assumptions:** Routing logic may not be the primary cause
- **Confidence:** Medium in the problem, low in any solution
- **Owner:** Product
- **Move-to-Now criteria:** Complete cause research, select an outcome threshold, and review feasibility with engineering

## Later

### Earlier visibility into queue-health degradation

- **Desired outcome:** Support leads recognize deteriorating queue health early enough to intervene
- **Why it matters:** Supports the broader response-quality objective
- **Current evidence:** Illustrative support-lead request, 2026-06-20, from one stakeholder; no user research or behavioral data
- **Key unknowns:** Which decisions leads cannot make today, which signals predict degradation, and whether another analytics surface already solves the need
- **Confidence:** Low
- **Reconsideration trigger:** Repeated lead interviews identify a common decision gap or service-level incidents show a detectable leading signal

## Not Now

| Opportunity or request | Reason not prioritized | Reconsideration trigger |
|---|---|---|
| Team-shared saved views | Private-view outcome is not yet validated and ownership rules are unresolved | Private-view adoption plus repeated evidence of sharing needs |
| Automated queue balancing | High operational and trust risk with insufficient problem evidence | Routing research demonstrates material preventable imbalance |

## Change Policy

- Review monthly and whenever a pilot readout, strategy change, or external commitment alters priorities
- Advance work only when the stated evidence, dependency, and capacity criteria are met
- Communicate material changes to support leadership and the product team
- Keep sprint sequencing and implementation issues in the delivery plan, not this roadmap
