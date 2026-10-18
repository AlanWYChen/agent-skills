---
name: crawler-optimization
description: Audit and improve what search engines, AI search crawlers, and non-JavaScript scrapers can extract from a website. Use for empty React app shells, prerendering and hydration, crawler metadata, discovery files, or crawlability regression checks. Supports audit-only and implementation requests; does not imply publishing or search-account changes.
---

# Crawler Optimization

Make the actual public content readable in the initial HTTP response while preserving the site's design, interactions, and factual accuracy. Separate three outcomes: technical access, useful extractable content, and eventual search discovery. Improving one does not prove the others.

## Establish what crawlers receive

- Identify the requested repository, deployment URL, hosting model, framework, build command, and existing checks. Keep unrelated sites and repositories separate even if they share a parent directory or domain. Preserve existing uncommitted changes.
- Inspect source HTML, generated production HTML, browser entry, content data, metadata, navigation, robots.txt, sitemap, and deployment workflow. Build output is the relevant artifact; inspecting source index.html alone is insufficient.
- Fetch the live page as a raw HTTP response when available. Record status, redirects, relevant headers, initial body content, links, metadata, and crawler-file responses. Compare a crawler user agent if useful, but do not present a spoofed request as a real crawl or proof of indexing. If access fails, clearly separate local findings from unverified deployment behavior.
- Compare raw HTML with a normal browser and a browser with JavaScript disabled. Look for missing headings, roles, product/project descriptions, skills, contact/profile links, download links, and content gated behind interactions. Check error statuses and robots directives as well as content.
- Do not assume every crawler lacks JavaScript or that an empty initial body proves Google has not indexed a page. Search engines and extraction tools have different rendering behavior. Consult current primary documentation before making engine-specific claims.

For audit-only requests, return evidence, limitations, and a prioritized implementation plan without changing the site.

## Implement the smallest suitable rendering change

Prefer the existing framework's supported static rendering or SSR. For a mostly static React/Vite site on static hosting, build-time rendering plus hydration often avoids a server runtime or framework migration. Read [the React/Vite reference](references/react-vite.md) when choosing this approach.

Render the same components and content data for initial HTML and the interactive application. Avoid a second hand-maintained SEO biography, hidden keyword blocks, bot-only content, or a noscript block as the sole substantive fix. Ensure all intended public routes receive appropriate HTML, canonical URLs, and real missing-page responses.

Retain useful content and essential navigation without JavaScript. For interactive cards and disclosures, provide an accessible static presentation, then enable collapsed/interactive behavior after hydration. Keep server markup and the first client render consistent. Verify inert, aria-hidden, keyboard focus, fragment navigation, and layout changes; CSS visibility alone cannot undo inert or accessibility attributes.

## Improve interpretation and discovery

- Preserve useful titles, descriptions, canonical URLs, and social-preview metadata. Use absolute public URLs where required and honor subpath deployments.
- Add appropriate static JSON-LD when it improves entity clarity. A personal portfolio can use ProfilePage with a Person mainEntity and verified sameAs profile URLs. Other sites need schemas that fit their actual content. Generate fields from maintained data where practical and keep claims consistent with visible text. Safely serialize JSON embedded in HTML.
- Repair placeholder profile links. Keep downloadable documents and contact links discoverable through ordinary anchors.
- Check existing crawler policy before editing robots.txt. A missing robots.txt is not itself a crawl block. Preserve intentional restrictions and treat AI search access separately from model-training preferences; do not silently broaden an existing policy.
- Add or repair a sitemap listing real canonical public pages. Do not list fragment sections as independent pages, fabricate lastmod dates, or include unrelated applications. Advertise the sitemap in robots.txt. For a small homepage-only site, a one-URL sitemap is sufficient.
- Treat special AI text files such as llms.txt as optional experiments, not prerequisites or substitutes for useful HTML. Verify current engine guidance if recommending them.

## Preserve content quality and user intent

Make expertise and ownership clear using verified source material and user statements. For portfolio cards, concise role summaries usually work better than copying resume bullets, employer marketing, or exhaustive implementation details. Preserve the user's chosen placement and tone. Describe engineering scope, architectural ownership, reliability, performance, and business importance when supported; never invent seniority, metrics, technologies, or outcomes to strengthen wording. Add detailed case-study pages only when the task calls for them and there is enough verified content.

## Verify and report

Use existing build verification and browser infrastructure rather than introducing a parallel stack. Match testing to the change:

- For rendering work, check raw built/served HTML for substantive body text and ordinary links, parse JSON-LD, and validate canonical/sitemap consistency and local assets. Metadata alone must not satisfy body-content checks.
- Exercise JavaScript-disabled reading, essential links, and fragment navigation. With JavaScript enabled, detect hydration errors and check existing pointer, touch, keyboard, responsive-layout, and reduced-motion behavior.
- Visually inspect meaningful layout changes. Extend deployment smoke checks to require substantive raw HTML, not only a rendered h1. Test against the local production build before publication when possible.
- For later copy-only edits, rebuilding and static-content verification may be enough; do not rerun a broad browser suite without a relevant concern.

Report what changed, what was tested, and whether the deployed page was verified. Keep deployment and Search Console actions within the user's authorization. Recommend owner-account URL Inspection, sitemap submission, and recrawl requests when appropriate. Do not claim guaranteed indexing, ranking improvements, or AI recommendations.
