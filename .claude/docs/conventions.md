# Conventions Reference

## Security

- **Never** read or modify `.env*` files; use environment config helpers (e.g. `ConfigService`, `process.env`, `dotenv`) — never hardcode values
- Use placeholders in examples (`YOUR_API_KEY`); never commit real secrets
- Sanitize user input to prevent XSS/CSRF/injection attacks
- Secrets management: use environment variables + a secrets manager in production

## Confirmations Required

Ask before:

- `git push`, `git commit`, `git merge`, `git rebase`, `git reset`, branch deletes
- Installing/updating packages (`npm install`, etc.)
- Destructive file operations or DB migrations that change schema/data
- Deployments or external mutating API calls

Read-only operations, lint, test, and build do **not** need confirmation.

## Commit & Branch Convention

Standard format: `type(scope): description`

- Types: `feat`, `fix`, `docs`, `refactor`, `test`, `chore`, `perf`, `ci`, `build`
- Example: `feat(auth): implement JWT refresh token`

With ticket: `TICKET-123: type(scope): description`

Branch naming: `feat/TICKET-123`, `fix/TICKET-456`, `hotfix/TICKET-789`, `docs/update-readme`

## Pre-PR Checklist

- [ ] `npm run build` passes
- [ ] `npm run lint` passes (ESLint + Prettier)
- [ ] `npm run check-types` passes
- [ ] All tests passing
- [ ] No `any` types, no `console.log` in production code
- [ ] Inputs validated (server-side + client-side)
- [ ] Error handling — no raw stack traces exposed to users
- [ ] No hardcoded secrets or API keys
- [ ] Loading and error states implemented in UI
- [ ] TODO comments addressed or tracked in issues
