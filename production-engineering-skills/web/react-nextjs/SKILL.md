---
name: react-nextjs
description: "Implement or review React and Next.js production behavior. Use for effects, state races, hydration, App Router conventions, caching, and server action security."
---

# React / Next.js Production

Read the parent [web guidance](../SKILL.md) before implementation or refactoring. Apply its structure and reusable UI guidance alongside this framework checklist.

## React

Check:
- stable keys
- effect cleanup
- stale closures
- request cancellation
- race conditions
- unnecessary derived state
- error boundaries
- Suspense where appropriate
- optimistic update rollback
- query-cache invalidation
- hydration-sensitive rendering

## Next.js App Router

Consider:
- `loading.tsx`
- `error.tsx`
- `not-found.tsx`
- `global-error.tsx`
- Metadata API
- `robots.ts`
- `sitemap.ts`
- `manifest.ts`
- Open Graph image generation
- Server Components vs Client Components
- Route Handlers
- Server Actions
- cache/revalidation semantics
- redirects

Treat Server Actions as public server endpoints:
- authenticate
- authorize
- validate
- check ownership
