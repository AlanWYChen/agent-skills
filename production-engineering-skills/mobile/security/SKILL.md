---
name: security
description: "Guide mobile security. Use when implementing or reviewing trust boundaries, authorization, input validation, secret handling, and application vulnerabilities in mobile applications."
---

# Mobile Security

Focus on client-device and API boundaries.

Check:
- server-side authorization
- secure token storage
- no embedded secrets
- certificate/TLS correctness with platform defaults enforced: ATS with no arbitrary loads outside justified domains, Android `usesCleartextTraffic="false"` plus a network security config, and debug-only exceptions
- certificate pinning only with backup pins and a rotation plan, or an explicit decision not to pin
- deep-link validation, including exported components and intent parameters
- WebView hardening
- file/share intent validation
- clipboard sensitivity
- screenshot/screen recording policy per platform (Android `FLAG_SECURE`; iOS cannot block screenshots, only hide content when backgrounding and observe recording)
- local database protection
- backup/restore exposure of sensitive data (Android backup rules, iOS file protection)
- overlay/tapjacking protection for sensitive actions where the platform supports it
- log redaction
- jailbreak/root assumptions where relevant
- push notification payload sensitivity
- biometric reauthentication for sensitive actions
- dependency vulnerabilities
- app integrity attestation (App Attest/DeviceCheck on iOS, Play Integrity) enforced server-side where abuse risk is high

Do not assume app-store distribution makes secrets private.
Anything in the binary should be considered recoverable by an attacker.
