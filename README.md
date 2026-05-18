# Codezela Web Skills

Production-grade web development skills for AI coding agents.

Codezela Web Skills is a curated collection of reusable Agent Skills designed to guide AI coding agents through real web-app engineering work. It focuses on practical delivery standards for modern production projects: inspecting the actual codebase, following the existing architecture, researching uncertain details, building cleanly, verifying real routes, and avoiding fake completion claims.

These skills are built for teams and developers who want AI agents to work with discipline, context, and production awareness instead of rushing into random code changes.

---

## What This Repository Contains

This repository packages Codezela's web development standards as portable Agent Skills.

Each skill is a self-contained workflow folder that teaches an AI agent how to handle a specific area of production web development. The repository follows the Agent Skills structure where each skill directory contains a required `SKILL.md` file with YAML frontmatter and Markdown instructions.

Current structure:

```text
skills/
  skill-name/
    SKILL.md
    agents/
      openai.yaml
```

The `SKILL.md` file is the portable core of each skill. The `agents/openai.yaml` file provides UI metadata and default prompt support for compatible agent environments.

---

## Core Purpose

This repository helps AI coding agents work like proper production engineers.

The skills guide agents to:

- inspect the real project before making changes;
- understand the existing architecture before adding new patterns;
- use current documentation when tools, frameworks, or APIs may have changed;
- avoid placeholders, fake links, fake success messages, and unsupported claims;
- build clean, responsive, accessible interfaces;
- protect authentication, data, storage, secrets, and user privacy;
- test affected areas properly before reporting work as complete;
- document changes clearly for handoff and deployment.

---

## Skill Catalogue

| Skill                           | Purpose                                                                                                                                                         |
| ------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `codezela-project-orchestrator` | Coordinates broad production web work, full feature delivery, repo audits, multi-skill execution, and release readiness.                                        |
| `project-intake-audit`          | Reviews unfamiliar repositories before implementation, risky changes, migrations, or production fixes.                                                          |
| `nextjs-app-router-production`  | Handles modern Next.js App Router work including routes, layouts, metadata, server components, actions, caching, images, and production behaviour.              |
| `public-site-content-seo`       | Guides public pages, SEO content, page structure, CTAs, metadata, sitemap, robots, structured data, and social previews.                                        |
| `hidden-admin-auth-cms`         | Covers admin-only areas, protected dashboards, authentication flows, password resets, profile handling, and CMS CRUD.                                           |
| `database-content-crud`         | Covers schema design, migrations, seeds, content ordering, slugs, search, pagination, safe deletes, and database verification.                                  |
| `media-storage-assets`          | Handles image sourcing, uploads, object storage, public URLs, fallbacks, optimisation, cleanup, and media verification.                                         |
| `forms-email-captcha`           | Covers contact forms, inquiry forms, auth forms, email delivery, SMTP or Resend setup, CAPTCHA, validation, spam protection, and truthful success/error states. |
| `frontend-polish-shadcn-qa`     | Guides UI implementation, shadcn/ui usage, responsive polish, accessibility, i18n, tables, dialogs, loading states, visual QA, and design-source matching.      |
| `performance-observability`     | Covers Lighthouse, PageSpeed, Core Web Vitals, bundle weight, scripts, caching, logs, analytics, uptime checks, and production diagnostics.                     |
| `security-privacy-hardening`    | Reviews authorisation, secrets, dependencies, headers, RLS, storage exposure, webhooks, rate limits, validation, and privacy risks.                             |
| `deployment-env-handoff`        | Prepares deployment, environment variables, README updates, AGENTS docs, migrations, provider setup, and live-domain checks.                                    |
| `verification-release-gate`     | Performs final verification before code is called done, safe to commit, production-ready, or safe to deploy.                                                    |

---

## Recommended Agent Workflow

For broad web-app tasks, start with the orchestrator skill:

