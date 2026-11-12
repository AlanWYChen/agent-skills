---
name: webhooks
description: "Implement or review incoming and outgoing webhooks. Use for signature verification, replay prevention, idempotency, ordering, delivery, and retries."
---

# Webhook Handling

For incoming webhooks:
- verify signatures against the raw request body before parsing JSON
- compare signatures in constant time
- validate the timestamp within a small clock-skew tolerance (for example ±300 s)
- keep two active secrets during rotation
- parse and validate schema
- acknowledge quickly
- enqueue heavy work
- deduplicate events by provider event ID with a unique constraint and return 2xx for duplicates
- make handling idempotent
- handle out-of-order events
- persist processing state
- retry safely
- provide operational visibility for failures

For outgoing webhooks:
- sign `timestamp + "." + body` with HMAC-SHA256 and send the timestamp and key ID
- cap retries (for example 24–72 h) with exponential backoff and jitter, isolating failures per endpoint
- validate destination URLs and reject private, link-local, and metadata ranges, re-checking redirects (SSRF)
- include event IDs
- version events
- allow secret rotation
