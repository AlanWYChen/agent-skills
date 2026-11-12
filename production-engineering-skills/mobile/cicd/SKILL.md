---
name: cicd
description: "Configure and review mobile CI/CD pipelines on GitHub Actions. Use for pull-request validation, iOS/Android signing, build artifacts, store deployment, and release recovery."
---

# Mobile CI/CD with GitHub Actions

GitHub Actions is the default CI/CD runner.

## Pull requests

Typical jobs:
- checkout
- restore package/build caches
- lint/format
- compile
- unit tests
- integration tests
- static analysis
- dependency/security scan

## iOS

Use:
- macOS GitHub runners or approved self-hosted runners
- Fastlane or Xcode Cloud automation where the repository already uses it
- code signing via protected secrets / App Store Connect credentials
- archived build artifacts
- TestFlight deployment from protected branches/environments

Prefer App Store Connect API keys over interactive credentials.

## Android

Use:
- Gradle caching
- Gradle Play Publisher or Fastlane where the repository already uses it
- signing secrets through GitHub Environments/Secrets
- AAB/APK build artifacts
- Play Console internal/testing track deployment

## Release safety

- protected production environments
- manual approval where appropriate
- version/build number automation
- immutable build artifacts
- changelog/release notes
- recovery plan: halt rollout, server-side kill switch or minimum-version gate, and a new build with a new build number; mobile binaries cannot be rolled back

## Dependency update policy

When configuring or auditing Dependabot, use the shared [Dependabot policy](../../shared/dependabot-policy/SKILL.md). Keep its templates and merge rules in that shared skill rather than duplicating them here.
