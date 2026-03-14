# [Component or Service Name]

**Status:** [Draft | In Review | Approved | Implemented]

**Location:** `docs/designs/[component-name].md`

---

## Overview

A brief summary of what this component or service is responsible for and why it exists.

## Context & Problem

**Background:** What is the current implementation context? What technical problem is this design addressing?

## Goals

**Goals:**
- Primary objective 1
- Primary objective 2
- Primary objective 3

## Scope & Ownership (Optional)

- [What this component owns]
- [What remains outside its scope]
- [Which teams or services it interacts with]

## Technical Design

<!-- The sub-sections below are a baseline. Adapt, merge, reorder, or replace them with domain-specific sections
when that better fits the component. Common additions: Processing Flow, Algorithm, Configuration, Examples. -->

### High-Level Approach

Describe the implementation shape at a system level. What are the major responsibilities, interactions, and boundaries?

```
[Optional: Include a concise architecture or sequence diagram]
```

### Processing Flow (Optional)

<!-- For pipeline-style components, an ASCII or code-block diagram of data flow can replace or supplement prose. -->

```
[Input]
  -> [Stage 1]
  -> [Stage 2]
  -> [Output]
```

### Algorithm (Optional)

<!-- For components with non-trivial logic, enumerate the steps here. -->

1. [Step 1]
2. [Step 2]
3. [Step 3]

### Configuration (Optional)

<!-- For components with tunable thresholds, flags, or env vars. -->

- `CONFIG_KEY` — description and default

### Examples (Optional)

<!-- For components where worked examples clarify behavior better than prose. -->

**Example 1: [Scenario name]**

- [Input or context]
- [Expected output or behavior]

### Interfaces & Contracts

- [API, event, job, or module contract]
- [Validation or compatibility expectations]

### Data Model / State

- [Schema, state machine, or key persisted data]
- [Relevant migrations or contract changes]

### Runtime / Operations

- [Concurrency, retries, scheduling, or scaling behavior]
- [Failure modes, observability, or recovery model]

### Security & Privacy

- [Trust boundaries]
- [Auth, secrets, or sensitive data handling]

### Key Design Decisions

**Decision 1:** [Important technical choice]
- **Rationale:** Why this choice?
- **Trade-offs:** What are we gaining and losing?

**Decision 2:** [Important technical choice]
- **Rationale:** Why this choice?
- **Trade-offs:** What are we gaining and losing?

## Impact

**System Impact:**
- Performance implications
- Scalability considerations
- Operational overhead

## Rollout / Migration (Optional)

- [Migration, compatibility, or rollout note]

## Open Questions (Optional)

- [ ] Question 1
- [ ] Question 2

## References

- [Related architecture doc]
- [Related feature doc]
- [External documentation]
