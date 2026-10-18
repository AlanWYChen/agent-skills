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
- CSP
- clickjacking protection via CSP/frame-ancestors

Never rely on:
- hidden buttons
- disabled controls
- client-side route guards
- client-side role checks
as security controls.
