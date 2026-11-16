# Polish log — GitHub Actions panel, v1 → v1.5

Chronological record of every UI/UX defect found while shipping one DSH plugin panel,
with the symptom the user saw, the root cause, the fix, and how it was verified. Keep
this as the concrete evidence behind the rules in `../SKILL.md`.

## Round 0 — "Failed to load plugins"

**Symptom:** the page showed `Failed to load plugins / @local/dsh-github-actions / web
boot: 1 entry did not activate`, and the plugin could not be used. No console details.

**Root cause:** the client module factory returned `{ apply, ... }` but no `inject`. The
page loader mounted the module with an empty dependency set; `apply` then read
`ctx.locale`/`ctx.connection` before those services were resolvable and threw, so the
entry was marked failed. The Host half was fine (Config row `schema`), which made it look
like an installation problem.

**Fix:** export `inject = ['slots', 'locale', 'connection']` from the factory and return
it. `apply` stays synchronous.

**Verification:** loader-shaped `vm` load asserted `Object.keys(module)` contains
`inject`; reinstalled and reloaded; the panel registered.

## Round 0b — plugin row `unsupported`, activation `TypeError`

**Symptom:** `application: failed`, diagnostic `TypeError: Cannot read properties of
undefined (reading 'validate')`; the plugin's config row showed `status: "unsupported"`.

**Root cause:** `Config` was a hand-written function with a `.parse` shim, not a native
Schemastery schema. Cordis validates with `Config['~standard'].validate(config)`, and the
DSH config inspector only accepts schemas carrying `Symbol.for('schemastery')`, `type`,
and `meta`.

**Fix:** `export const Config = s.object({ ... })` (real instance). The instance is
callable, keeps `~standard`, and satisfies the inspector; attach `.parse` non-enumerably
only for test compatibility.

**Verification:** `Reflect.get(Config, Symbol.for('schemastery')) === true`,
`Config['~standard'].validate({})` returns defaults; Config row `schema`.

## Round 0c — mostly unstyled panel

**Symptom:** a panel rendered with no borders, transparent backgrounds, a colorless
primary button.

**Root cause:** 13 of the 14 `--dsw-alias-*` variables used did not exist in the running
theme. `var(--undefined)` invalidates the whole declaration at computed-value time, so
`color` fell back to inherit and backgrounds/borders vanished.

**Fix:** remapped to real tokens (`label-primary`, `label-secondary`,
`label-primary-inverted`, `border-l2`, `bg-layer-1/2`, `interactive-bg-hover`,
`state-success-*`, `state-warn-*`, `button-primary-fill/hover`).

**Verification:** a script diffed every `var(--dsw-alias-*)` in the plugin against the
installed theme file → `used 16 missing []`; zero literal hex/rgb/hsl.

## Round 1 — pills, alignment, scrolling, empty state

**Symptom (screenshot):** Success and Failed pills had different widths; the middle
workflow column ("CI") started at different x positions; the long list grew the page
instead of scrolling; "No runs are currently running." hugged the left border.

**Root causes and fixes:**

| Issue | Root cause | Fix |
| --- | --- | --- |
| Pill widths | Pills sized by text; the status column was `max-content` | Fixed status track (132px), one `.pill` class with `min-width`, `justify-content/self:center`, `nowrap` |
| Middle column shift | Running used a 5-column template and Recent a 6-column one; both had `max-content` branch/event | One shared six-column template for both row kinds and the header; fixed px data columns; always render all six cells |
| No scrolling | Sections were content-height; only one scroll rule existed | Per-section `.scroll` containers with `overflow-y:auto`, bounded height, `tabIndex=0`, localized `aria-label`; sticky headings |
| Empty state | The line sat at the scroll edge | Wrapper with list padding + line with row padding; later `text-align:center` |
| Header row | No column headers | Non-interactive header per list on the same template (`aria-hidden`) |

**Verification:** a new frozen `test/layout.test.js` (6 tests) authored and RED-validated
before implementation; CSS assertions bound to rendered class names; independent
verifier confirmed one shared template occurrence and no `max-content` in row columns.

## Round 2 — theme-token audit, locale parity, state polish

**Symptom (verifier findings):** 13/14 theme tokens undefined (see Round 0c — this was
caught here in a second pass); an inline dictionary string differed from `locale/en.json`;
the panel was expected to look unstyled in warning/success areas.

**Fixes:** token remap; inline dictionaries made identical to `locale/*.json` (key and
value parity); `box-sizing` added where content-box sizing would overflow.

