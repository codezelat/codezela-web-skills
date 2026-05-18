---
name: media-storage-assets
description: Use when implementing or auditing media storage, online image sourcing, uploads, Cloudflare R2, S3, Backblaze B2, public asset URLs, image validation, fallback images, next/image, LCP warnings, fit/cover behavior, cleanup, or unused assets.
---

# Media Storage Assets

Use this for any feature where files enter the app, leave the app, or affect page performance.

## Non-Negotiables

- Storage credentials stay in env only.
- Do not ask the database to store binary files unless the app explicitly requires that architecture; store media in object storage and keep DB metadata/URLs/keys.
- Validate file type, size, count, and dimensions where relevant.
- When sourcing images online, verify usage rights and suitability; do not hotlink random images as a production dependency.
- Uploaded public URLs must be reachable by the runtime and crawlers when used publicly.
- Do not leave orphaned objects after update/delete flows.
- Use fit/contain/cover intentionally. Content cards often need full-image visibility on a light background; heroes can use cover.
- Above-the-fold images need reserved space and only the actual LCP candidate should be eager/high priority.
- Use stable object keys, safe filenames, content type, and long cache headers for immutable uploads.
- Prefer the repo's current provider. If greenfield, R2/B2/S3-compatible object storage is a practical default; choose based on deploy/provider constraints, public URL needs, and cost.

## Workflow

1. Inspect existing storage helper, env names, image config, upload forms, public rendering, and cleanup paths.
2. Confirm provider requirements: endpoint, bucket, region/account, access key, secret, public base URL/custom domain, CORS.
3. If images/assets must be sourced, find suitable rights-safe assets, download or upload them deliberately, optimize dimensions/format, write useful alt text, and name files cleanly.
4. Implement upload through a server-safe helper or signed upload flow.
5. Store only needed metadata: URL/key, alt text, position/order, content type if useful.
6. Add fallback image for missing content images.
7. Configure framework image allowlist/remote patterns.
8. Delete replaced/removed objects after DB transaction success or with safe compensating cleanup.
9. Audit unused local images only after confirming no DB rows, content records, or code paths use them.

## Checks

- Upload works with real provider env.
- Missing env gives a clear admin error.
- Public URL opens directly.
- Image renders in listing/card/detail/metadata surfaces.
- Delete/update removes orphaned storage objects.
- LCP/image warnings are addressed only on actual above-the-fold images.
- Sourced images are optimized, rights-safe for the intended use, not hotlinked accidentally, and visually tested in every place they appear.
