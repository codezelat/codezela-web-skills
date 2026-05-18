---
name: performance-observability
description: Use when improving or auditing speed, Core Web Vitals, Lighthouse, PageSpeed, LCP, CLS, INP, bundle size, caching, third-party scripts, analytics, logging, monitoring, or production diagnostics.
---

# Performance Observability

Use this when performance must be improved without breaking product behavior.

## Non-Negotiables

- Measure before and after when feasible.
- Use production builds for serious performance claims; dev-mode timing is not proof.
- Use Lighthouse as the default local proof path for speed/Core Web Vitals work when browser tooling is available.
- Keep lab results separate from live field data and PageSpeed/CrUX data.
- Optimize the actual bottleneck, not a generic checklist.
- Preserve business flows while removing weight.
- Add observability where future failures would otherwise be silent.

## Workflow

1. Identify affected routes, critical user flows, current framework/build mode, and whether the user expects Google/PageSpeed proof.
2. Run a production build, serve it with the repo's production start command, then run Lighthouse locally when feasible.
3. Capture mobile first, then desktop when relevant. Record score, LCP, CLS, INP/TBT, FCP, Speed Index, and the top failing audits.
4. Inspect LCP, CLS, INP/TBT, render-blocking resources, image delivery, JS execution, third-party scripts, fonts, cache headers, robots/SEO warnings, and accessibility regressions surfaced by Lighthouse.
5. Fix in small steps: image sizing/format/priority, route-level Suspense, script strategies, font loading, dead JS, data caching, pagination, and DB query shape.
6. Add or confirm logging/analytics/error reporting for critical server actions, API routes, jobs, and provider calls.
7. Re-run the same Lighthouse/profile checks and compare before/after.

## Common Fixes

- Only the real above-the-fold LCP image gets eager/high priority.
- Delay non-critical analytics and marketing scripts.
- Reserve layout space for images, skeletons, and auth-dependent shells.
- Keep expensive providers out of global client layouts unless every page needs them.
- Cache static/public data intentionally and revalidate after mutations.
- Avoid blocking entire pages on optional DB sections.
- Do not claim Google speed/PageSpeed readiness from source review alone; run Lighthouse or clearly state why it could not be run.

## Checks

- `npm run build` or equivalent succeeds.
- Production-build Lighthouse result recorded for speed work when feasible.
- Live PageSpeed/CrUX status is reported separately from local Lighthouse lab results.
- No new console warnings for images/scripts/layout.
- Core route smoke confirms UX did not regress.
- Remaining bottlenecks are named with evidence.
