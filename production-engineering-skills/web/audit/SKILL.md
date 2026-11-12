---
name: audit
description: "Audit web production readiness. Use when reviewing completeness, security, accessibility, performance, observability, testing, and release configuration, and when producing severity-ranked findings."
---

# Web Production Audit

Audit:
- product completeness
- UX states
- forms
- authentication
- authorization
- privacy/consent
- accessibility
- security
- SEO
- performance
- observability
- testing
- CI/CD (GitHub Actions or the existing system)
- deployment configuration

Repository sweep:
- TODO
- FIXME
- debugger
- console.log
- localhost
- example.com
- lorem ipsum
- href="#"
- mock data
- hard-coded credentials
- public secrets
- `.env*` files, client-exposed prefixes, and public source maps

Scope the sweep to application source and exclude `node_modules`, build output, coverage, test fixtures, and lockfiles; intentional server-side logging is not a finding.

Classify findings:
- Critical: blocks release or is a security/privacy breach
- High: breaks a critical workflow or exposes data
- Medium: degraded behavior or accessibility barrier
- Low: polish or minor performance issue

For each finding report: location, issue, impact, evidence, and recommended fix.

Do not call the app production-ready while Critical findings remain.
