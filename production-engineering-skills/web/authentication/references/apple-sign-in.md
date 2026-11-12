# Sign in with Apple for Web

Use Apple's authorization flow through a server-controlled callback.

For web, `client_id` is the Apple Services ID, not the app bundle ID. The code exchange needs a server-generated `client_secret`: an ES256 JWT signed with the `.p8` key, with the Apple Team ID as `iss`, the Services ID as `sub`, `aud` set to `https://appleid.apple.com`, and `exp` at most six months ahead. Request `response_mode=form_post` whenever `name` or `email` scopes are requested. Keep the `.p8` key server-only, register the Return URL as HTTPS, and validate the ID token's `aud` (Services ID) and `nonce` claim.

## Typical flow

1. Generate state and nonce.
2. Redirect the user to Apple.
3. Receive the authorization response on the server.
4. Validate state and nonce.
5. Validate the Apple identity token:
   - signature
   - issuer
   - audience
   - expiry
6. Use the stable Apple subject identifier as the provider identity.
7. Create/link the local account.
8. Create the application's own session.

## Important details

- Apple may only provide the user's name the first time.
- Users may use Apple's private relay email.
- Do not use mutable email as the provider's primary identity key.
- Store the Apple `sub` value.
- Account linking must handle relay-email cases safely.
