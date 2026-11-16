---
name: dsh-plugin-ui-ux
description: The operational meaning of "follow DSH's native design" for plugin UI — inherit the shell instead of rebuilding it, use the page grammar (toolbar + filling body + bounded lists), hierarchy from semantic tokens rather than colors, host control sizes and spacing rhythm, selectors that name what they select, intentional loading/empty/error/stale states, and a native-design acceptance test to run before shipping.
whenToUse: When designing or reviewing any page, panel, toolbar, list, row, pill, selector, empty state, loading state, or decoration in the DSH Web UI, and when a screenshot suggests the result "doesn't look like DSH".
---

# DSH plugin UI/UX

This is the UI/UX guidance for DeepSeek Harness plugins: what a native DSH surface
means in practice, and the acceptance test for it.

**Native means additive, not adjacent.** A plugin that follows DSH's design reads as a
capability the shell always had: same frame, same typography, same color roles, same
density, same states. It does not bring its own chrome, palette, type scale, or
interaction metaphor. When in doubt, copy the nearest host surface's grammar rather than
inventing a better-looking one.

Treat the rules below as defaults with reasons, not a pixel spec. Numbers are anchors;
the reason is what you apply to a case the numbers don't cover.

## 1. Inherit the shell

- No app shell of your own: no title bar, brand mark, navigation tabs, or back button.
  Your panel *is content* inside the shell's main area.
- No second palette, font, icon set, or motion language.
- No modal for an ordinary flow. Inline surfaces and banners first; overlays only for
  global or transient notices.
- No second scrollbar: one scroll region per independently scrolling concept.
- Theme tokens, not colors. If a token you want does not exist, the design is wrong
  before the variable is.

## 2. Page grammar

A full panel has three parts and nothing else:

1. **Toolbar** — the page title, the scope selector (what this page is about), and the
   few actions that apply to the whole page.
2. **Context line** (optional) — a secondary identity or environment shown as a link or
   quiet badge, never as a competing selector.
3. **Body** — the content, which fills the remaining height.

- The body owns the height (flex chain), so data regions scroll inside it and the page
  itself does not grow with data.
- Region headings stay visible while their region scrolls (sticky within the region, not
  floating over the shell).
- Compose in regions: a heading, then either a bounded list or an intentional empty/
  loading/error state. Do not alternate many small widgets.

## 3. Hierarchy through roles

- **Text**: one primary role for values and titles, one secondary for metadata and
  labels, one tertiary/dimmed for de-emphasis. Size carries scale, weight carries
  emphasis; do not use both plus color for the same jump.
- **Surfaces**: page background is the base; raised rows/cards use the next layer;
  sunken or inset areas the layer after that. Elevation is a 1px border and a subtle
  background step — not shadows, blur, gradients, or glass.
- **Brand color** belongs to the primary action and genuine accent. **State colors**
  belong to state. A failed run is not "brand red", it is the error/warn role.
- Separators are borders, not extra containers. Prefer whitespace over another card.
- Status must survive grayscale: text plus a tokenized pill, not a colored dot alone.

## 4. Density and rhythm

- Space on a small grid: close elements inside a group, a clear step between groups,
  a larger step between regions and around the page.
- Controls share one height and one radius; icon-only controls are square and at least
  comfortably clickable; pills are fully rounded.
- A data row is compact: identity, a little metadata, status. If a row needs two lines,
  something belongs in a detail view instead.
- **Alignment is the quality signal.** Things that read as a column must share a content
  box; the same control looks the same in every view. Most "it looks off" reports are
  one inconsistent inset or two different templates.

## 5. Controls

- Prefer native form controls, styled by the host's tokens, over custom widgets. A
  native select with a real `aria-label` beats a handmade menu and looks native by
  construction.
- A select is sized for its longest realistic option, not its current one; long values
  ellipsize rather than widen the page.
- One filled/primary action per view. Everything else is bordered or quiet; destructive
  actions take the error role and a confirmation step proportional to the risk.
- Links go to the source of truth (open the underlying record) and external ones say so
  with an icon plus a new tab. A button-like link may be styled as a bordered control, but
  must stay keyboard-focusable and centered like its neighbors.
- Toolbar controls share one vertical center; icon glyphs are block-level so they do not
  sit on a text baseline.
- Do not invent toggles, steppers, or segmented controls unless you are composing an
  existing host primitive; if you must, match its size, radius, hover, and focus ring.

## 6. Selection and identity

- A selector names **the thing being selected** (project, session, filter) in the user's
  words — never a derived attribute of the current selection.
- Secondary identity (repository, branch, environment) is a separate affordance next to
  the selector: a link, a badge, a quiet button. Do not overload the selector's label.
- Remember the user's selection across reloads when the choice is durable; validate it
  against the live list and fall back deliberately, never silently.
