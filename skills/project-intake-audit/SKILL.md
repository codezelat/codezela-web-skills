---
name: project-intake-audit
description: Use when starting work in an unfamiliar repo, broad production-readiness task, risky feature, deployment check, admin/CMS setup, or when the user asks to inspect, audit, check everything, or understand before edits.
---

# Project Intake Audit

Use this before implementation when wrong assumptions could create churn. The goal is to find the real path, not to produce a generic plan.

## Non-Negotiables

- Inspect the current repo before writing code.
- Read repo instructions first: `AGENTS.md`, `README.md`, `.env.example`, package scripts, framework config, and relevant local skills/docs.
- Check dirty worktree state and never overwrite unrelated user changes.
- Preserve current architecture, data layer, and UI patterns unless the user explicitly asks for redesign/refactor.
- If Figma, screenshots, live URLs, or brand assets are provided, identify the exact source of truth and how to access it before UI implementation.
- If a tool/framework/provider is version-sensitive, read local bundled docs or current official docs before editing.
- If content, imagery, provider settings, or current best practice is uncertain, identify what needs research before implementation.
- Do not treat memory, another repo, or an older project as confirmed-current fact.

## Workflow

1. Check `pwd`, `git status --short`, branch, package manager, and dirty files.
2. Read project instructions, package scripts, framework config, env examples, route structure, and deployment config.
3. Identify stack: framework version, UI system, design source, auth, database, storage, email, captcha, analytics, deploy target.
4. Map existing patterns: data access, validation, forms, server/client boundaries, layouts, components, scripts, docs, and testing.
5. Identify exact user intent and scope: public site, admin, DB, media, forms, SEO, performance, security, deploy, or verification.
6. List risks: secrets, migrations, live data, deploy env, provider dashboards, content/image rights, cache/crawler behavior, dirty unrelated work.
7. Choose the next specialist skill sequence.

## Output

- Current stack, design source, and version-sensitive docs that matter.
- Relevant route/data/component map.
- Existing patterns to preserve.
- Risks, blocked facts, and env/provider dependencies.
- Proposed skill sequence and immediate next action.

## Do Not

- Start coding before this audit when the user asks for "fully", "prod ready", "check everything", or gives a large brief.
- Assume a previous repo's schema, env, route names, or provider setup still applies.
- Say something is ready before the relevant real path has been verified.
