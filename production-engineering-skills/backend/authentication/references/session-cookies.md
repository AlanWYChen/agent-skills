# Backend Session Cookies

For cookie-based sessions:

- `HttpOnly`, `Secure`, and `SameSite=Lax` by default: `Strict` for high-risk sessions, and `None` only for cross-site flows with `Secure`.
- `__Host-` prefix, `Path=/`, and no `Domain` attribute.
- High-entropy session IDs stored server-side, rotated on sign-in and on privilege change.
- Idle and absolute timeouts, server-side revocation, and logout-all-sessions.
- CSRF protection for cookie-authenticated state changes: a synchronizer token or `Origin`/`Sec-Fetch-Site` validation. `SameSite` alone is not sufficient.
- Never put session IDs in URLs, logs, or client-readable storage.
