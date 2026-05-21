# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

> Full documentation: [.claude/docs/](.claude/docs/)

## Project

<!-- TODO: Replace with your project description -->
[Your project name] — [brief description, e.g. "AI-powered SaaS app, Node.js backend + React frontend"].

## References

| Topic                                             | File                                                         |
| ------------------------------------------------- | ------------------------------------------------------------ |
| Project structure, commands, architecture, infra  | [.claude/docs/architecture.md](.claude/docs/architecture.md) |
| Backend rules (framework, ORM, validation)        | [.claude/docs/backend.md](.claude/docs/backend.md)           |
| Frontend rules (framework, components, styling)   | [.claude/docs/frontend.md](.claude/docs/frontend.md)         |
| Testing patterns                                  | [.claude/docs/testing.md](.claude/docs/testing.md)           |
| Conventions, security, Pre-PR checklist           | [.claude/docs/conventions.md](.claude/docs/conventions.md)   |

## When to Read References

Read the relevant doc **before** starting work on any non-trivial task:

- Exploring project structure, running commands → `.claude/docs/architecture.md`
- Any backend work → `.claude/docs/backend.md`
- Any frontend work → `.claude/docs/frontend.md`
- Writing or reviewing tests → `.claude/docs/testing.md`
- Committing, PR review, security → `.claude/docs/conventions.md`

## Skills

| Skill                         | When to use                                                              |
| ----------------------------- | ------------------------------------------------------------------------ |
| `brainstorming`               | Before implementing any new feature or behavior change                   |
| `test-driven-development`     | Before writing implementation code                                       |
| `requesting-code-review`      | After completing a feature or task                                       |
| `systematic-debugging`        | On any bug, test failure, or unexpected behavior                         |
| `writing-plans`               | When given a spec or requirements for a multi-step task                  |

## Core Principles

- **Single Responsibility** — one clear purpose per module, service, or component
- **DRY** — avoid duplication; one fact in one place
- **YAGNI** — don't build features before they're needed
- **KISS** — favor clarity over complexity
- **Composition over inheritance** — small, focused units; inject dependencies

## Confirmations Required

Ask before: `git push`, `git commit`, `git merge`, `git rebase`, `git reset`,
branch deletes, `npm install`, destructive DB migrations, deployments.
Read-only ops, lint, test, build do **not** need confirmation.

## Commit Format

`type(scope): description`
Types: `feat` `fix` `docs` `refactor` `test` `chore` `perf` `ci` `build`
With ticket: `TICKET-123: type(scope): description`

## Architecture Decisions

Non-trivial architectural changes → add ADR in [`docs/adr/`](docs/adr/) first.
