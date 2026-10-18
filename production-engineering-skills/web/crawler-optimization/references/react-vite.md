# React/Vite on static hosting

Use this reference when an existing client-rendered React/Vite site needs meaningful initial HTML without a server deployment. Adapt the entry paths, asset base, and output directory to the repository. Prefer framework-native rendering when it already exists.

## Build-time rendering

1. Keep the ordinary Vite client build so hashed assets and styles remain correct.
2. Add a server entry exporting a render function. Use React's renderToString with the same App and initial state as the browser; return markup and, if needed, identity data. Keep the root wrappers consistent, including StrictMode when used.
3. After the client build, load the server entry with Vite's server module loader and inject its result into the built HTML template. Assert that injection targets exist and fail the build if rendering fails. Use replacement callbacks so `$` sequences in generated content are not interpreted as replacement tokens.
4. Always close Vite resources in a finally block. Avoid dependency scanning, filesystem watchers, and WebSocket listeners that are unnecessary for a one-shot render. A working configuration in the originating project was:

```js
const server = await createServer({
  server: { middlewareMode: true, hmr: false, ws: false, watch: null },
  optimizeDeps: { noDiscovery: true, include: [] },
  appType: 'custom',
});
```

Check these options against the installed Vite version rather than treating them as universal APIs. Use the project's supported Node runtime, not an older default shell runtime.

5. Serialize JSON-LD using JSON.stringify and replace literal `<` with the literal escape sequence `\u003c` before placing it in a script element. This prevents data from terminating the script element.
6. Wire rendering into the standard build command, before artifact checks and upload. Deploy the exact checked output. The rendering entry and Vite server are build tools; neither needs a production server.

For client startup, an ordinary static site can preserve empty-root development rendering and hydrate the production artifact:

```jsx
const root = document.getElementById('root');
const app = <StrictMode><App /></StrictMode>;
if (root.hasChildNodes()) {
  hydrateRoot(root, app);
} else {
  createRoot(root).render(app);
}
```

## Browser-only behavior and static fallbacks

Keep window/document access out of rendering and module initialization. Run it in effects or event handlers. Avoid dates, randomness, viewport checks, or client-only data that would produce different first-render markup. Do not suppress hydration warnings to hide mismatches.

A disclosure can initially render readable content with `enhanced = false`. After hydration, set enhanced state and enable the normal collapsed presentation. Scope fallback styles to unenhanced cards, hide controls that cannot work without JavaScript, and give static content natural height. Apply inert and aria-hidden only when the enhanced disclosure is actually collapsed. Contributions intended to remain visible should not be placed in a collapsed region merely for search purposes.

If enabling the interactive layout changes section positions, restore direct fragment navigation after that layout is enabled, not before. Test direct fragment entry and refreshed fragments; an h1 already present in static HTML does not prove hydration is finished.

## Meaningful checks

- Require representative body content, including each role summary or product/project description, and real resume/profile/contact anchors. Parsing text with an HTML parser is more robust than substring assertions where escaping or markup splits content.
- Validate JSON-LD as JSON and compare canonical, sitemap locations, and generated identity URLs. Check local asset existence while respecting deployment base paths.
- Serve real built files for tests. Give robots.txt and sitemap.xml appropriate content types, and return real 404s for unknown paths rather than SPA fallback HTML.
- In JavaScript-disabled contexts, verify that summaries and links are visible and not inert. With JavaScript enabled, monitor page errors and hydration-related console errors, then run the existing interaction checks.
- Preserve expected negative tests: a deliberate 404 can emit a network console error without indicating an application or hydration failure.
- Use screenshots after hydration and relevant transitions have settled. Fixed headers and element screenshots can produce misleading overlaps; inspect the actual viewport before changing working layout based on a capture artifact.

Keep a concise project note explaining rendering, content sources, crawler policy, checks, and post-deployment indexing steps. Do not copy personal identity data, employer details, or unrelated site paths from another project into a reusable implementation.