**Verification:** theme diff `used 16 missing []`; locale parity 55/55 → later 66/66,
74/74, 75/75, 76/76 at each increment; zero literal colors.

## Round 3 — fill the height, header geometry, empty alignment

**Symptom (screenshot):** Recent sat in a fixed-height box instead of using the rest of
the panel; the empty line was left-aligned while rows started further right; the header
labels were ~14px left of the data they label.

**Root causes:**
- Only a base `max-height:52vh` scroll rule; no flex growth for the Recent section.
- The empty line was outside the list's horizontal inset (14px vs 28px).
- The header lived outside `.list`, so its content box was `W−28` while a row's was
  `W−56`; the shared `1fr` absorbed the difference and put the fixed columns 14px apart.
  The page also used `height:100%` + 20px padding without `border-box`, so the border box
  exceeded the host by 40px.

**Fixes:** full flex height chain (`page → body → sections`, `flex:1;min-height:0`);
Recent scroller `flex:1;max-height:none`, Running capped at 40vh; empty wrapper 14 + line
14 = 28px then centered; `.gha-header{padding:6px 28px}` (= list + row); `box-sizing:
border-box` on page and scrollers.

**Verification:** content-box math (`W=1000`: both Name x=28, Workflow x=306, right edge
972); a user-approved frozen-test revision changed the header padding expectation from
14px to 28px, with the approval and diff recorded in the manifest.

## Round 4 — remembered workspace, repo control, spacing

**Symptom (screenshot + feedback):** the panel forgot the selected project; the dropdown
was too narrow; the Git-icon sat slightly high; Running and Recent were fused; the
dropdown showed the repo name instead of the project name.

**Fixes:**
- Guarded `localStorage` (`github-actions.workspace`): restore only if the id is still in
  the live list; write once per change; storage errors swallowed.
- Dropdown becomes a project selector with host sizing
  (`min-width:240px; max-width:360px; width:auto; height:32px; ellipsis`).
- Repo identity moves to its own button-like `inline-flex` link (slug + 16px icon,
  32px, `align-items:center`, icon `display:block`).
- Toolbar `align-items:center`; `.sections` `gap:16px`; empty line `text-align:center`.

**Process note:** two frozen v1.3 assertions pinned the dropdown to the repo slug. The
user's explicit feedback ("the dropdown always be the project name") was recorded as the
approval, the test author applied a two-line revision, and the manifest recorded the
change with an integrity proof.

## Round 5 — cache, loading, and instant switching

**Symptom:** switching project/repo re-fetched from GitHub with a blank wait and no
feedback; a cold panel collapsed into the error surface.

**Fixes:**
- Session `Map<workspaceId, snapshot>` cache; only successful values; ≤20 entries;
  render cached rows immediately (no loading) and refresh in the background without
  `refresh:true`; failed refresh keeps rows + banner and is never cached.
- Dedicated `loading` state (one centered `role="status"`/`aria-live="polite"` line),
  shown only on cache miss; `describeState(null)` stays the error surface.
- Per-workspace request tokens so out-of-order responses cannot overwrite newer data or
  banner over it.
- Cache later hoisted from the component `useRef` to module/factory scope so switching
  panels away and back does not drop it; still not persisted, still bounded.

**Verification:** `test/ux2.test.js` (7 tests: cache hit, failed refresh, never-cache,
20-entry bound, loading, toolbar, spacing/locale) and `test/ux3.test.js` (2 tests:
remount cache, same-workspace ordering), each authored and RED-validated before
implementation; verifier drove the client module with deferred per-workspace RPC.

## Cross-cutting lessons

1. **Structure first.** Four of the biggest defects were wiring: missing `inject`,
   non-native `Config`, nonexistent tokens, and component-scoped state. No amount of CSS
   review finds those.
2. **Declarations are not geometry.** The header and rows shared an identical template
   and still misaligned by 14px; only content-box math caught it.
3. **One rule per concept.** Two row kinds with two templates is how the middle column
   drifted; one shared rule for rows + header fixed it and stayed fixed.
4. **States are part of design.** Empty, loading, stale, error, and cache-miss each need
   an intentional rendering; `null` collapsing to "error" is a common bug.
5. **Screenshots are the acceptance test for spacing.** Each user screenshot produced one
   measurable hypothesis; each fix was a class-level change plus a frozen assertion.
6. **TDD keeps polish from regressing.** Every round added a frozen test; later rounds
   re-ran all earlier ones, so a new flex box could not silently undo an old alignment.
