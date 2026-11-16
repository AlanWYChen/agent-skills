# Layout recipes — copy-ready patterns for DSH plugin panels

These are the shapes that survived real screenshot review. Replace `my-` prefixes and
token names only with verified equivalents.

## 1. Page → body → sections (fills the host, no page scroll)

```css
.my-page{box-sizing:border-box;display:flex;flex-direction:column;height:100%;min-height:0;gap:16px;padding:20px;color:var(--dsw-alias-label-primary)}
.my-toolbar{display:flex;align-items:center;justify-content:space-between;gap:16px;flex-wrap:wrap}
.my-toolbar-main{display:flex;align-items:center;gap:12px;flex-wrap:wrap;min-width:0}
.my-body{display:flex;flex-direction:column;flex:1;min-height:0}
.my-sections{display:flex;flex-direction:column;flex:1;min-height:0;gap:16px}
.my-section{display:flex;flex-direction:column;min-height:0}
.my-section--grow{flex:1;min-height:0}
.my-scroll{box-sizing:border-box;overflow-y:auto;max-height:min(40vh, 560px);
  scrollbar-width:thin;scrollbar-color:var(--dsw-alias-border-l2) var(--dsw-alias-bg-layer-1);
  border:1px solid var(--dsw-alias-border-l2);border-radius:12px;background:var(--dsw-alias-bg-layer-1);padding:0 0 10px}
.my-section--grow .my-scroll{flex:1;min-height:0;max-height:none}
.my-scroll::-webkit-scrollbar{width:8px}
.my-scroll::-webkit-scrollbar-thumb{background:var(--dsw-alias-border-l2);border-radius:8px}
.my-section-title{position:sticky;top:0;z-index:1;margin:0;padding:8px 14px;font-size:14px;font-weight:600;
  color:var(--dsw-alias-label-primary);background:var(--dsw-alias-bg-layer-1)}
```

The section that must grow gets `flex:1;min-height:0`; its scroller overrides
`max-height:none`. Content-sized sections keep a cap (40vh) so they cannot starve the
growing section.

## 2. Rows + header on one template

```css
.my-row,.my-header{display:grid;align-items:center;gap:12px;
  grid-template-columns:minmax(0,1fr) 140px 140px 110px 96px 132px}
.my-row{border:1px solid var(--dsw-alias-border-l2);border-radius:10px;
  background:var(--dsw-alias-bg-layer-1);padding:10px 14px;cursor:pointer}
.my-row:hover{background:var(--dsw-alias-interactive-bg-hover)}
.my-list{display:flex;flex-direction:column;gap:8px;padding:10px 14px 14px}
.my-header{padding:6px 28px;border-bottom:1px solid var(--dsw-alias-border-l2)} /* list 14 + row 14 */
.my-header-cell{font-size:11px;font-weight:600;letter-spacing:.04em;text-transform:uppercase;
  color:var(--dsw-alias-label-secondary);overflow:hidden;text-overflow:ellipsis;white-space:nowrap}
.my-cell{font-size:12px;color:var(--dsw-alias-label-secondary);overflow:hidden;text-overflow:ellipsis;white-space:nowrap}
@media (max-width:720px){
  .my-row,.my-header{grid-template-columns:minmax(0,1fr) 120px 96px 120px}
  .my-cell--branch,.my-cell--event,.my-header-cell--branch,.my-header-cell--event{display:none}
}
```

Rules that matter more than the numbers: one template for every row kind **and** the
header; fixed px for data columns; the name column is the only `1fr`; every row renders
all cells (empty string, never `null`); the header's horizontal padding is
`listPad + rowPad`.

## 3. Status pills and badges

```css
.my-pill{box-sizing:border-box;display:inline-flex;align-items:center;justify-content:center;
  justify-self:center;min-width:112px;font-size:11px;font-weight:600;border-radius:999px;
  padding:2px 9px;border:1px solid var(--dsw-alias-border-l2);white-space:nowrap}
.my-pill--ok{border-color:var(--dsw-alias-state-success-secondary);background:var(--dsw-alias-state-success-tertiary);color:var(--dsw-alias-state-success-primary)}
.my-pill--bad{border-color:var(--dsw-alias-state-warn-secondary);background:var(--dsw-alias-state-warn-tertiary);color:var(--dsw-alias-state-warn-label)}
.my-pill--neutral{border-color:var(--dsw-alias-border-l2);background:var(--dsw-alias-bg-layer-2);color:var(--dsw-alias-label-secondary)}
```

Use one sizing class for all tones; tones change color only. `min-width` under
content-box sizing plus padding/border overflows a narrow track — always pair it with
`box-sizing:border-box`.

## 4. Empty state aligned with data text

```js
h('div', { className: 'my-list my-empty-wrap' },
  h('p', { className: 'my-empty-line' }, t('empty')))
```

```css
.my-empty-wrap{padding:10px 14px 14px}   /* same as .my-list */
.my-empty-line{margin:0;padding:14px;text-align:center;   /* same as .my-row */
  color:var(--dsw-alias-label-secondary);font-size:13px}
```