- If the page can span scopes, state the scope once, clearly, and keep it in one place.

## 7. Data display

- Homogeneous collections are **rows**, not a grid of cards. One line per record:
  identity left, descriptive metadata next, status and time on the right.
- Column headers are optional; use them when metadata would otherwise be ambiguous.
  They are quieter than the data and must align with it exactly.
- Status is a short label in a fixed slot so the column reads as one edge. Relative time
  for recency, absolute time available on hover or in the link target.
- The row is the affordance: hover and focus states, and activation opens the
  authoritative page. Details, logs, and editing belong to that page until they earn a
  dedicated surface here.
- Truncate, don't wrap, secondary metadata; wrapping breaks scanability and row rhythm.

## 8. States are part of the design

Every data surface has more than one look, and each is designed:

- **Cold loading** — when there is nothing to show yet, one quiet status line or
  skeleton in the content area. Never a spinner over stale data.
- **Warm refresh** — cached content stays; refresh happens without a layout jump or a
  blocking indicator.
- **Empty (first time)** — says what this surface would show and what to do next, in a
  sentence or two, centered and aligned with the content it replaces.
- **Empty (after filter/scope)** — distinguishes "nothing matches" from "nothing exists".
- **Error** — inline, near the cause, actionable, and keeps whatever content is still
  valid. No error dialog for a failed read.
- **Stale/partial** — a subdued warning line above the retained content; never hide the
  content to show the warning.
- **Live** — a subtle pulse on genuinely live status, and it respects reduced motion.

## 9. Language and tone

Short, declarative, sentence case. Actions are verbs ("Refresh", "Sign out"), labels are
nouns ("Status", "Recent"), and messages explain the consequence rather than the
mechanism. No exclamation marks, no marketing, no invented product voice. Every visible
string comes from the host locale system, with locales kept key-identical so a missing
translation fails loudly in review rather than silently in one language.

## 10. Keyboard, focus, and accessibility

Everything reachable and operable by keyboard, with the host focus ring. Scrollable
regions are focusable and labeled. Rows activate on Enter/Space. Status changes use a
polite live region. Icons are either labeled controls or hidden decoration. Nothing
relies on color alone, and every token pair is checked in both themes.

## 11. When DSH has no pattern for it

Compose from what exists before inventing: a bordered control, a tokenized pill, a
quiet link, a disclosure, a settings row. If a genuinely new pattern is unavoidable, it
must read as a variation of an existing one — same height, radii, spacing, focus ring,
state colors — and stay inside your class prefix. A plugin-specific pattern that looks
like it belongs upstream is a design bug; propose it upstream instead.

## 12. The native-design test

Run this before shipping, and again after every screenshot round:

- **Squint** — can you tell it is the same product? If your section has a different
  density, palette, or chrome, it is not native yet.
- **Alignment** — pick three elements that read as a column and measure their content
  boxes. They must match; a shared grid template is not enough.
- **Density** — compare your row height, control height, and page padding with the
  nearest host page. Off by more than one step means either too airy or too cramped.
- **Token** — every color, radius, and type size resolves from the host tokens; zero
  literal colors; every token name actually exists in the running theme.
- **State** — open it with no data, with stale data, with a failing read, with an
  in-flight read, and with a long list. Each must look intentional.
- **Keyboard** — tab through the page: focus order, focus visibility, row activation,
  and scrollable regions all work without a mouse.
- **Language** — one tone, sentence case, no lorem, all strings localized.
- **Refresh** — a client bundle change only appears after a page refresh; verify the
  installed artifact, not the source you just edited.

## 13. Drift signals

If you see any of these, the design has stopped being native — fix the structure, not
the shading:

- a custom header bar, brand row, or navigation inside the content area;
- every row wrapped in its own card, or cards inside cards;
- three different control heights, radii, or paddings on one toolbar;
- literal hex colors, or token names that don't exist in the running theme;
- status pills sized by their text, so the column edge is ragged;
- two selectors for the same scope, or a selector labelled by a derived value;
- a data list that grows the page, or two nested scrollbars;
- empty text or an icon aligned to the border instead of the content;
- a loading spinner over data that is already displayed, or `null` rendered as "error";
- duplicate layout templates for two row kinds (they will drift apart on the next edit).

## References

- `references/layout-recipes.md` — one concrete CSS skeleton that satisfies this guide
  (page grammar, rows, header, pills, empty/loading, toolbar controls, cache shape).
- `references/polish-log.md` — the real review trail from one shipped panel: every
  symptom, root cause, fix, and the guideline it became. Useful as evidence, not as spec.
- For generic web interaction-state guidance beyond DSH (async data, validation, retry
  flows), see [web UX states](../../production-engineering-skills/web/ux-states/SKILL.md).
