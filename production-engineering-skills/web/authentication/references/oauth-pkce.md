# OAuth 2.0 Authorization Code + PKCE

Use PKCE for every authorization-code client, including confidential server clients (current OAuth security guidance, RFC 9700 / OAuth 2.1). Never use `plain`.

- Generate a high-entropy `code_verifier`.
- Derive `code_challenge`.
- Use `S256`.
- Generate and validate `state`.
- Use nonce for OIDC identity flows where applicable.
- Validate the ID token signature, issuer, audience, expiry, and nonce before trusting its claims.
- Exchange the authorization code only at the trusted callback boundary.
- Validate redirect URI exactly.
- Request minimum scopes.
- Treat access and refresh tokens as secrets.
- Rotate/refresh tokens securely.
- Handle revoked credentials.
