# Verifying Apple Identity on the Backend

Validate:
- token signature using Apple's published keys
- issuer
- audience
- expiry
- nonce where applicable

Use Apple `sub` as the stable provider identity.

Account linking must account for:
- private relay emails
- email changes
- multiple login methods

Link accounts by `(iss, sub)`. Attach an existing local account only when exactly one account matches a verified email; Apple's relay email, and an email absent after first authorization, are display-only and never the identity key.
