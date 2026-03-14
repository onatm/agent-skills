# Search Indexing Worker Example

Use `../assets/doc-starters/component-design-doc.md` as the baseline, then adapt it to the component or service you are documenting.

## Overview

The Search Indexing Worker transforms normalized content into search-ready documents so query latency stays low and ranking quality stays consistent.

## Context & Problem

**Background:** Content is stored in relational tables, but search workloads need denormalized documents. Without a worker, indexing becomes inconsistent and fresh content is not queryable quickly.

## Goals

**Goals:**
- Keep index freshness under 60 seconds
- Maintain idempotent indexing on retries
- Avoid direct coupling between API handlers and index writes

## Scope & Ownership

- Owns indexing-ready transformations from normalized content into search documents
- Does not own upstream content ingestion or the query UI
- Integrates with relational storage and the search document store

## Technical Design

### High-Level Approach

- Poll ready records from `content`
- Build index documents with normalized tags and metadata
- Upsert into `search_documents`

### Interfaces & Contracts

- Reads records in a ready-to-index state from `content`
- Writes denormalized documents to `search_documents`
- Relies on stable keys so retries overwrite rather than duplicate

### Data Model / State

- `search_documents` stores denormalized search payloads
- Worker claims `content` rows using explicit state transitions

### Runtime / Operations

- Batch polling controls throughput and backpressure
- Retries must be idempotent and visible in worker logs
- Failures should not block unrelated content from being indexed

### Security & Privacy

- Worker uses service credentials with scoped write access
- Only public or publishable fields are indexed

### Key Design Decisions

**Decision 1:** Queue-based batch indexing
- **Rationale:** Controlled throughput and backpressure management.
- **Trade-offs:** Slightly stale reads under heavy ingest.

**Decision 2:** Idempotent upsert writes
- **Rationale:** Safe retries without duplicate index records.
- **Trade-offs:** More careful key design required.

## Impact

**System Impact:**
- Predictable indexing throughput
- Better query performance for discovery pages
- Additional worker operations overhead

## Open Questions

- [ ] Should index updates be event-driven instead of polling?
- [ ] What is the acceptable reindex window for backfills?

## References

- [Architecture Guide](../ARCHITECTURE.md)
- [Web Architecture](../designs/web-architecture.md)
