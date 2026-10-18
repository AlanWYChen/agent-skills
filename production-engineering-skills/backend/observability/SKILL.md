---
name: observability
description: "Guide backend observability. Use when implementing or reviewing logs, metrics, failures, correlation, alerts, and sensitive data redaction in backend applications."
---

# Backend Observability

Use:
- structured JSON logs
- request IDs
- correlation IDs
- metrics
- distributed traces
- dashboards
- actionable alerts

Track at minimum where applicable:
- request rate
- error rate
- latency
- saturation
- dependency latency/errors
- DB latency/connections
- queue depth
- job retries/failures
- webhook failures
- cache hit rate

Never log:
- passwords
- full auth tokens
- API keys
- private keys
- unnecessary sensitive data

Propagate trace/correlation context across HTTP, queues, and jobs.
