---
name: dsh-plugin
description: "Guide DeepSeek Harness plugin work that has a user-facing surface. Use when designing, implementing, or reviewing a DSH plugin panel, page, toolbar, list, or decoration, and route to the applicable UI/UX guidance."
---

# DSH Plugin Skills

## Purpose

This pack collects guidance for DeepSeek Harness (DSH) plugins, starting with the part
most likely to be judged immediately: the user interface. A plugin is not a standalone
app; it renders inside the Harness Web GUI and is judged against that shell.

## Choose the category

- [UI/UX](UI-UX/SKILL.md) for anything a person sees and operates: the native-design
  guideline, then panels, pages, toolbars, selectors, lists, rows, status,
  empty/loading/error states, and accessibility. Supporting recipes and the review log
  live in `UI-UX/references/`.

More categories can be added here as the pack grows; read only the applicable one.

## Global principles

- **Native by default.** Inherit the shell's frame, typography, color roles, density, and
  states instead of introducing a second design language. The operational rules live in
  the UI/UX guidance.
- **The Host owns privileged work.** Credentials, network reads, and file/process access
  stay on the Host half; the browser talks to it through the authenticated bridge and
  receives data, never secrets.
- **A plugin must activate.** A client half that loads but fails to activate is a broken
  plugin, even when the Host half is healthy; follow the activation rules in the UI/UX
  guidance.
- **Design and verification go together.** Every visual state you add is a state someone
  must verify; keep the checks reproducible rather than relying on one lucky screenshot.

## Routing

1. Decide whether the task has a user-facing surface. If not, this pack does not apply.
2. Read [UI/UX](UI-UX/SKILL.md) before designing or changing that surface.
3. Follow its links to concrete guidance and examples, resolving them relative to the
   file that contains them.
4. Before completion, run the native-design test described in the guidance.
