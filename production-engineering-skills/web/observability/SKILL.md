---
name: observability
description: "Guide web observability. Use when implementing or reviewing logs, metrics, failures, correlation, alerts, and sensitive data redaction in web applications."
---

# Web Observability

## Frontend

Capture:
- runtime exceptions
- unhandled promise rejections
- failed API requests
- route/page failures
- Web Vitals
- release version
- environment

## Server/API

Use:
- structured logs
- request IDs
- correlation IDs
- latency/error metrics
- tracing for cross-service flows

Never log:
- passwords
- auth tokens
- private keys
- unnecessary sensitive personal data

Upload source maps for the exact release and tag errors with the release version; sample traces and logs deliberately; scrub PII before sending; collect Web Vitals attribution through RUM; alert on SLO burn rather than raw thresholds, and distinguish user errors from system failures.
