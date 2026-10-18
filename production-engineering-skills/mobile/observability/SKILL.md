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

Use correlation IDs to connect mobile requests to backend traces.

Never record:
- passwords
- raw tokens
- private keys
- sensitive form contents
- unnecessary personal data

Separate analytics from operational telemetry.
