---
name: public-site-content-seo
description: Use when building, auditing, or polishing public pages, content research, copy, CTAs, metadata, sitemap, robots, JSON-LD, Open Graph, Twitter/X, WhatsApp previews, share images, crawler behavior, or no-placeholder cleanup.
---

# Public Site Content SEO

Use this to turn a public-facing site from assembled into credible, crawlable, shareable, and ready for real users. The site may be corporate, SaaS, ecommerce, service, portfolio, content, or product-led; do not assume any specific page set exists.

## Quality Bar

- Minimal, useful wording. No filler, vague chips, fake CTAs, lorem ipsum, or placeholder copy.
- Every button/link must go somewhere real; remove fake socials and dead downloads instead of guessing.
- Contact, address, phone, social, legal, and business claims must be true or omitted.
- Page titles and descriptions must be human-written, specific, and sized for search snippets.
- If copy, claims, examples, or imagery are missing, research suitable current material instead of inventing weak filler.
- Public DB sections need scoped loading, empty, and error states so one slow query does not block the whole page.
- Preserve the current brand voice and visual system unless the user explicitly asks for redesign.
- Social preview images must be absolute, public, crawler-safe URLs on production.

## Workflow

1. Map all public routes, shared header/footer/nav, sitemap, robots, metadata helpers, content sources, and social image helpers.
2. Search for placeholders, dead links, TODO copy, fake socials, dummy emails/phones, lorem ipsum, and unfinished CTAs.
3. Research missing business/content facts, competitive context, terminology, and suitable imagery when required by the page.
4. Rewrite copy with concise, brand-specific language and clear user intent.
5. Add or fix metadata: title template, canonical URL, description, OG/Twitter image, alternates if applicable.
6. Add structured data where useful: Organization, Product, Article, Q&A/help content, BreadcrumbList, or another schema that matches the actual page.
7. Ensure legal, policy, help, knowledge, article, product, or service pages are clear and not overclaiming when they exist.
8. Ensure 404/not-found, search empty states, pagination, filters, and taxonomy/category links are production-quality when present.
9. For share previews, verify live HTML and direct image URL status/content type; local metadata is not enough.
10. Verify generated HTML and route behavior.

## Checks

- Public routes render without placeholder content.
- Header/footer links work and do not expose private/admin paths.
- Metadata appears in initial HTML.
- Sitemap includes public canonical routes and excludes private/admin/API routes.
- Robots policy matches the deployment intent.
- Mobile/tablet/desktop layouts remain readable with no content overflow.
- Share previews use reachable absolute HTTPS image URLs and safe fallbacks for dynamic pages.
- Researched/source material is either verified, clearly cited in internal notes when needed, or omitted if rights/facts are uncertain.
