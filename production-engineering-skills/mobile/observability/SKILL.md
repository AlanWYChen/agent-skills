---
name: observability
description: "Guide mobile observability. Use when implementing or reviewing logs, metrics, failures, correlation, alerts, and sensitive data redaction in mobile applications."
---

# Mobile Observability

Capture:
- crashes
- non-fatal exceptions
- ANRs / hangs
- app startup performance
- network failures
- release/build number
- OS version
- device class
- app state transitions when useful
- iOS hangs and watchdog terminations (MetricKit `MXHangDiagnostic`) alongside Android ANRs

Upload symbols and verify a release build deobfuscates: dSYMs, ProGuard/R8 `mapping.txt`, NDK symbols, and Hermes or Flutter source maps. Track crash-free sessions/users, alert on crash-rate regressions, and gate crash/analytics SDK initialization on consent where required.

Use correlation IDs to connect mobile requests to backend traces.

Never record:
- passwords
- raw tokens
- private keys
- sensitive form contents
- unnecessary personal data

Separate analytics from operational telemetry.
