---
name: audit
description: "Guide mobile audit. Use when implementing or reviewing production readiness, security, reliability, testing, release configuration, and prioritized findings in mobile applications."
---

# Mobile Production Audit

Audit:
- onboarding and account lifecycle
- authentication
- API authorization
- secure token storage
- permissions
- deep links
- offline/retry behavior
- accessibility
- performance
- crash handling
- observability
- testing
- GitHub Actions CI/CD
- signing/release setup
- store-readiness
- privacy/consent

Repository sweep:
- TODO/FIXME
- debug menus and development-only flags
- hard-coded credentials and test keys
- placeholder or lorem-ipsum content
- localhost/dev API endpoints
- disabled certificate pinning or App Transport Security exceptions
- verbose production logging

Classify findings with these definitions:
- Critical: blocks release or is a security/privacy breach (store rejection, exposed credential, missing server-side authorization)
- High: breaks a critical workflow or compromises data integrity for a meaningful set of users
- Medium: degraded behavior, unhandled failure state, or accessibility barrier
- Low: polish, consistency, or minor performance issue

For each finding report: location, issue, impact, evidence, recommended fix.

Include privacy/consent and the data collected by analytics and crash SDKs.

Do not call the app release-ready while Critical findings remain.
