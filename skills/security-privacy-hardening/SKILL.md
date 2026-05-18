---
name: security-privacy-hardening
description: Use when auditing or fixing authZ, secrets, vulnerable dependencies, security headers, RLS, storage exposure, webhooks, admin access, rate limits, validation, privacy, abuse controls, or production security readiness.
---

# Security Privacy Hardening

Use this when safety, access control, or privacy can affect production users or business data.

## Non-Negotiables

- Never print or commit secrets, tokens, passwords, private keys, or one-time reset links.
- Authentication is not authorization; check object ownership, role, and route-level access.
- Provider webhooks must verify signatures.
- Inputs must be validated server-side and queries parameterized.
- Private storage must not become public by accident.
- Security fixes must be verified by attempting the relevant allowed and blocked paths.

## Workflow

1. Map assets: public routes, admin routes, APIs/actions, DB tables, storage buckets, webhooks, env vars, and third-party providers.
2. Threat-model the requested surface: who can call it, what data changes, what secrets are involved, and what abuse looks like.
3. Check authN/authZ, CSRF/session behavior, open redirects, reset tokens, role checks, IDOR, rate limits, and audit logs.
4. Check data safety: SQL injection, XSS, file upload validation, RLS/policies, private/public bucket boundaries, and PII minimization.
5. Check platform posture: security headers, robots/admin exclusion, dependency audit, env separation, and deploy preview exposure.
6. Patch narrowly and verify the exploit path is blocked.

## Common Findings

- Public UI hides an action but server action/API lacks permission checks.
- Password reset success is shown although email failed.
- Admin pages are protected but admin APIs are callable directly.
- Storage upload validates extension but not MIME/content size.
- `.env.example` is safe but tracked docs mention real credentials.

## Checks

- Allowed user/path still works.
- Disallowed user/path is blocked server-side.
- Secret scan of touched files is clean.
- Dependency audit outcome is reported honestly.
- Security headers or provider settings are verified when changed.
