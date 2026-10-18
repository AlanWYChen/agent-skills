---
name: authentication
description: "Guide web authentication. Use when implementing or reviewing sign-in, identity verification, session or token lifecycle, account recovery, and authorization boundaries in web applications."
---

# Web Authentication

Implement complete authentication flows rather than login UI only.

## Core flows

Consider:
- signup
- login
- logout
- email verification
- password reset
- change password
- change email
- reauthentication for sensitive actions
- session expiration and refresh
- active sessions
- logout-all-sessions
- MFA
- passkeys/WebAuthn
- account linking
- account deletion
- data export

## Authorization

Authorization must be enforced server-side for:
- routes
- APIs
- server actions
- files
- organizations
- resource ownership
- subscription entitlements

## References

Use the reference matching the provider or mechanism:
- [references/google-oauth.md](references/google-oauth.md)
- [references/apple-sign-in.md](references/apple-sign-in.md)
- [references/passkeys-webauthn.md](references/passkeys-webauthn.md)
- [references/oauth-pkce.md](references/oauth-pkce.md)
- [references/session-cookies.md](references/session-cookies.md)

Do not put OAuth client secrets in browser bundles.
