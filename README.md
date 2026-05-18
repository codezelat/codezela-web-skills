# Codezela Web Skills

Production web-development skills for AI coding agents.

This repository packages Codezela's web-app engineering standards as portable [Agent Skills](https://agentskills.io/home). The skills are written for real production work: inspect first, follow the current repo, research when facts are uncertain, build cleanly, verify the actual path, and avoid fake "done" states.

## What This Is

Agent Skills are reusable folders that teach an AI agent a focused workflow. Per the Agent Skills specification, each skill is a directory containing a required `SKILL.md` with YAML frontmatter and Markdown instructions. Skills may also include optional `scripts/`, `references/`, or `assets/`, loaded only when needed through progressive disclosure.

This repo currently keeps every skill self-contained:

```text
skills/
  skill-name/
    SKILL.md
    agents/
      openai.yaml
```

The `agents/openai.yaml` files are UI metadata for agents that support them. The portable core remains `SKILL.md`.

## Install

After publishing this repo on GitHub, install all skills with the skills CLI:

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

Manual Codex install is also valid:

```bash
mkdir -p ~/.codex/skills
cp -R skills/* ~/.codex/skills/
```

## How It Appears On skills.sh

[skills.sh](https://www.skills.sh/) indexes public skills installed through the open `skills` CLI. The documented flow is:

1. Publish this repository publicly on GitHub.
2. Ensure the repo has valid skill folders under `skills/`.
3. Install through the CLI, for example:

```bash
npx skills add codezelat/codezela-web-skills --skill '*'
```

4. Once users install it, anonymous CLI telemetry can surface the skills on skills.sh and its leaderboard.

Telemetry can be disabled by users with:

```bash
DISABLE_TELEMETRY=1 npx skills add codezelat/codezela-web-skills --skill '*'
```

If telemetry is disabled, installs should not contribute to leaderboard ranking.

## Skill Catalog

| Skill                           | Use When                                                                                                                      |
| ------------------------------- | ----------------------------------------------------------------------------------------------------------------------------- |
| `codezela-project-orchestrator` | Broad production web work, full feature delivery, repo readiness, end-to-end audits, and multi-skill execution.               |
| `project-intake-audit`          | Starting in an unfamiliar repo or before risky production work.                                                               |
| `nextjs-app-router-production`  | Building or reviewing modern Next.js App Router routes, layouts, metadata, actions, caching, and image behavior.              |
| `public-site-content-seo`       | Public pages, content research, copy, CTAs, metadata, sitemap, robots, structured data, and share previews.                   |
| `hidden-admin-auth-cms`         | Hidden/admin-only auth, protected dashboards, password reset, profile, and CMS CRUD.                                          |
| `database-content-crud`         | Schema, migrations, seeds, ordering, slugs, search, pagination, safe deletes, and data verification.                          |
| `media-storage-assets`          | Online image sourcing, uploads, object storage, public URLs, fallback images, optimization, and cleanup.                      |
| `forms-email-captcha`           | Contact/inquiry/auth forms, Resend/SMTP, Turnstile/reCAPTCHA, truthful success/error states, and spam protection.             |
| `frontend-polish-shadcn-qa`     | Figma/design-source implementation, shadcn UI, responsive UX, accessibility, i18n, dialogs, tables, skeletons, and visual QA. |
| `performance-observability`     | Lighthouse, PageSpeed, Core Web Vitals, bundle weight, scripts, caching, logs, analytics, and production diagnostics.         |
| `security-privacy-hardening`    | AuthZ, secrets, dependencies, headers, RLS, storage exposure, webhooks, rate limits, validation, and privacy.                 |
| `deployment-env-handoff`        | Vercel/deployment readiness, env vars, README/AGENTS, migrations, provider setup, and live-domain checks.                     |
| `verification-release-gate`     | Final proof before saying work is done, production-ready, safe to commit, or safe to deploy.                                  |

## Codezela Web Standard

These skills encode a specific working standard:

- Inspect the real repo before changing code.
- Preserve existing architecture and design unless the task explicitly changes it.
- Use current official docs or bundled local docs for version-sensitive tools.
- Research uncertain content, imagery, libraries, provider setup, standards, or current rules instead of guessing.
- Treat Figma, screenshots, live references, and brand assets as source-of-truth when provided.
- Keep words minimal and useful; no filler, fake CTAs, placeholder copy, or dead links.
- Prefer smooth, modern, responsive interfaces with strong hierarchy and clean interaction states.
- Use the repo's component system; use shadcn/ui when it fits instead of creating parallel primitives.
- Prefer Better Auth, Resend, Turnstile, and R2/B2/S3-style object storage only when the repo has no stronger existing standard.
- Never hardcode secrets, real admin credentials, bootstrap passwords, reset tokens, or fake provider success.
- Source imagery responsibly, verify usage rights, optimize assets, write useful alt text, and test every place they appear.
- Use production-build Lighthouse for serious speed claims when feasible, and separate local Lighthouse from live PageSpeed/CrUX data.
- Verify the real route, DB, auth, email, storage, crawler, browser, and deploy path that the change affects.

## Recommended Workflow

For broad web-app work, start with:

```text
Use $codezela-project-orchestrator for this task.
```

The orchestrator should route work through the specialist skills:

1. Audit the repo and exact scope.
2. Research current docs, provider settings, content, images, and standards when needed.
3. Implement with the repo's architecture.
4. Run focused tests and browser checks.
5. Verify every affected surface, not just the first page.
6. Update docs/env/migrations when behavior changes.
7. Report verified facts separately from environment-dependent items.

## Maintaining Skills

When editing or adding a skill:

1. Keep the folder name and `name:` frontmatter identical.
2. Use lowercase letters, numbers, and hyphens only.
3. Keep `description:` trigger-focused with concrete keywords.
4. Keep `SKILL.md` concise and procedural.
5. Add `agents/openai.yaml` for UI metadata and ensure its `default_prompt` references `$skill-name`.
6. Do not add project-specific facts to a reusable skill; put project facts in that project's `AGENTS.md`.
7. Do not add root-level docs unless they help install, use, or maintain the repo.

## Validation

Run these checks before committing:

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

Smoke the install flow before release:

```bash
npx skills add . --list
npx skills add . --skill '*' -a codex --copy
npx skills list -a codex
```

## License

MIT License. See [LICENSE](LICENSE).
