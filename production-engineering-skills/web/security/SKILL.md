---
name: security
description: "Guide web security. Use when implementing or reviewing trust boundaries, authorization, input validation, secret handling, and application vulnerabilities in web applications."
---

# Web Security

Focus on browser, HTTP, application, and API boundaries.

Check:
- server-side authentication and authorization
- CSRF
- XSS
- SQL/NoSQL injection
- SSRF
- open redirects
- path traversal
- command injection
- secure file uploads
- security headers
- restrictive CORS
- secure cookies
- secret exposure
- rate limiting
- abuse prevention
- dependency vulnerabilities
- CSP (nonces or hashes rather than `unsafe-inline`)
- clickjacking protection via CSP/frame-ancestors
- Subresource Integrity for third-party scripts and styles where the host supports CORS

Never rely on:
- hidden buttons
- disabled controls
- client-side route guards
- client-side role checks
as security controls.

Baseline: HTTPS with HSTS (including subdomains once verified), a CSP with `frame-ancestors` (nonces or hashes rather than `unsafe-inline`), `X-Content-Type-Options: nosniff`, a strict `Referrer-Policy`, and a minimal `Permissions-Policy`. Set them once in `next.config` headers, middleware, or host configuration and verify every route.

Client-exposed prefixes (`NEXT_PUBLIC_`, `VITE_`, `PUBLIC_`) are inlined into the bundle at build time, so only public values may use them; keep secrets in server-only modules and check the built bundle.

## Uploads and injection
- validate uploads by magic bytes and an allowed MIME set, cap size, randomize stored names, keep files outside the webroot, serve through signed URLs, and scan where feasible
- sanitize `dangerouslySetInnerHTML` input and allowlist URL schemes for user-supplied links
