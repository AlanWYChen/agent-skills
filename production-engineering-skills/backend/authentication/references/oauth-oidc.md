# OAuth / OIDC Backend Guidance

For Authorization Code flows:
- bind `state` to the user's session (server-side or in a `__Host-` cookie), compare exactly, and make it single-use with a short TTL
- validate nonce for OIDC where applicable
- exchange codes over trusted server boundaries
- register exact redirect URIs and reject everything else
- require PKCE S256 for public clients
- validate ID tokens with a library: exact issuer, audience, `exp`/`iat` with small skew, and matching `nonce`
- request minimal scopes
- encrypt refresh tokens at rest
- rotate credentials
- handle revocation
- support provider outage/error cases

Do not confuse authentication with authorization.
