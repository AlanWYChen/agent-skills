---
name: security
description: "Guide backend security. Use when implementing or reviewing trust boundaries, authorization, input validation, secret handling, and application vulnerabilities in backend applications."
---

# Backend Security

Check:
- authentication
- authorization
- least privilege
- runtime schema validation
- SQL/NoSQL injection
- command injection
- SSRF
- path traversal
- unsafe deserialization
- secret management
- rate limiting
- abuse controls
- dependency vulnerabilities
- secure defaults
- sensitive log redaction
- security audit logging for privileged and high-impact actions
- encryption in transit
- encryption at rest where appropriate
- tenant isolation
- file/object authorization
- admin endpoint protection

Treat every external system and client as untrusted.

Normative defaults:
- authorize every object access server-side (BOLA/IDOR) and scope every query by tenant
- reject unknown fields on write models (mass assignment)
- restrict user-supplied outbound URLs against private, link-local, and metadata ranges (SSRF), re-checking redirects
- derive client IP from a trusted proxy configuration, never from an untrusted header
- enforce request size and time limits at the edge
- enforce rate limits at the edge or atomically in a shared store, keyed by principal and route class; use separate strict buckets for sign-in, OTP, and password reset, return 429 with `Retry-After`, and define fail-open or fail-closed behavior
