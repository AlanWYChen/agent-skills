---
name: audit
description: "Guide backend audit. Use when implementing or reviewing production readiness, security, reliability, testing, release configuration, and prioritized findings in backend applications."
---

# Backend Production Audit

Audit:
- API design
- authentication
- authorization
- runtime validation
- data integrity
- migrations
- security
- reliability
- observability
- background jobs
- webhook behavior
- unit/integration/contract/E2E coverage
- load/resilience testing where justified
- GitHub Actions CI/CD
- deployment and rollback

Repository sweep:
- TODO
- FIXME
- hard-coded credentials
- debug endpoints
- unrestricted CORS
- disabled auth
- test keys
- localhost production config
- missing timeouts
- unbounded retries

Classify:
- Critical: exploitable authorization bypass, data loss or corruption, secret exposure, or unauthenticated access to sensitive data
- High: missing object-level authorization, unsafe retries on non-idempotent writes, unbounded resource use, or absent authorization checks on a reachable path
- Medium: degraded failure handling, missing observability for critical paths, or inconsistent validation
- Low: polish or maintainability

Treat each sweep item as a check with evidence: cite the file, the command, and the observed output.

Do not call the service production-ready while any Critical or High finding remains open; a documented risk acceptance must name an owner and a date.
