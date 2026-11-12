---
name: release
description: "Prepare and review mobile releases. Use for versioning, store metadata, privacy disclosures, rollout, backward compatibility, and hotfix planning."
---

# Mobile Release Management

Check:
- semantic/app version
- build number
- release notes
- privacy manifests/disclosures
- Play Data Safety and data-collection disclosures
- content rating and target SDK/API level compliance
- store metadata
- screenshots where required
- permission purpose strings
- crash-free metrics and a crash-free session target
- staged/phased rollout
- feature flags/kill switches
- backward compatibility with older backend versions
- minimum supported app version policy
- forced-update behavior only when justified

Rollout can be halted, not rolled back: a released iOS version cannot be reverted, and an Android `versionCode` must always increase. Recovery means halting the rollout, using a server-side kill switch or minimum-version gate, and shipping a new build; retain dSYMs and ProGuard/R8 mapping files for the broken version.

## Store submission gates
- Apple export compliance (`ITSAppUsesNonExemptEncryption`)
- Apple privacy manifest and Required Reason API declarations, including third-party SDK manifests
- App Tracking Transparency (`NSUserTrackingUsageDescription`) before any tracking
- privacy policy and support URLs, and current IAP vs external-purchase-link rules for digital goods
- current platform build requirements: Apple's minimum Xcode/SDK and Google's target API level change annually; verify each submission cycle

## Over-the-air updates
Apple guideline 3.3.2 permits JS-bundle over-the-air updates only for changes within the app's intended purpose; native capability changes cannot be shipped this way. Verify the current status of any OTA service before adopting it, and treat retired services as unavailable.
