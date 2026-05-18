---
name: database-content-crud
description: Use when designing, migrating, seeding, or fixing database-backed content, catalogs, categories, articles, CMS data, Postgres, Neon, Supabase, migrations, slugs, ordering, search, pagination, safe deletes, or data verification.
---

# Database Content CRUD

Use this for content systems where the data model, admin UX, and public rendering must stay consistent.

## Non-Negotiables

- Follow the repo's current data layer. Do not introduce an ORM/query builder if the repo uses raw SQL, and do not bypass an ORM if the repo standardizes on one.
- Migrations and seeds must be idempotent where possible.
- Never run destructive data changes without inspecting current counts and scope.
- New CRUD must handle validation, empty states, search/filter/pagination, ordering, edit/delete edge cases, and path revalidation/cache invalidation.
- Verify DB state after writes.
- Keep ordering explicit. Edits should not reorder rows unless the order field changes; new rows can appear first only if that is the chosen rule.
- Use transactions for multi-table writes and asset cleanup coordination.

## Workflow

1. Inspect schema, migrations, data helpers, server actions/API routes, and admin components.
2. Define content model: required fields, optional metadata, slugs, category relations, images, sort order, status/publish fields.
3. Add migration/update script using the repo's existing migration pattern.
4. Implement typed validation and unique slug handling.
5. Implement create/update/delete with transactions for related rows, images, and dependent records.
6. Add admin UI with search/filter/sort/pagination and non-browser confirmation dialogs.
7. Revalidate affected public/admin/sitemap paths.
8. Read back counts and sample rows after seed or data migration.

## Edge Cases

- Slug collision on create and update.
- Required category deleted while products reference it.
- Empty search/filter result.
- Pagination beyond last page after delete.
- Failed image upload after DB insert.
- Seed rerun after manual admin edits.
- User edits title but should preserve explicit slug/order.

## Checks

- Migration runs cleanly against target DB.
- Seed can rerun without duplicates.
- CRUD create/edit/delete works from admin.
- Public listing/detail pages reflect DB data.
- New additions and edits preserve intended ordering rules.
