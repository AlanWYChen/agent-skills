# Secure Token Storage on Mobile

Use OS-provided secure storage:
- iOS: Keychain generic-password items with an accessibility class such as `kSecAttrAccessibleAfterFirstUnlockThisDeviceOnly` (device-only, never migrated or restored).
- Android: keep tokens out of Keystore, which stores keys rather than blobs. Hold an AES key in Keystore, use it to encrypt the token into DataStore/SharedPreferences, and exclude that file from Auto Backup (`android:allowBackup="false"` or `dataExtractionRules`). `androidx.security-crypto` is in maintenance mode; verify its current status before adopting it.

Keychain items survive app deletion on iOS. Delete them on first launch and on account switch, not only on explicit logout.

Avoid storing access/refresh tokens in:
- plaintext preferences
- SQLite without appropriate protection
- logs
- crash reports

Consider:
- token rotation
- refresh token revocation
- device compromise assumptions
- clearing credentials on logout
- biometric gating for especially sensitive local secrets