```text
Use $codezela-project-orchestrator for this task.
```

The orchestrator should route the work through the correct specialist skills based on the task.

Recommended delivery flow:

1. Understand the request and define the affected area.
2. Inspect the real repository, files, routes, dependencies, and conventions.
3. Identify the correct specialist skill or combination of skills.
4. Research current documentation when facts, APIs, packages, standards, or provider behaviour may have changed.
5. Implement changes within the existing architecture.
6. Run focused checks for the affected feature.
7. Verify the real user-facing route, admin path, API path, database path, email path, storage path, or deployment path.
8. Update documentation, environment notes, migrations, or handoff instructions when behaviour changes.
9. Report what was verified, what changed, and what still depends on external configuration.

---

## Codezela Web Standard

The skills in this repository follow a strict production standard.

### Repo Awareness

Agents must inspect the actual project before acting. They should not assume the framework version, folder structure, styling system, authentication library, database provider, or deployment platform.

### Architecture Respect

Agents must preserve the current architecture unless the task explicitly requires a change. Existing components, utilities, naming conventions, API patterns, and styling systems should be reused wherever possible.

### No Placeholder Work

Agents must not leave fake copy, fake links, fake images, fake data, fake credentials, fake success states, or unfinished UI labelled as complete. Temporary work must be clearly marked and should not be treated as production-ready.

### Current Documentation

Version-sensitive tools must be checked against current official documentation or local bundled docs when needed. This applies to frameworks, package APIs, provider setup, analytics, auth systems, storage platforms, deployment services, search indexing, and compliance rules.

### Design Quality

Interfaces should be modern, responsive, accessible, and visually polished. Agents should use the repo’s existing component system and should prefer shadcn/ui where it fits instead of creating unnecessary parallel primitives.

### Content Quality

Public content must be useful, concise, human-readable, and conversion-aware. It should avoid filler, generic AI wording, keyword stuffing, weak CTAs, unsupported claims, and dead links.

### Security Discipline

Agents must never hardcode secrets, admin credentials, reset tokens, API keys, provider secrets, or bootstrap passwords. Authentication, authorisation, rate limits, validation, headers, webhooks, storage access, and privacy exposure must be handled carefully.

### Real Verification

Agents must verify the actual affected path. A build passing is not enough if the real page, API route, auth flow, database operation, email delivery, media upload, or deployment path has not been checked.

---

## Installation

Install all skills from the GitHub repository:

```bash
npx skills add codezelat/codezela-web-skills --skill '*'
```

Install globally for Codex:

```bash
npx skills add codezelat/codezela-web-skills -g -a codex --skill '*'
```

Install into the current project for Codex:

```bash
npx skills add codezelat/codezela-web-skills -a codex --skill '*'
```

List available skills before installing:

```bash
npx skills add codezelat/codezela-web-skills --list
```

Install from a local checkout:

```bash
npx skills add /absolute/path/to/codezela-web-skills --skill '*'
```

Manual Codex installation:

```bash
mkdir -p ~/.codex/skills
cp -R skills/* ~/.codex/skills/
```

---

## Using Individual Skills

You can ask an agent to use a specific skill directly.

Examples:

```text
Use $project-intake-audit to review this repository before implementation.
```

```text
Use $nextjs-app-router-production to fix this Next.js App Router issue.
```

```text
Use $forms-email-captcha to implement and verify this contact form.
```

```text
Use $verification-release-gate before saying this is ready to deploy.
```

Use the orchestrator when the task spans several areas, such as building a full feature, auditing a production project, preparing deployment, or fixing an issue that may involve frontend, backend, data, security, and verification.

---

## When To Use This Repository

Use Codezela Web Skills for:

- production website builds;
- web-app feature development;
- Next.js App Router projects;
- admin dashboards and CMS systems;
- content-heavy public websites;
- SEO-focused landing pages;
- database-backed CRUD features;
- form, email, and CAPTCHA workflows;
- media upload and storage workflows;
- deployment readiness checks;
- security and privacy hardening;
- performance and observability reviews;
- final QA before release.

