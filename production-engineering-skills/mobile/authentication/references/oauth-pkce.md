# OAuth/OIDC + PKCE for Mobile

Use Authorization Code + PKCE.

- launch the system browser / secure auth session
- do not use embedded webviews for sensitive OAuth login unless provider explicitly supports it
- generate state and PKCE verifier/challenge
- use `S256`
- validate redirect/deep-link callback
- validate state
- exchange code securely
- validate the ID token or access token on the backend, not only in the app
- request minimal scopes
- handle token expiration and revocation
