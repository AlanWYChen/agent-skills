# Mobile UI / E2E Testing

Cover critical journeys:
- first launch/onboarding
- sign in
- sign out
- password/account recovery
- deep link into authenticated content
- offline/reconnect
- create/edit/delete critical resources
- subscription purchase/restore where applicable

Typical tools:
- XCUITest
- Espresso / UI Automator
- Maestro
- Detox
- Appium

Real devices are required for biometrics, push, camera, in-app purchase, and universal/app links. Grant system permissions programmatically (for example `GrantPermissionRule` or UiAutomator) because Espresso cannot click system dialogs; seed data through a mock backend (WireMock, MockWebServer) or dedicated test accounts, and quarantine flaky tests with a named owner.
