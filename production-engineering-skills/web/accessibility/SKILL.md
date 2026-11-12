---
name: accessibility
description: "Guide web accessibility. Use when implementing or reviewing accessibility semantics, assistive technologies, focus, contrast, motion, and input behavior in web applications."
---

# Web Accessibility

Target WCAG 2.2 AA and document any exception explicitly instead of leaving it implicit.

Check:
- semantic HTML
- logical headings
- keyboard operation
- visible focus
- proper labels
- accessible dialogs
- focus trapping/restoration
- aria-live for dynamic updates when needed
- color contrast
- non-color cues
- reduced-motion preference
- touch target size
- zoom/text resizing
- alt text
- captions/transcripts
- skip-to-content
- table semantics
- screen-reader sanity checks
- text contrast 4.5:1 and non-text/large-text contrast 3:1
- 24×24 CSS px minimum target size (WCAG 2.5.8)
- 200% zoom and 320 px reflow without loss
- route-change focus management and document-title updates in SPAs
- `<html lang>` and landmarks on every page
- alternatives for dragging (2.5.7), no redundant entry (3.3.7), and accessible authentication (3.3.8)

Prefer native HTML elements over custom ARIA widgets.
