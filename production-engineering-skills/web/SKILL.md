---
name: web
description: "Guide production web development. Use for browser applications, public websites, SPAs, and server-rendered or statically generated sites, including repository structure, component extraction, and behavior-preserving refactors; select the relevant web guidance."
---

# Web Application Production Skill

Use for:
- React
- Next.js
- Remix
- Vue
- Nuxt
- Svelte/SvelteKit
- Angular
- SPAs
- SSR/SSG applications
- browser-based SaaS products
- public websites

## Structure and reusable UI

Apply this guidance before web implementation or refactoring, then load the relevant supporting skills. Inspect the existing framework conventions and repository structure first.

- Distinguish page composition from reusable UI. Moving large blocks from an app file into section files is only the first step; inspect the repeated patterns inside those sections as well.
- Keep page-specific sections separate from reusable components. For a small React/Vite site, a useful structure is `src/layout/` for the site header and footer, `src/sections/` for page-specific sections, `src/components/` for reusable UI, and `src/data/` for content and configuration. Keep `App.jsx` focused on composition and genuinely shared behavior.
- Follow framework routing conventions and established feature boundaries when they already provide this separation. Treat the folder example as a starting point, not a required tree; avoid empty folders or extra nesting without a purpose.
- Extract components around repeated visual or behavioral units with meaningful inputs. Examples include a company card, a stack symbol with its title, a technology chip, a stack group, or a project feature populated by project data. Use clear props or composition to support the actual variations.
- Prefer one reusable project presentation with separate project content over one nearly identical component per named project. Keep formatting and interaction logic in UI code rather than embedding JSX in content data.
- Keep state at the narrowest owner that supports the workflow. Preserve state shared by navigation and content, such as a home control that clears an expanded card; do not relocate it solely to shorten the app file.
- Avoid extracting every wrapper, adding speculative variants, or designing a general-purpose UI library for a small site. The goal is useful reuse and clear ownership, not a target file count or line limit.

## Refactor verification

For a structural refactor, preserve content, styling hooks, DOM semantics, IDs, fragment links, accessible names, focus behavior, and interaction timing unless the user requested changes.

- Check hydration and initial HTML when SSR or prerendering is present. Comparing rendered output before and after extraction can catch accidental content or markup changes; account for generated bundle filenames.
- Run the existing build, formatting, output verification, and relevant interaction checks. Cover keyboard, pointer, touch, and responsive behavior where affected. Add tests for meaningful coverage gaps rather than tests that merely mirror the extraction.
- Update repository documentation when file locations or editing responsibilities change.

## Subskills

Read when relevant:

- [product-completeness/SKILL.md](product-completeness/SKILL.md)
- [ux-states/SKILL.md](ux-states/SKILL.md)
- [authentication/SKILL.md](authentication/SKILL.md)
- [security/SKILL.md](security/SKILL.md)
- [accessibility/SKILL.md](accessibility/SKILL.md)
- [seo/SKILL.md](seo/SKILL.md)
- [crawler-optimization/SKILL.md](crawler-optimization/SKILL.md) — audit and improve initial HTML, AI/search crawler access, metadata, and discovery files
- [performance/SKILL.md](performance/SKILL.md)
- [observability/SKILL.md](observability/SKILL.md)
- [testing/SKILL.md](testing/SKILL.md)
- [cicd/SKILL.md](cicd/SKILL.md)
- [react-nextjs/SKILL.md](react-nextjs/SKILL.md)
- [legal-privacy/SKILL.md](legal-privacy/SKILL.md)
- [audit/SKILL.md](audit/SKILL.md)

Before declaring a substantial web feature complete, run the web production audit.
