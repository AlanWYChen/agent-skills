# Web Session Cookies

For server-managed browser sessions, sensitive cookies should generally be:

- `HttpOnly`
- `Secure`
- `SameSite=Lax` by default, `Strict` for high-risk sessions, and `None` only for cross-site flows and always with `Secure`
- narrowly scoped by domain/path
- rotated after authentication/privilege changes
- invalidated on logout

Also consider:
- CSRF protection
- session expiration
- idle timeout
- absolute timeout
- server-side revocation
- logout-all-sessions
- session fixation protection

Use the `__Host-` prefix with `Path=/` and no `Domain` attribute, a high-entropy server-side session ID, and server-side storage. Require CSRF tokens or `Origin`/`Sec-Fetch-Site` validation for state-changing requests; `SameSite` alone is not sufficient.

See [password and email flows](password-flows.md) when implementing the non-OAuth paths.
