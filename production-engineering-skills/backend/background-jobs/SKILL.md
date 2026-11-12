---
name: background-jobs
description: "Design and review background jobs and queues. Use for asynchronous processing, retries, deduplication, ordering, and safe reprocessing."
---

# Background Jobs and Queues

For jobs/events consider:
- idempotency
- retry policy
- exponential backoff
- jitter
- max attempts
- dead-letter queue
- poison-message handling
- deduplication
- ordering requirements
- visibility timeout/lease behavior
- job timeout
- cancellation
- observability
- progress/state reporting
- safe reprocessing
- transactional outbox/inbox patterns where needed
- write outbox rows in the same transaction as the state change and relay them through a publisher or change log
- deduplicate consumers with a unique `(consumer, event_id)`
- order by aggregate key where required; keep the visibility timeout above the maximum job duration and extend leases
- assume at-least-once delivery and support DLQ redrive
