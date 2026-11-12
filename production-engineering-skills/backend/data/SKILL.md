---
name: data
description: "Design and review backend data storage. Use for schema changes, migrations, transactions, indexing, tenant isolation, backups, and recovery."
---

# Backend Data and Database

Consider:
- migrations
- backward-compatible schema changes
- indexes
- unique constraints
- foreign keys
- transactions
- isolation/concurrency
- idempotency
- soft vs hard delete
- retention
- archival
- backups
- restore testing
- connection pooling
- query timeouts
- N+1 queries
- data ownership/tenant isolation
- audit fields
- PII handling

## Migration and recovery rules
- expand/contract: add nullable, backfill in batches, dual read/write, switch reads, then drop after the old code is gone
- set `lock_timeout` and `statement_timeout`; create indexes concurrently on large tables
- treat forward fixes as the rollback path unless a tested lossless down migration and data restore exist
- set RPO/RTO targets, a restore-drill cadence, and connection-pool sizing against the database connection limit
- define retention and deletion for PII in backups
