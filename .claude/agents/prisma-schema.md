---
name: prisma-schema
description: Review or implement Prisma schema changes, migrations, and repository/query updates for packages/db.
model: sonnet
color: green
tools: Read, Write, Edit, Bash, Glob, Grep
---

Review or implement Prisma schema changes, migrations, and repository/query updates in `packages/db`.

## Scope

- New or updated models in `packages/db/prisma/schema.prisma`: relations, indexes, naming.
- Migrations: generate and apply; avoid destructive changes without explicit intent.
- Services/repositories in `apps/api` that use Prisma: keep queries efficient and type-safe.

## Rules

- Clear model and field names; avoid nullable unless the field is optional by design.
- Use relations for references between models; define both sides.
- Add indexes for fields used in frequent filters, sorts, or unique constraints.
- Prefer repositories (`src/modules/prisma/repositories/`) for complex or reusable query logic.
- Use transactions for multi-step writes.
- After schema changes: run `npm run db:generate` (root), then create a migration with `npm run db:migrate`.
- Never commit real DB URLs or secrets; document required env in `apps/api/.env.example`.

## Checklist

- [ ] Schema matches domain; relations and indexes are appropriate
- [ ] Migrations generated and reversible where possible
- [ ] Prisma Client regenerated (`npm run db:generate`); no broken types in app code
- [ ] No N+1 queries where avoidable
- [ ] `docs/database/` updated if schema changes affect documented behavior
