---
name: authentication
description: "Guide mobile authentication. Use when implementing or reviewing sign-in, identity verification, session or token lifecycle, account recovery, and authorization boundaries in mobile applications."
---

# Mobile Authentication

## Core flows

Consider:
- email/password with verification
- password reset, change password, and change email
- active sessions
- data export
- Google sign-in
- Sign in with Apple
- passkeys
- OAuth/OIDC
- MFA
- biometric reauthentication
- secure token refresh
- logout
- logout all sessions
- account linking
- account deletion

## Account deletion

In-app deletion is required where the app offers account creation (App Store 5.1.1(v)), and a web deletion route must be declared in Play Data Safety. Reauthenticate, revoke sessions and refresh tokens (including Sign in with Apple tokens), delete server-side data, and clear Keychain items, local databases, and caches.

## References

- [references/google-sign-in.md](references/google-sign-in.md)
- [references/apple-sign-in.md](references/apple-sign-in.md)
- [references/oauth-pkce.md](references/oauth-pkce.md)
- [references/passkeys.md](references/passkeys.md)
- [references/secure-token-storage.md](references/secure-token-storage.md)
- [references/biometrics.md](references/biometrics.md)

Mobile apps are public clients: do not embed OAuth client secrets in the app binary.
