---
name: accessibility
description: "Guide mobile accessibility. Use when implementing or reviewing accessibility semantics, assistive technologies, focus, contrast, motion, and input behavior in mobile applications."
---

# Mobile Accessibility

Target WCAG 2.2 AA plus platform minimums: 44×44 pt touch targets on iOS, 48×48 dp on Android, 4.5:1 text contrast and 3:1 for large text and non-text indicators.

Check:
- VoiceOver/TalkBack labels
- accessibility traits/roles
- dynamic type / font scaling
- color contrast
- non-color cues
- reduced motion
- switch control / keyboard where relevant
- logical focus order
- accessible custom controls
- touch target size
- semantic grouping
- announcements for async state changes
- orientation/large text behavior

Verify with iOS `performAccessibilityAudit()` and Accessibility Inspector, Android Accessibility Scanner and Espresso `AccessibilityChecks`, and manual VoiceOver/TalkBack passes on critical flows.
