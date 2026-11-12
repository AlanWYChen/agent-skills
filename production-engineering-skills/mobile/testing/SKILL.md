---
name: testing
description: "Guide mobile testing. Use when implementing or reviewing test selection, critical workflow coverage, and appropriate unit, integration, or end-to-end checks in mobile applications."
---

# Mobile Testing

References:
- [unit.md](unit.md)
- [integration.md](integration.md)
- [ui-e2e.md](ui-e2e.md)
- [device-compatibility.md](device-compatibility.md)
- [accessibility.md](accessibility.md)

Use the cheapest reliable layer that catches the failure.

Define the support matrix explicitly (minimum and current OS, small and large phone, tablet if supported). Hardware-backed flows — biometrics, push, camera, in-app purchase, universal/app links — need real devices; simulators and emulators cannot validate them.
