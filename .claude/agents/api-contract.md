---
name: api-contract
description: Review or define API contracts across the stack — DTOs, GraphQL types, Zod schemas, request/response shapes, status codes, and error formats.
model: sonnet
color: purple
tools: Read, Edit, Glob, Grep
---

Review or define API contracts across the full stack: NestJS DTOs + GraphQL resolvers on the server, TypeScript types + Zod schemas on the client.

## Scope

- **Server (apps/api):** Controllers, DTOs, GraphQL resolvers/types, status codes, error shapes; consistency across all endpoints.
- **Client (apps/web):** TypeScript types and Zod schemas for API requests and responses; TanStack Query / Apollo Client usage, error handling, loading states.
- **Shared (packages/graphql):** graphql-codegen output; keep generated types in sync with resolver definitions.
- **Docs:** Keep `docs/api/` in sync with actual endpoints and types.
- **Compatibility:** Avoid breaking changes to existing clients; version or extend when needed.

## Rules

- One canonical shape per resource; reuse DTOs with `PartialType`, `PickType`, `OmitType` on the server; reuse Zod schemas on the client.
- Validate all inputs on the server (class-validator DTOs); validate all API responses on the client (Zod).
- Never leak internal or sensitive fields (e.g. `password`) in responses or client types.
- Document new or changed endpoints/types in `docs/api/`.

## Checklist

- [ ] Server DTOs match request/response shapes; class-validator decorators in place
- [ ] Client Zod schemas match server response shapes
- [ ] GraphQL types generated and in sync with resolvers
- [ ] Correct HTTP/GraphQL status codes and consistent error body shape
- [ ] Sensitive data excluded from all responses and client types
- [ ] Error and loading states handled in UI
- [ ] `docs/api/` updated with new or changed operations
