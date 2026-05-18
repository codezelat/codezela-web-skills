---
name: nextjs-app-router-production
description: Use when implementing or reviewing Next.js App Router routes, layouts, metadata, Server Components, Server Actions, route handlers, caching, images, errors, loading states, scripts, or framework upgrades.
---

# Next.js App Router Production

Use this for production Next.js work where version drift can cause subtle bugs.

## Non-Negotiables

- Read the installed Next version and local docs under `node_modules/next/dist/docs/` when available; otherwise use current official docs.
- Keep App Router patterns. Do not introduce Pages Router files or APIs into an App Router project.
- Use Server Components by default. Add `"use client"` only for hooks, browser APIs, event handlers, or stateful interactivity.
- Use Server Actions for form mutations when that is the repo pattern; use route handlers for machine/API integrations.
- Keep metadata, canonical URLs, robots, sitemap, structured data, and social previews consistent across public routes.
- Treat loading, error, not-found, and route-group layouts as part of the user experience, not optional extras.

## Workflow

1. Inspect existing app structure, layouts, route groups, and helper modules.
2. Identify dynamic/static/ISR requirements before changing data fetching or cache behavior.
3. Read docs for touched APIs: metadata, route handlers, images, caching, forms/actions, redirects, middleware/proxy, errors.
4. Implement with repo-native conventions, aliases, validation, and typed helpers.
5. Add scoped skeletons for async sections that should not block the whole page.
6. Verify initial HTML when metadata, SEO, crawler, or social behavior matters.

## Common Decisions

- Above-the-fold image: reserve dimensions and use eager/high-priority only for the actual LCP candidate.
- Public DB section: isolate it with Suspense/loading UI if the rest of the page should render quickly.
- Redirect/auth guard: centralize in layout/helper, not ad hoc page checks.
- Dynamic route metadata: never emit broken absolute URLs; provide fallback social images when content images are absent.

## Checks

- `npm run lint` or repo equivalent.
- Typecheck/build script if present.
- `git diff --check`.
- Production build for route/layout/metadata/config changes.
- Browser or HTML smoke for changed routes.
