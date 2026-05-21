# Backend Rules Reference

<!-- TODO: Add your framework-specific rules below the universal section -->

## TypeScript & Code Quality

- Strict TypeScript throughout; avoid `any`; use interfaces and enums for contracts
- Resolve all TypeScript, ESLint, and Prettier errors before finishing — never introduce new ones
- No `console.log` in production; use a proper logger (Winston / Pino / NestJS Logger / etc.)
- Comments explain _why_, not _what_

## Validation & DTOs

- Every request input must be validated before reaching business logic
- Never expose sensitive fields (e.g. `password`, `token`) in response types
- Sanitize user input to prevent injection attacks

## Data Layer

- Encapsulate all database calls in a repository or data-access layer
- Services must not call the database directly — go through the data layer
- After schema changes: regenerate client / run migrations before continuing
- Add indexes for fields used in frequent filters, sorts, or unique constraints

## Modules / Structure

<!-- Fill in your framework-specific structure, e.g.:

### NestJS
- One folder per feature under `src/modules/`
- Controller → Service → Repository → PrismaService
- Use `@Public()` to opt out of global JWT guard

### Express / Fastify
- One folder per domain under `src/routes/`
- Route handler → service → repository
- Middleware for auth, validation, error handling

### Django / FastAPI / Rails
- [Your conventions here]
-->

## Error Handling

- Throw typed exceptions / HTTP errors; never return raw error objects
- Catch and log unexpected errors; return safe, user-friendly messages
- Use structured error responses: `{ message, code, statusCode }`

## Background Jobs

<!-- Describe your queue/job conventions if applicable:
- Job naming convention
- Retry strategy
- Dead letter queue handling
-->
