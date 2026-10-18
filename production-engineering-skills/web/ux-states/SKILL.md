---
name: ux-states
description: "Implement and review web interaction states. Use for asynchronous data, loading and error handling, offline behavior, forms, validation, and retry flows."
---

# Web UX States

For each async/data-driven component consider:

- initial
- loading
- skeleton loading
- success
- empty
- no results
- partial failure
- stale data
- refreshing
- offline
- timeout
- unauthorized
- forbidden
- not found
- rate limited
- maintenance
- disabled/read-only
- pending/processing
- cancelled/expired
- retry

For forms include:
- client validation
- server validation
- field errors
- form errors
- duplicate-submit prevention
- submission progress
- input preservation after failure
- accessible error announcements
- success confirmation
- unsaved-changes handling where appropriate
