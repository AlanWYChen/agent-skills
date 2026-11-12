# Biometric Reauthentication on Mobile

Use LocalAuthentication on iOS or BiometricPrompt on Android for step-up authentication, not as the only factor.

- Bind the check to a protected operation; "biometrics are enabled" is not authorization.
- iOS: `kSecAccessControlBiometryCurrentSet` invalidates the item when the enrolled biometric set changes. Handle that invalidation and fall back according to product policy.
- Android: bind a Keystore key to biometric authentication with a `CryptoObject`, and handle lockout and `BIOMETRIC_ERROR_*` results.
- Provide a secure fallback (device passcode or account recovery); never fall through silently to a weaker check.
- Re-prompt for sensitive actions, and clear elevated state on backgrounding or timeout.
