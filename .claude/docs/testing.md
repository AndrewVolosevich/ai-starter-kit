# Testing Reference

> **Skill:** Use `test-driven-development` before writing implementation code.
> **Agent:** Use `.claude/agents/test-writer.md` subagent for writing or extending tests.

## Core Principle

Test behavior and contracts, not implementation details. A good test describes *what* the system does, not *how* it does it internally.

## Backend Tests

- **Unit tests:** Test services / use-cases with mocked dependencies (DB, external APIs)
- **Integration / E2E tests:** Test HTTP endpoints with a real or in-memory DB; test auth flows, validation errors
- Colocate unit tests next to source files (`*.spec.ts` / `*.test.ts`)
- Integration / e2e tests in a dedicated `test/` folder

<!-- Fill in your test runner, e.g.:
- Jest: `npm test` / `npm run test:e2e`
- Pytest: `pytest`
- Go: `go test ./...`
-->

## Frontend Tests

- Test user interactions and outcomes, not implementation details
- Mock API calls and external dependencies
- Test the most critical user flows (happy path + key error states)

<!-- Fill in your test framework, e.g.:
- Jest + React Testing Library: `npm test`
- Vitest + Vue Testing Library: `vitest run`
- Playwright / Cypress: `npm run test:e2e`
-->

## What to Test

1. Happy path — expected inputs produce expected outputs
2. Validation errors — invalid inputs are rejected with clear messages
3. Critical error branches — auth failures, not-found, server errors
4. Do **not** test: implementation details, private methods, third-party library internals
