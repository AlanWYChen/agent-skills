---
name: authentication
description: "Guide mobile authentication. Use when implementing or reviewing sign-in, identity verification, session or token lifecycle, account recovery, and authorization boundaries in mobile applications."
---

# Mobile Authentication

## Core flows

Consider:
- email/password
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

## References

- [references/google-sign-in.md](references/google-sign-in.md)
- [references/apple-sign-in.md](references/apple-sign-in.md)
- [references/oauth-pkce.md](references/oauth-pkce.md)
- [references/passkeys.md](references/passkeys.md)
- [references/secure-token-storage.md](references/secure-token-storage.md)

Mobile apps are public clients: do not embed OAuth client secrets in the app binary.
