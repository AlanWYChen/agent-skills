# Password and Email Flows (Web)

- Hash passwords with Argon2id (or bcrypt with a tuned cost), never with reversible encryption or unsalted hashes.
- Rate-limit and throttle login, reset, and verification attempts by account and by source; detect credential stuffing.
- Return uniform responses and timing for unknown accounts to resist enumeration.
- Reset and verification tokens: high entropy, hashed at rest, single-use, short TTL, invalidated on password or email change.
- Invalidate sessions on password change and support logout-all-sessions.
- Validate post-login `returnTo` and redirect targets against an allowlist; never redirect to an external URL.
- Bind `state` and the PKCE verifier to the pre-auth session in an `HttpOnly` cookie, not to a query parameter.
- Provide MFA recovery codes and a recovery path that does not bypass verification.
- Send transactional email through a provider with SPF, DKIM, and DMARC configured.
