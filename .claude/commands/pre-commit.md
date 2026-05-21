Run the pre-commit checklist and fix any failures before committing.

## Steps

Run in order from the repo root; fix failures, re-run until clean:

1. `npm run lint` — fix all ESLint errors
2. `npm run format` — apply Prettier; ensure formatted files are saved
3. `npm run check-types` — confirm no TypeScript errors
4. `npm test` (from `apps/api/`) — all unit tests must pass
5. `npm run test:e2e` (from `apps/api/`) — run if API routes or DB schema were changed

## Before confirming ready to commit

- No `.env*` or secret files in staged changes
- Commit message follows format: `{TICKET}: {type}({scope}): {description}`
  - Example: `PROJ-123: feat(auth): add refresh token endpoint`
- No `console.log` left in production code
- No `any` types introduced
- All new inputs validated via DTOs (server) or Zod (client)
