# Sign in with Apple for Mobile

App Store Guideline 4.8 requires an equivalent privacy-respecting login option when the app offers third-party login such as Google; Sign in with Apple conventionally satisfies it. When users delete their accounts, revoke the Apple tokens through the REST `/auth/revoke` endpoint: the client secret is an ES256 JWT signed with the `.p8` key, valid for at most six months, with the bundle ID as audience.

Use AuthenticationServices on Apple platforms where applicable.

## Flow

- request authorization
- use nonce when integrating with backend identity providers
- send the identity token/authorization result to the backend
- backend validates signature, issuer, audience, expiry, and nonce
- use Apple subject identifier as stable provider identity
- create the application's own backend session/tokens

Remember:
- name may only be supplied on first authorization
- private relay email may be used
- email should not be treated as the stable Apple identity key
