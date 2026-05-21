# AI Starter Kit

A ready-to-copy folder of AI tooling for any new project — Claude Code configured, Husky hooks wired, and all skills committed so it works out of the box.

## What's in the box

| File / Folder | What it gives you |
|---|---|
| `.claude/settings.json` | `.env` protection (deny + Bash hook), prettier auto-format after every edit |
| `.claude/agents/` | 9 specialized subagents: reviewer, test-writer, security-reviewer, performance, prisma-schema, error-handling, api-contract, kb-crawler, ticket-creator |
| `.claude/commands/` | Slash commands: `/create-feature`, `/pre-commit`, `/explain`, `/prompt-creator` |
| `.claude/skills/` | Superpowers (14 skills), find-skills, next-best-practices, vercel-react-best-practices — committed so no global plugin needed |
| `.claude/docs/` | Template reference files: fill in architecture, backend, frontend, testing, conventions |
| `CLAUDE.md` | Lightweight index — fill in project description and update references |
| `.husky/pre-commit` | lint-staged + tests on every commit |
| `.husky/pre-push` | type-check + lint before every push |
| `.lintstagedrc.json` | ESLint + Prettier on staged TS/TSX files |
| `skills-lock.json` | Reproducible skill installs via `npx skills experimental_install` |

## How to use

1. **Copy this folder into your new project:**
   ```bash
   cp -R ai-starter-kit/. my-new-project/
   cd my-new-project
   ```

2. **Install Husky hooks:**
   ```bash
   npm install   # installs husky + lint-staged, runs `prepare` to activate hooks
   ```

3. **Fill in `CLAUDE.md`** — replace the `<!-- TODO -->` placeholder with your project description.

4. **Fill in `.claude/docs/`** — each file has `<!-- TODO -->` sections for your tech stack. Keep what's universal, replace what's project-specific.

5. **Adjust `.claude/settings.json`** — add any project-specific `allow` rules you need.

6. **Add your linter config** — `.lintstagedrc.json` expects ESLint in the project. If you're not using ESLint, remove the `eslint` entry.

## Stack-agnostic by design

This kit works with any tech stack — Next.js, NestJS, Express, Fastify, Django, Rails, Go, whatever. The only assumption is **Node.js + npm** (for Husky). If you're not using Node at the root, adapt `.husky/pre-commit` and `.husky/pre-push` to call your lint/test commands directly.

## Updating skills

Skills are committed to `.claude/skills/` so they work without the global superpowers plugin. To update them:

```bash
npx skills update
git add .claude/skills/ skills-lock.json
git commit -m "chore(skills): update to latest"
```
