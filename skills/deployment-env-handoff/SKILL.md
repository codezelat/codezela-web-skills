---
name: deployment-env-handoff
description: Use when preparing or auditing deployment readiness, Vercel, env vars, .env.example, README, AGENTS.md, migrations, live-domain checks, pushed-vs-deployed status, provider setup, no-secrets audits, or launch handoff.
---

# Deployment Env Handoff

Use this when local success must become repeatable deployment success.

## Non-Negotiables

- Do not put secrets in tracked files.
- `.env.example` documents names and purpose, not real values.
- README/AGENTS should match actual scripts and architecture.
- Deployment readiness includes migrations, provider dashboards, storage/email/auth domains, and live URL checks.
- Pushed code is not the same as deployed code; verify the live target when asked.
- Do not leave temporary migration/seed/docs files unless they are intentionally reusable.

## Workflow

1. Inspect package scripts, build command, output mode, deploy config, env usage, migrations, and provider dependencies.
2. Search for secret-like values in tracked files.
3. Update `.env.example` with all required and optional env vars grouped by service.
4. Update README/AGENTS with setup, migrations, seed, build, deploy, and verification commands.
5. Confirm `.gitignore` covers local env, generated private artifacts, and provider dumps.
6. Run build/lint/typecheck as relevant.
7. For Vercel or similar, check custom domain, production URL, runtime env, and migration order.

## Handoff Format

- Required env by provider.
- Commands to install, migrate, seed, build, and start.
- Provider dashboard settings still required.
- Verification already run.
- Known environment-dependent items not proven locally.
