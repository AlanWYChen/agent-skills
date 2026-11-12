---
name: testing
description: "Guide web testing. Use when implementing or reviewing test selection, critical workflow coverage, and appropriate unit, integration, or end-to-end checks in web applications."
---

# Web Testing

Select the appropriate test layer instead of pushing everything into E2E:
- pure logic → unit
- component behavior and accessibility → component
- UI plus API/database boundaries → integration
- cross-page, browser-only, or navigation flows → E2E

References:
- [unit.md](unit.md)
- [component.md](component.md)
- [integration.md](integration.md)
- [e2e.md](e2e.md)
- [accessibility.md](accessibility.md)
- [visual.md](visual.md)

Mock at the network boundary (for example MSW) rather than at internal modules. Make time, randomness, and test data deterministic and isolated per test. Quarantine flaky tests with a named owner and a fix deadline; retries detect flakiness, they do not fix it. Every critical workflow must have integration and/or E2E coverage.
