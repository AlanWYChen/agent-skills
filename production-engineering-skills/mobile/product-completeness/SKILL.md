---
name: product-completeness
description: "Guide mobile product completeness. Use when implementing or reviewing complete product workflows, account lifecycle, navigation, error states, and applicable settings in mobile applications."
---

# Mobile Product Completeness

Check:
- onboarding
- login/signup
- logout
- account settings
- permissions education
- push notification settings
- deep links
- universal links/app links
- offline behavior
- background/foreground transitions
- error/retry states
- empty states
- app-update handling
- account deletion
- privacy controls
- subscription restore
- accessibility
- tablet/large-screen behavior if supported
- orientation behavior
- safe areas/notches
- keyboard handling
- localization/RTL and locale-specific formatting
- subscription purchase, restore, and server-side receipt validation (App Store Server API, Play Developer API)

## Deep links
- iOS: associated-domains entitlement plus an AASA `applinks` file served over HTTPS with the correct content type; verify on a real device.
- Android: `autoVerify` intent filters plus `assetlinks.json` containing the Play App Signing certificate SHA-256.
- Treat every link parameter as attacker-controlled: allowlist scheme/host/path, never carry access tokens in links, and require sign-in before authenticated routes while queueing the link until after sign-in.
