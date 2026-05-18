---
name: verification-release-gate
description: Use before claiming work is done, production-ready, safe to commit, safe to deploy, fully working, or when the user asks if everything is good, checked, verified, tested, visually checked, browser-tested, or ready.
---

# Verification Release Gate

Use this to prove the work, not to reassure. It also covers practical tests and smoke checks when a separate test suite would be overkill.

## Rule

Do not say "done", "prod ready", "safe to commit", or "fully working" until the relevant checks have actually run or the unverified dependency is explicitly called out.

## Test Choice

- Unit tests for pure helpers, validation, slugging, formatting, auth/path helpers.
- Integration tests for server actions, DB helpers, auth guards, provider wrappers, and webhooks.
- Browser/e2e tests for critical user flows, responsive behavior, dialogs, search/filter/pagination, and auth flows.
- Smoke scripts or manual live checks for storage, email, social crawlers, provider dashboards, and deployment.
- Visual/content smoke checks for pages where images, copy, generated content, or design-source parity changed.
- Do not add brittle tests for implementation details that users cannot observe.

## Verification Matrix

- Code: lint, typecheck, tests, build, `git diff --check`.
- Dependencies: audit when requested or security-sensitive.
- UI: browser or HTML smoke for changed routes.
- DB: migration/seed run and readback counts/sample rows.
- Auth: login/logout/protected redirect/reset/email path.
- Forms/email: real provider request or truthful missing-env behavior.
- Storage: upload/delete and direct public URL reachability.
- Images/assets: source rights checked, optimized files render correctly, no broken local/R2/public URLs.
- SEO/social: generated HTML tags plus live image URL status.
- Deploy: live domain/custom domain after deployment, not just local build.
- Security: secret scan, dependency audit, authZ/permission checks when relevant.
- Performance: production-build Lighthouse when speed/Core Web Vitals changed and browser tooling is available; otherwise state the fallback clearly.

## Workflow

1. Identify what changed and which checks are relevant.
2. Add or update targeted regression coverage where the risk justifies it.
3. Run repo-native scripts first.
4. Add targeted runtime/live checks for every affected path family, not only the obvious page.
5. Check visual/content/media output where assets or copy changed.
6. Stop local servers started for verification unless user asked to keep them.
7. Report commands and results concisely.
8. Separate verified from not verified.

## Final Report Shape

- Changed: one concise paragraph.
- Verified: commands/routes/provider checks that actually ran.
- Not verified or environment-dependent: exact reason and next action.
- Risk: only if a meaningful residual risk remains.

## Common Failure Patterns

- Build passes but live domain still serves old deploy.
- UI success appears but email/provider call failed.
- Local asset exists but deployed social crawler image URL 404s.
- Audit suggests unsafe downgrade; do not apply force fixes without explicit approval.
- Browser automation unavailable; use honest fallback and say what was not checked.
