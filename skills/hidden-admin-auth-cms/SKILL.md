---
name: hidden-admin-auth-cms
description: Use when building or hardening hidden admin authentication, admin-only login, no-signup flows, password reset, protected dashboards, profile, CMS CRUD, route protection, sessions, or admin seeding.
---

# Hidden Admin Auth CMS

Use this for private operator/admin areas that must not leak into the public UX.

## Non-Negotiables

- Keep auth surface isolated under the configured hidden admin path, usually `/hidden-admin/*`.
- Do not add public signup unless the product explicitly requires it.
- Do not hardcode real admin credentials in code, docs, placeholders, or tests.
- Password reset and redirects must be path-safe; no open redirects.
- Missing email/provider env must fail truthfully, not fake success.
- Protected admin routes should inherit a central layout/session gate.
- Admin UI should be minimal, searchable, responsive, and direct; avoid marketing fluff.
- In modern TypeScript/Next.js apps without an existing auth standard, Better Auth is a strong default for admin email/password auth. Still read current docs and preserve an existing auth stack if already chosen.
- Use Turnstile or equivalent abuse protection for admin login/reset when production risk warrants it, but keep local development env-driven and truthful.

## Workflow

1. Inspect current auth library, session helper, DB adapter, route structure, middleware/layout gates, and env contract.
2. Read current docs for auth library APIs before changing config or adapters.
3. Define public auth entry points and protected route groups.
4. Implement login, logout, forgot/reset password, profile/change password if needed.
5. Ensure sign-up is disabled, unreachable, and not linked.
6. Add admin shell: sidebar/mobile nav, header, active states, sign-out, and role-safe navigation.
7. Add CRUD screens with validation, search/filter/sort/pagination, dialogs, and safe delete flows.
8. Revalidate public/admin paths after mutations.
9. Keep admin excluded from public analytics, public language widgets, sitemap, and indexable robots output.

## Checks

- Unauthenticated users redirect from protected routes.
- Authenticated admin redirects away from login to dashboard.
- Login/logout updates UI immediately.
- Reset email path works with env and fails clearly without env.
- Dashboard/profile/CRUD routes are protected.
- No admin credential or reset token appears in git-tracked docs/code.
- CAPTCHA/abuse protection is enforced only when configured and behaves clearly when not configured locally.
