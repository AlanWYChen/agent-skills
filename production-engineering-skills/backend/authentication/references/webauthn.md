# WebAuthn Verification on the Backend

Registration:
- issue single-use challenge
- verify RP ID/origin
- verify `clientDataJSON.type` (`webauthn.create`/`webauthn.get`), the single-use server-side challenge (at least 16 bytes, short TTL), the exact origin, and `rpIdHash == SHA-256(rpId)`; default to `attestation: "none"`
- store credential ID and public key

Authentication:
- issue single-use challenge
- verify RP ID/origin
- validate signature and credential
- store signCount and flag decreases; do not reject zero-count synced passkeys
- check the UP/UV flags according to policy
- establish the application session/token after successful verification

Recovery must be designed separately.
