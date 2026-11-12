---
name: seo
description: "Improve public web page discoverability. Use for titles, canonical URLs, robots directives, sitemaps, social metadata, structured data, and rendered content."
---

# Web SEO and Discoverability

For public/indexable pages consider:
- unique title
- meta description
- canonical URL
- semantic heading structure
- robots.txt
- sitemap.xml
- Open Graph metadata
- social preview image
- Twitter/X card metadata
- favicon
- web manifest
- structured data when semantically valid
- hreflang for localized sites
- correct status codes
- redirect strategy
- no accidental noindex
- duplicate URL prevention
- SSR/SSG where content discoverability depends on rendered HTML

Common failure modes: a robots-disallowed URL is never read for `noindex`, so `noindex` cannot remove blocked pages; canonical tags must be self-referencing on canonical pages; sitemaps stop at 50,000 URLs or 50 MB; use `x-default` for language selectors; distinguish 301 from 302; normalize trailing slashes and case; use `X-Robots-Tag` for non-HTML resources.
