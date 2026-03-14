# [Project or Domain] Architecture

## Overview

[1-3 paragraphs describing the system or domain, the scope of this doc, and why the architecture matters.]

Service and component design docs live in `docs/designs/`. Feature docs live in `docs/features/`.

## Scope & Boundaries

- [What this architecture doc covers]
- [What related docs it links out to instead of duplicating]

## Architecture Principles

### 1. [Principle Name]
- [Principle detail]
- [Why it matters]

### 2. [Principle Name]
- [Principle detail]
- [Why it matters]

### 3. [Principle Name]
- [Principle detail]
- [Why it matters]

## System / Domain Topology

[Describe the major components and the boundaries between them.]

```
[Optional high-level diagram: Mermaid or ASCII]
```

**Active Components:**
- **[Component A]** - [Responsibility]
- **[Component B]** - [Responsibility]
- **[Component C]** - [Responsibility]

## Shared Patterns

- [Pattern or convention]
- [Pattern or convention]

## Data / Control Flow

### Stage 1: [Name]
**Input:** [Source]
**Process:** [Summary]
**Output:** [Result]

### Stage 2: [Name]
**Input:** [Source]
**Process:** [Summary]
**Output:** [Result]

## Deployment / Runtime Model

- [Runtime platform and workload types]
- [How workloads are scheduled or scaled]
- [Environment or secret management model]

## Security & Operations

- [Trust boundaries and public entry points]
- [Authentication or authorization model]
- [Observability, failure handling, or recovery model]

## Related Design Docs

- [Component or service design doc]
- [Feature doc]
- [Operational or deployment doc]

## Open Questions

- [ ] Question 1
- [ ] Question 2

## References

- [Project README](../README.md)
- [Related architecture or design docs]
