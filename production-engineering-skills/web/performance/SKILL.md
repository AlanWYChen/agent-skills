---
name: performance
description: "Guide web performance. Use when implementing or reviewing runtime performance, responsiveness, resource usage, and bottlenecks in web applications."
---

# Web Performance

Track:
- LCP
- CLS
- INP
- server latency
- JS bundle size

Measure with field data (RUM or CrUX) and lab tooling (Lighthouse) before optimizing, and set budgets for the metrics that matter to the product.

Consider:
- route/code splitting
- lazy loading
- tree shaking
- image optimization
- responsive images
- modern image formats
- font loading/subsetting
- CDN
- caching
- compression
- request deduplication
- sensible prefetch/preconnect
- list virtualization
- reducing unnecessary React rerenders
- API/database performance
- avoiding hydration issues

Target p75 field values of LCP ≤ 2.5 s, INP ≤ 200 ms, and CLS ≤ 0.1, plus a TTFB and JS budget, and enforce the same budgets in CI (Lighthouse CI, size-limit) as the build workflow.

Cache policy: hashed assets `Cache-Control: public, max-age=31536000, immutable`; HTML `no-cache` or short-lived with revalidation; `stale-while-revalidate` only deliberately; correct `Vary`; purge or version on deploy; never cache `Set-Cookie` or personalized responses at a shared edge.
