# Collector + Summarizer Architecture Example

Use `../assets/doc-starters/architecture-doc.md` as the baseline, then adapt it to the system or domain you are documenting.

## Overview

This example shows a multi-service pipeline where a collector discovers external links and a summarizer enriches extracted content. The architecture doc focuses on boundaries, shared coordination patterns, and how related design docs fit together.

Service and component design docs live in `docs/designs/`. Feature docs live in `docs/features/`.

## Scope & Boundaries

- Covers the shared pipeline, coordination model, and runtime boundaries
- Leaves worker-specific implementation details to service design docs

## Architecture Principles

### 1. Database-Driven Service Coordination
- Internal services communicate via table state transitions rather than direct service-to-service APIs.
- This keeps workers decoupled and easier to scale independently.

### 2. Independent Worker Services
- Collector and summarizer are separately deployable and independently scalable.
- Failures in one stage do not block unrelated runtime surfaces.

### 3. Explicit State Lifecycles
- Each processing table has clear intermediate and terminal states.
- Retries remain bounded and idempotent.

## System / Domain Topology

```
External Sources -> Collector Service -> link_queue -> Summarizer Service -> summaries
```

**Active Components:**
- **Collector Service** - Fetches links and enqueues normalized work items.
- **Summarizer Service** - Claims queued content, generates summaries, and persists outputs.
- **PostgreSQL** - Shared system of record and coordination layer.

## Shared Patterns

- Queue claims use row-level locking and state transitions
- Service boundaries are enforced through tables and explicit ownership

## Data / Control Flow

### Stage 1: Collection
**Input:** External source feeds
**Process:** Fetch links, canonicalize URLs, insert queue rows with `pending` status
**Output:** `link_queue` rows ready for processing

### Stage 2: Summarization
**Input:** Queue rows with `pending` status
**Process:** Claim work, extract content, generate summaries
**Output:** `summaries` rows linked to processed content

## Deployment / Runtime Model

- Collector and summarizer run as scheduled jobs or workers
- Database credentials are scoped per service role

## Security & Operations

- Worker services use least-privilege database access
- Structured logs capture queue claims, retries, and terminal failures
- Retry attempts are bounded to avoid infinite processing loops

## Related Design Docs

- [Collector Service](./designs/example-collector.md)
- [Summarizer Service](./designs/example-summarizer.md)
- [Content Discovery Feature](./features/discovery.md)

## References

- [Project README](../README.md)
- [Architecture Starter](../assets/doc-starters/architecture-doc.md)
