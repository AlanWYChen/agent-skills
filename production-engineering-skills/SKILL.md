---
name: production-engineering-skills
description: "Guide production application development across web, mobile, and backend systems. Use when implementing or auditing production workflows; route to the applicable domain and supporting guidance."
---

# Production Engineering Skills

## Purpose

This is a domain-routed skill pack for production application development.

Choose the relevant domain first:

- [Web guidance](web/SKILL.md) for browser-based applications and websites
- [Mobile guidance](mobile/SKILL.md) for iOS, Android, and cross-platform mobile apps
- [Backend guidance](backend/SKILL.md) for APIs, services, workers, queues, data services, and platform systems

Each domain intentionally duplicates important concerns such as:
- security
- observability
- testing
- CI/CD
- authentication

The duplicated versions are customized for the domain rather than treated as generic advice.

## Shared repository workflows

- [Dependabot policy](shared/dependabot-policy/SKILL.md): use when configuring or auditing dependency update schedules, official GitHub Actions auto-merge, and manual review for application dependencies. This policy is shared across domains; read it only when the task concerns Dependabot.

## Routing

When working on a task:

1. Identify whether the task is primarily web, mobile, backend, or multi-domain.
2. Read that domain's linked `SKILL.md`.
3. Read only the applicable supporting skills using its relative links. Resolve each link relative to the file containing it, without relying on automatic discovery of nested skills.
4. Before completion, run the domain-specific production audit.
5. For cross-domain systems, run the audit for every affected domain.

## Global Principles

- Build complete workflows, not happy-path demos.
- Never treat frontend/mobile UI checks as authoritative authorization.
- Validate untrusted input at runtime.
- Do not expose secrets to clients.
- Prefer observability and recoverability over silent failure.
- Use GitHub Actions as the default CI/CD implementation unless the repository already uses another system.
- Test critical workflows at the appropriate layer instead of overusing one test type.