---

## What The Skills Expect From Agents

Agents using this repository should:

- read the task carefully before editing;
- inspect files before modifying them;
- avoid broad rewrites when a focused fix is safer;
- keep changes aligned with existing project conventions;
- use official sources for uncertain or current technical details;
- run relevant checks instead of guessing;
- be honest about what could not be verified;
- separate verified facts from assumptions;
- keep handoff notes clear and useful.

---

## What The Skills Should Not Be Used For

These skills are not intended for:

- blind code generation without repo inspection;
- fake portfolio projects with placeholder claims;
- unsupported SEO or performance guarantees;
- copying third-party content without rights;
- bypassing authentication or security controls;
- storing secrets directly in code;
- replacing project-specific documentation, architecture decisions, or business rules.

For project-specific facts, use that project’s own documentation, such as `AGENTS.md`, internal docs, issue descriptions, environment notes, and deployment instructions.

---

## Publishing And Discovery

Public Agent Skills can be discovered through the open skills ecosystem after they are published and installed through the skills CLI.

Recommended publishing flow:

1. Keep this repository public on GitHub.
2. Ensure all reusable skill folders are inside `skills/`.
3. Validate each skill folder before release.
4. Install the skills using the CLI:

```bash
npx skills add codezelat/codezela-web-skills --skill '*'
```

5. Once users install the repository, anonymous CLI telemetry may help surface the skills on public discovery platforms such as skills.sh.

Users can disable telemetry when installing:

```bash
DISABLE_TELEMETRY=1 npx skills add codezelat/codezela-web-skills --skill '*'
```

When telemetry is disabled, the installation should not contribute to public leaderboard ranking.

---

## Maintaining Skills

When editing an existing skill or adding a new one:

1. Keep the folder name and `name:` frontmatter identical.
2. Use lowercase letters, numbers, and hyphens only for skill folder names.
3. Keep `description:` trigger-focused with clear keywords.
4. Keep `SKILL.md` concise, practical, and procedural.
5. Add `agents/openai.yaml` for UI metadata.
6. Ensure the default prompt references the correct skill name using `$skill-name`.
7. Keep reusable skills free from client-specific or project-specific facts.
8. Put project-specific instructions in the target project’s `AGENTS.md`.
9. Avoid root-level documentation unless it helps installation, usage, validation, or maintenance.
10. Review every skill for clarity, safety, and production usefulness before release.

---

## Validation

Run these checks before committing changes:

```bash
git diff --check

for d in skills/*; do
  n="${d##*/}"
  front="$(sed -n 's/^name: //p' "$d/SKILL.md")"
  test "$front" = "$n" || echo "NAME_MISMATCH $n $front"
  test -f "$d/agents/openai.yaml" || echo "MISSING_AGENT $n"
  rg -F "\$$n" "$d/agents/openai.yaml" >/dev/null || echo "PROMPT_MISSING_SKILL $n"
done
```

Optional validation if `skills-ref` is available:

```bash
skills-ref validate skills/*
```

Smoke test the install flow before release:

```bash
npx skills add . --list
npx skills add . --skill '*' -a codex --copy
npx skills list -a codex
```

---

## Recommended Release Checklist

Before publishing or updating the repository:

- every skill has a valid `SKILL.md`;
- every `name:` value matches its folder name;
- every skill has an `agents/openai.yaml` file;
- every default prompt points to the correct `$skill-name`;
- no project-specific client facts are inside reusable skills;
- no secrets, credentials, tokens, or private URLs are committed;
- installation commands work from a clean environment;
- the skill catalogue in this README matches the actual folders;
- validation commands pass;
- the repository is ready for public installation.

---

## Licence

MIT Licence. See [`LICENSE`](LICENSE).
