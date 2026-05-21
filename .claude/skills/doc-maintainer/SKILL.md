Act as a documentation governance agent for this monorepo. Maintain quality and consistency across all files in `docs/`.

## Documentation Map

| Section     | Path                | Covers                                                          |
| ----------- | ------------------- | --------------------------------------------------------------- |
| Setup       | `docs/setup/`       | Install, run, scripts, env vars, Docker, Prisma setup           |
| Development | `docs/development/` | Standards, folder structure, feature workflow, code reviews     |
| API         | `docs/api/`         | GraphQL schema, REST conventions, DTOs, endpoints, error shapes |
| Database    | `docs/database/`    | Prisma schema, migrations, repositories                         |
| Testing     | `docs/testing/`     | Unit (Jest), e2e (Supertest, Playwright), mocks, coverage       |
| Components  | `docs/components/`  | UI components, Server vs Client Components (web)                |
| Styling     | `docs/styling/`     | Tailwind, design tokens (web)                                   |
| Deployment  | `docs/deployment/`  | Build, production, Vercel, Railway, Supabase, Upstash           |
| Plans       | `docs/plans/`       | Implementation plans, feature specs                             |

`docs/README.md` is the main index — it must list all sections with short descriptions and links.

## Before Creating a New Document

1. Search `docs/` and `CLAUDE.md` for existing coverage of the same topic.
2. Use the table above to decide where the doc belongs.
3. Extend or update existing docs instead of creating duplicates.
4. If a topic spans sections, choose one primary doc and add "See also" links from others.

## Known Single-Source Topics

Do not create parallel docs for these — one canonical location each:

| Topic                 | Canonical Location                     |
| --------------------- | -------------------------------------- |
| Project structure     | `docs/development/folder-structure.md` |
| Env vars and setup    | `docs/setup/environment.md`            |
| Run scripts           | `docs/setup/environment.md`            |
| GraphQL API reference | `docs/api/graphql.md`                  |
| Database schema       | `docs/database/schema.md`              |
| Migrations            | `docs/database/migrations.md`          |
| Main doc index        | `docs/README.md`                       |

## When Editing Documentation

1. If renaming or moving a file, grep for old path references and update them (including `docs/README.md`).
2. When adding a doc to a section, add a link and short description to `docs/README.md`.
3. Cross-check Node.js / package versions against `package.json`; prefer "see package.json" over hardcoding versions.
4. Never put real secrets or API keys in docs — use placeholders (e.g. `your-secret-key`).
5. Use consistent terms: server — "controller", "service", "DTO", "guard", "module"; web — "page", "layout", "Server Component", "Client Component", "route".
6. English only for all documentation, code, and comments.

## Quality Checks Before Finishing

1. All internal markdown links point to existing files under `docs/`.
2. No secrets, passwords, or real API keys in the text.
3. Code examples (`bash`, `ts`, `tsx`, `json`) are syntactically valid and match project style.
4. Referenced paths (`src/`, `app/`, `packages/db/prisma/`, config files) exist in the repo.
5. Markdown style: ATX headings (`##`), fenced code blocks with language tags.
6. If adding a new file, ensure `docs/README.md` references it.
7. Links between docs use relative paths (e.g. `../api/graphql.md`).
