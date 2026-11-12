# Passkeys on Mobile

Use platform credential APIs:
- iOS AuthenticationServices
- Android Credential Manager / passkey APIs

Backend responsibilities:
- generate challenges
- verify WebAuthn/passkey assertions
- validate relying party/origin/app association: on iOS the `webcredentials` associated-domains entitlement plus an AASA `webcredentials` section served over HTTPS, and on Android `assetlinks.json` listing both the upload-key and Play App Signing SHA-256 fingerprints
- store credential public keys/IDs
- support recovery and device migration scenarios

Never verify passkey assertions only on-device.
