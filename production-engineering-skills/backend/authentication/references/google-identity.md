# Verifying Google Identity on the Backend

When receiving a Google ID token:

Validate:
- cryptographic signature against Google's current keys
- issuer
- audience/client ID
- expiry
- nonce where the flow uses one

Use the provider subject (`sub`) as the stable Google identity key.

Do not trust:
- email alone
- client-side profile objects
- unsigned claims

Link accounts by `(iss, sub)`. Attach an existing local account only when the provider asserts a verified email (`email_verified === true`) and exactly one account matches; never merge automatically on an unverified or absent email.
