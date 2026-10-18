---
name: reliability
description: "Design and review backend reliability. Use for dependency failures, bounded retries, timeouts, graceful shutdown, capacity, and recovery."
---

# Backend Reliability

Design for partial failure.

Consider:
- timeouts
- retries
- exponential backoff
- jitter
- retry budgets
- circuit breakers where appropriate
- idempotency
- deduplication
- graceful shutdown
- health/readiness checks
- load shedding
- queue backpressure
- dependency degradation
- fallback behavior
- dead-letter queues
- disaster recovery
- capacity limits