Inset = wrapper + line = 28px, matching a row's content (`list 14 + row 14`). Centering
is `text-align`, not flex, so the line wraps naturally.

## 5. Button-like link with an icon (toolbar)

```js
h('a', { className: 'my-repo-link', href: url, target: '_blank', rel: 'noreferrer noopener',
  'aria-label': t('a11y.openRepo') },
  h('span', null, 'owner/name'),
  h('svg', { className: 'my-repo-icon', viewBox: '0 0 16 16', width: 16, height: 16,
    fill: 'none', stroke: 'currentColor', strokeWidth: 1.6, 'aria-hidden': 'true' }, /* paths */))
```

```css
.my-repo-select{height:32px;min-width:240px;max-width:360px;width:auto;text-overflow:ellipsis;
  font:inherit;font-size:13px;color:var(--dsw-alias-label-primary);
  background:var(--dsw-alias-bg-layer-1);border:1px solid var(--dsw-alias-border-l2);
  border-radius:8px;padding:6px 10px}
.my-repo-link{display:inline-flex;align-items:center;gap:6px;height:32px;padding:0 10px;
  border:1px solid var(--dsw-alias-border-l2);border-radius:8px;
  background:var(--dsw-alias-bg-layer-1);color:var(--dsw-alias-label-primary);
  font-size:12px;text-decoration:none;white-space:nowrap}
.my-repo-link:hover{background:var(--dsw-alias-interactive-bg-hover)}
.my-repo-icon{display:block;flex:none;line-height:1}
```

Toolbar row and left group both `align-items:center`; icon `display:block` removes the
inline baseline that makes it sit high.

## 6. States: loading / error / stale

```js
// cache miss + in flight
h('div', { className: 'my-loading', role: 'status', 'aria-live': 'polite' }, t('loading'))
```

```css
.my-loading{display:flex;align-items:center;justify-content:center;padding:32px;
  text-align:center;color:var(--dsw-alias-label-secondary);font-size:13px}
```

- Loading is a page-level state, not a snapshot value: `snapshot === null && error === null`.
- On cache hit, render the snapshot and never show loading; refresh in the background.
- A failed background refresh keeps the rows and shows the existing banner; failures are
  never cached.
- Stale data gets one subdued warning line above the rows, never a hidden list.

## 7. Cache + request tokens (module scope)

```js
// factory scope — survives panel unmount, not page reload
const snapshotCache = new Map();      // entityId -> snapshot (successes only)
const latestTokens = new Map();       // entityId -> token
let tokenSequence = 0;

function nextToken(id) {
  tokenSequence += 1;
  latestTokens.set(String(id), tokenSequence);
  return tokenSequence;
}
function isLatest(id, token) {
  return latestTokens.get(String(id)) === token;
}
function cacheSnapshot(id, value) {
  if (value === null || typeof value !== 'object') return;
  snapshotCache.delete(String(id));
  snapshotCache.set(String(id), value);
  while (snapshotCache.size > 20) snapshotCache.delete(snapshotCache.keys().next().value);
}
```

`loadSnapshot` computes a token before the call, ignores results for an entity the user
left, and applies state/cache/banner only when `isLatest(id, token)`. Seed the initial
state from the cache so a remount paints rows immediately.

## 8. Harness notes (tests)

- Load `src/client.js` in `vm` with `window.__ModuleLoader__` capturing `{id, factory}`;
  `factory((spec) => spec === 'react' ? ReactStub : undefined)`.
- React stub: `createElement`, `Fragment`, `useState`/`useRef`/`useEffect`/`useMemo`/
  `useCallback`/`useSyncExternalStore`; record state writes, run effects, expose
  `setState` to drive re-renders.
- Fakes: `setTimeout`/`clearTimeout` with an advance() loop, `document.visibilityState`
  with `visibilitychange`, `localStorage` Map, `window.open` recorder.
- RPC: inject a function `(channel, method, payload) => Promise` so tests can defer
  responses and test cache hits, loading, failures, and out-of-order completion.
- CSS: parse the `CSS` template string into rule objects, look up classes, and assert
  declarations — then bind each assertion to a rendered class name so renames break.
- Geometry: compute content boxes from the parsed paddings; equal content widths are
  what make columns line up, not equal template strings.

## 9. Common failure signatures

| Symptom | Look at |
| --- | --- |
| `web boot: 1 entry did not activate … : failed` | client factory export missing `inject` |
| Plugin row `unsupported`, activation `… reading 'validate'` | `Config` not a native Schemastery schema |
| Panel mostly unstyled, borders gone | undefined `--dsw-alias-*` tokens |
| Middle column shifts per row | different templates or `max-content` data columns |
| Pills vary in width | per-conclusion sizing classes, content-box `min-width` |
| Header labels offset by one padding unit | header content box ≠ row content box |
| Page scrolls forever / list never scrolls | missing flex chain (`height:100%`, `min-height:0`, `flex:1`) |
| Empty text hugs the border | empty line outside the row-aligned inset |
| Icon sits high | bare inline anchor / `align-items:flex-start` |
| Switching entity flashes empty | component-scoped cache, or no cache with no loading state |
