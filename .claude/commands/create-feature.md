Create a complete full-stack feature (API module + web route + components). Follow `CLAUDE.md` and agent guidelines.

## Server: NestJS Feature (apps/api)

1. **Module** — `XxxModule` in `src/modules/<feature>/`, register in `AppModule`.
2. **Service** — `XxxService` with all business logic; inject PrismaService or a repository; throw NestJS exceptions (`NotFoundException`, `BadRequestException`, etc.).
3. **Controller / Resolver** — thin transport layer only — validate input via DTOs, delegate to service, return result. No business logic.
4. **DTOs** — request/response DTOs in `dto/` with `class-validator` decorators; use separate response DTOs to avoid exposing sensitive fields.
5. **Prisma** — add/update models in `packages/db/prisma/schema.prisma` if needed; run `npm run db:generate` and `npm run db:migrate`; create a repository in `src/modules/prisma/repositories/` for complex or reusable queries.
6. **Tests** — unit tests for service with mocked Prisma/repository (`*.spec.ts` next to source); e2e tests for new endpoints if relevant.

## Client: Next.js Feature (apps/web)

1. **Route** — Add page(s) under `app/[locale]/(main)/<feature>/page.tsx`; use the existing main layout (Navbar + `max-w-7xl` container).
2. **Components** — Add UI in `components/pages/<feature>/`; prefer Server Components; add `"use client"` only for interactivity.
3. **Data fetching** — Use `gqlFetch` from `lib/graphql-client.ts` for queries/mutations (no Apollo Client). For real-time streaming use `subscribeToChatStream` pattern from `lib/ws-client.ts`.
4. **Types & validation** — Define TypeScript interfaces inline or in the component file; add Zod schemas to `lib/validators/` only if reused across files.
5. **Forms** — Use React Hook Form + Zod for validation.
6. **i18n** — Add translation keys to all three locale files: `messages/en.json`, `messages/ru.json`, `messages/uk.json`.
7. **Tests** — Unit tests for components and hooks (Jest + React Testing Library); e2e for critical flows if Playwright is set up.

## Requirements

- Strict TypeScript — no `any`, no unresolved errors.
- All inputs validated; guards applied on server; no business logic in controllers.
- Export only what other modules need; use `forwardRef` only when unavoidable.
