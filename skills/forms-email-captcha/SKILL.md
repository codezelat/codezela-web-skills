---
name: forms-email-captcha
description: Use when building or hardening contact forms, inquiry forms, auth emails, password reset, Resend, SMTP, Turnstile, reCAPTCHA, truthful success/error states, spam protection, or provider env handling.
---

# Forms Email Captcha

Use this for forms where a visible success state must correspond to a real server-side result.

## Non-Negotiables

- Do not show success if the real email/provider action failed.
- Missing provider env should produce a clear, safe configuration error.
- CAPTCHA can be bypassed locally only by explicit env-driven logic; production checks must be enforced when keys are configured.
- Do not expose secrets or raw provider errors to users.
- Validate server-side with the repo's validation library.
- Preserve submitted values on validation errors except sensitive fields.
- Avoid browser alerts; use inline errors, toasts, or dialogs matching the repo.
- In modern TypeScript/Next.js apps without an existing email standard, Resend is a strong default. Still preserve the repo's chosen provider if it already exists.
- Use Turnstile or equivalent where spam/abuse risk exists, not as decorative friction.

## Workflow

1. Inspect existing form state pattern: Server Actions, API routes, `useActionState`, toasts, field errors.
2. Inspect email helper and provider env contract.
3. Add schema validation, honeypot, rate-limit, and CAPTCHA if appropriate.
4. Send emails through a throwing provider wrapper.
5. Return concise user-facing success/error states.
6. Document required env in `.env.example` and README when behavior changes.

## Edge Cases

- Provider key missing.
- Sender or recipient missing.
- CAPTCHA token missing/expired/invalid.
- Duplicate submission while pending.
- Provider timeout.
- User enters invalid email, very long text, or script-like content.
- Password reset token expired or reused.

## Checks

- Valid form path sends real provider request when env exists.
- Missing env returns truthful config error.
- CAPTCHA absent locally behaves as documented.
- CAPTCHA invalid in production/configured mode blocks submission.
- No browser alerts; use inline errors/toasts/dialogs per repo pattern.
