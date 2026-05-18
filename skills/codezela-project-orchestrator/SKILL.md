---
name: codezela-project-orchestrator
description: Use when a user asks for broad production web work, full feature delivery, repo readiness, end-to-end audit, CMS/admin/public-site implementation, or a pipeline from brief through verification.
---

# Codezela Project Orchestrator

Use this to coordinate a production workflow. It chooses the correct specialist sequence and keeps scope, verification, and handoff tight.

## Operating Rules

- Start with the real repo state, not assumptions.
- Preserve architecture and design unless the user explicitly changes scope.
- Prefer current official or bundled docs for unstable tools and framework versions; research online when library/provider behavior, assets, or standards may have changed.
- Do not hardcode secrets, bootstrap credentials, fake links, placeholder content, or provider success states.
- Encode a clean product taste by default: minimal wording, smooth modern UI, responsive behavior, no clutter, no fake content.
- If Figma, screenshots, live references, or brand assets are provided, make visual parity part of scope and route UI work through `frontend-polish-shadcn-qa`.
- If content or images are missing, source real suitable material through `public-site-content-seo` and `media-storage-assets` instead of leaving placeholders.
- Prefer Better Auth, Resend, Turnstile, and R2/B2/S3-style storage only when they fit the repo and user intent; never force providers blindly.
- Keep docs/env/scripts/migrations synced when behavior changes.
- End with proof: lint/typecheck/build/test/browser/DB/email/storage/crawler/deploy checks as relevant.

## Skill Sequence

1. Start with `project-intake-audit` unless the repo state is already fresh in the current turn.
2. Use `nextjs-app-router-production` for Next.js route/layout/framework work.
3. Use `public-site-content-seo` for public pages, content, SEO, sitemap, robots, structured data, and share previews.
4. Use `hidden-admin-auth-cms` for admin auth, protected dashboards, or CRUD CMS.
5. Use `database-content-crud` for schema, migrations, seeds, content models, ordering, search, pagination.
6. Use `media-storage-assets` for uploads, R2/S3/B2, image rendering, fallbacks, LCP, asset cleanup.
7. Use `forms-email-captcha` for contact, inquiry, reset email, CAPTCHA, truthful form states.
8. Use `frontend-polish-shadcn-qa` for Figma/design-source parity, responsive UI, shadcn, skeletons, dialogs, a11y, i18n, visual QA.
9. Use `performance-observability` for Core Web Vitals, Lighthouse, caching, scripts, logs, and monitoring.
10. Use `security-privacy-hardening` for authZ, secrets, headers, dependencies, abuse controls, and privacy.
11. Use `deployment-env-handoff` for env/docs/Vercel/live readiness.
12. End with `verification-release-gate` for tests, smoke checks, and final proof.

## Execution Pattern

1. Audit: map the repo and exact requested surfaces.
2. Research: read current docs, design sources, provider setup, and asset/content sources when needed.
3. Plan: list the skill sequence and high-risk checks.
4. Implement: work in the smallest coherent slices.
5. Verify: run repo-native gates and real-path checks across every affected surface, not only the first page.
6. Handoff: say what changed, what was verified, and what remains environment-dependent.

## Done Criteria

- Implementation follows current repo architecture.
- Docs/env/migrations are synced when needed.
- Real path verification has run for the changed surfaces.
- Final response separates verified facts from remaining deploy/provider dependencies.
