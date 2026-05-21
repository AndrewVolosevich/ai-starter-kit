# Architecture Reference

<!-- TODO: Fill in with your project's actual architecture -->

## Project Structure

```
<!-- Replace with your folder structure, e.g.:

# Monorepo (Turborepo / Nx):
apps/
├── web/     # Frontend
└── api/     # Backend
packages/
└── shared/  # Shared types, utilities

# Or two separate folders:
client/      # Frontend (Next.js / React / Vue / etc.)
server/      # Backend (NestJS / Express / Fastify / etc.)

# Or a single app:
src/
├── client/
└── server/
```

## Tech Stack

```
<!-- Fill in:
Backend:  [framework + version + port]
Frontend: [framework + version + port]
Database: [PostgreSQL / MySQL / MongoDB + ORM/ODM]
Cache:    [Redis / Memcached]
Queue:    [BullMQ / RabbitMQ / SQS]
Storage:  [S3 / Cloudflare R2 / MinIO]
```

## Commands

```bash
# TODO: Replace with your actual commands
npm run dev          # Start development server(s)
npm run build        # Build for production
npm run lint         # Lint all code
npm run check-types  # TypeScript type check
npm test             # Run tests
```

## Communication

<!-- Describe how your layers communicate:
- Client → Server: [REST / GraphQL / tRPC / gRPC]
- Real-time: [WebSockets / SSE / long polling]
- Background jobs: [queue type + worker pattern]
- File storage: [local / S3-compatible]
-->

## Authentication

<!-- Describe your auth approach:
- Strategy: [JWT / session / OAuth / API key]
- Token storage: [localStorage / httpOnly cookie / memory]
- Guard: [middleware / decorator / guard class]
- Refresh: [rotation strategy]
-->

## Infrastructure (local via Docker)

<!-- Replace with your services:
| Service    | Port | Credentials   |
| ---------- | ---- | ------------- |
| PostgreSQL  | 5432 | user/password |
| Redis       | 6379 | —             |
| MinIO       | 9000 | user/password |
-->

## Environment Variables

<!-- List required env vars (no values — see .env.example):
Backend:
- DATABASE_URL
- REDIS_URL
- JWT_SECRET
- PORT

Frontend:
- NEXT_PUBLIC_API_URL (or VITE_API_URL, etc.)
-->

## Production Targets

<!-- Where does your project deploy?
Frontend → [Vercel / Cloudflare Pages / Netlify]
Backend  → [Railway / Render / Fly.io / AWS]
Database → [Supabase / Neon / PlanetScale / RDS]
Cache    → [Upstash / Redis Cloud]
Files    → [Cloudflare R2 / AWS S3]
-->

## Claude Code Configuration (`.claude/`)

```
.claude/
├── settings.json     # Permissions + hooks (.env deny, prettier auto-format)
├── docs/             # Reference files (this folder)
├── agents/           # Specialized subagents (reviewer, test-writer, etc.)
├── commands/         # Slash commands (/create-feature, /pre-commit, etc.)
└── skills/           # Reusable skills (superpowers, find-skills, etc.)
```
