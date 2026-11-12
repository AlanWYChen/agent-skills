---
name: authentication
description: "Guide backend authentication. Use when implementing or reviewing sign-in, identity verification, session or token lifecycle, account recovery, and authorization boundaries in backend applications."
---

# Backend Authentication and Identity

The backend is the authoritative boundary for identity and authorization.

Support applicable mechanisms:
- session cookies
- JWT access tokens
- OAuth/OIDC
- Google identity
- Apple identity
- service-to-service auth
- API keys
- mTLS
- passkey/WebAuthn verification
- MFA

References:
- [references/google-identity.md](references/google-identity.md)
- [references/apple-identity.md](references/apple-identity.md)
- [references/oauth-oidc.md](references/oauth-oidc.md)
- [references/jwt.md](references/jwt.md)
- [references/api-keys.md](references/api-keys.md)
- [references/service-to-service.md](references/service-to-service.md)
- [references/webauthn.md](references/webauthn.md)
- [references/session-cookies.md](references/session-cookies.md)

## Credential handling
- hash passwords with Argon2id (or bcrypt with a tuned cost), never fast hashes, and check breached-password lists where feasible
- rotate refresh tokens on use, detect reuse, and revoke the token family on reuse
- store API keys as hashes and compare them in constant time
- provide MFA recovery codes and a step-up path for sensitive actions

## Account recovery
Use single-use hashed tokens with a short TTL, uniform responses to avoid account enumeration, reauthentication before email or authenticator changes, and revocation of all sessions and refresh tokens after recovery. Rate-limit recovery attempts.
