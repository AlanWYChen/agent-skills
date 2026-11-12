# Google Sign-In for Mobile

Use platform-supported Google Sign-In / OAuth SDKs.

## Principles

- Treat the app as a public client.
- Use PKCE for authorization code flows.
- Validate identity tokens on the backend when establishing a server session.
- Verify issuer, audience, expiry, and nonce where applicable.
- Do not trust a client-supplied Google profile as proof of identity.
- Keep server API authorization independent from UI login state.
- Handle cancelled sign-in and revoked Google access cleanly.

## Client configuration

- Android OAuth clients are bound to package name and signing-certificate SHA-1. Register both the upload key and the Play App Signing certificate, or sign-in fails once Play signs the build.
- iOS requires the reversed client ID URL scheme in the app configuration.
- Prefer current Google Identity Services on iOS and Credential Manager on Android over the legacy GoogleSignIn SDK; verify current guidance before choosing a library.
