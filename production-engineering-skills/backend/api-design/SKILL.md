---
name: api-design
description: "Design and review backend API contracts. Use when changing resource models, request validation, error schemas, pagination, versioning, or compatibility."
---

# Backend API Design

Rules:
- keep resources stable, validate at runtime, and reject unknown fields
- errors use RFC 9457 `application/problem+json` with a stable machine-readable code
- cursor pagination with a default limit (for example 20) and maximum (for example 100); opaque cursors
- version through the path or media type; announce deprecation with `Deprecation`/`Sunset` and keep both versions live during migration
- unsafe methods with side effects accept an `Idempotency-Key`; persist `(principal, key, route, body_hash)` under a unique constraint with a TTL, replay the stored response, and return 409 for the same key with a different body
- return 429 with `Retry-After` and expose rate-limit headers consistently
- authenticated responses are `Cache-Control: private, no-store`, or `Vary: Authorization` where a shared cache is intended; never let a shared cache serve personalized data
- document the schema with OpenAPI or GraphQL SDL and keep it in sync with code
- GraphQL: bound depth, complexity, and cost; authorize per field; batch with DataLoader; disable introspection in production unless required; use persisted queries where supported
- gRPC: propagate deadlines and cancellation, and set per-call timeouts
- filter, sort, and search only on indexed, allowlisted fields
