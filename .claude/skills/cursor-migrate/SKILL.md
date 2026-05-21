---
name: cursor-migrate
description: Migrate AI configuration between Cursor and Claude Code formats. Converts rules, commands, skills, and agents in both directions.
user-invocable: true
---

# Cursor ↔ Claude Code Migration

Migrate AI configuration files between Cursor (`.cursor/`) and Claude Code (`.claude/`) formats. Supports both directions.

## Usage

The user must specify a direction:

- **"cursor → claude"** — convert Cursor config to Claude Code
- **"claude → cursor"** — convert Claude Code config back to Cursor

If not specified, ask the user which direction before proceeding.

---

## Direction 1: Cursor → Claude Code

### Rules: `.cursor/rules/*.mdc` → `CLAUDE.md`

1. Read all `.mdc` files in `.cursor/rules/`.
2. For files with `alwaysApply: true` — extract their content and merge into the **Code Rules** section of `CLAUDE.md` (create it if absent). Deduplicate against existing content.
3. For files scoped to globs (e.g. `*.controller.ts`) — add as a named subsection under **Code Rules** with the glob noted.
4. Never overwrite existing `CLAUDE.md` content — extend it.

### Commands: `.cursor/commands/*.md` → `.claude/commands/*.md`

1. Read each file in `.cursor/commands/`.
2. Write to `.claude/commands/<same-name>.md` preserving content as-is.
3. Translate any non-English prose to English (code rules require English).

### Skills: `.cursor/skills/<name>/SKILL.md` → `.claude/skills/<name>/SKILL.md`

1. Read each `SKILL.md` found under `.cursor/skills/`.
2. Strip Cursor-specific frontmatter fields (`user-invocable`, `disable-model-invocation`); keep `name` and `description` as plain text or omit frontmatter entirely.
3. Create folder `.claude/skills/<name>/` if it doesn't exist.
4. Write content to `.claude/skills/<name>/SKILL.md`.

### Agents: `.cursor/agents/*.md` → `.claude/agents/*.md`

1. Read each file in `.cursor/agents/`.
2. Add YAML frontmatter with these fields:
   ```yaml
   ---
   name: <filename without extension>
   description: <first non-empty line of the file, or infer from content>
   model: <choose: opus for security/critical, haiku for lightweight, sonnet for the rest>
   color: <assign a unique color per agent — see palette below>
   tools: <minimal set needed — see tool assignment rules below>
   ---
   ```
3. Write to `.claude/agents/<same-name>.md`.

**Color palette** (assign uniquely across agents):
`red`, `orange`, `yellow`, `green`, `cyan`, `blue`, `purple`, `pink`

**Tool assignment rules:**

- Read-only analysis (reviewer, security, api-contract, error-handling): `Read, Grep, Glob`
- Needs to run commands or tests (performance, test-writer): add `Bash`
- Needs to write/edit files (test-writer, prisma-schema, create-feature): add `Write, Edit`
- Needs web access: add `WebFetch, WebSearch`
- Minimal (prompt-creator, explain): `Read` only

**Model assignment rules:**

- Security-critical tasks → `opus`
- Lightweight / creative / non-code tasks → `haiku`
- Everything else → `sonnet`

---

## Direction 2: Claude Code → Cursor

### `CLAUDE.md` → `.cursor/rules/*.mdc`

1. Read `CLAUDE.md`.
2. Split **Code Rules** section into logical groups matching Cursor rule conventions.
3. For each group create `.cursor/rules/<group-name>.mdc` with frontmatter:
   ```yaml
   ---
   description: <one-line description>
   alwaysApply: true
   ---
   ```
   Or use `globs` instead of `alwaysApply` if the rule is scope-specific.
4. Do not duplicate content already in existing `.mdc` files — check first.

### `.claude/commands/*.md` → `.cursor/commands/*.md`

1. Copy content as-is to `.cursor/commands/<same-name>.md`.
2. No structural changes needed.

### `.claude/skills/<name>/SKILL.md` → `.cursor/skills/<name>/SKILL.md`

1. For each folder in `.claude/skills/`, read its `SKILL.md`.
2. Create folder `.cursor/skills/<name>/` if it doesn't exist.
3. Add Cursor skill frontmatter:
   ```yaml
   ---
   name: <name>
   description: <description from content or filename>
   user-invocable: true
   disable-model-invocation: false
   ---
   ```
4. Write to `.cursor/skills/<name>/SKILL.md`.

### `.claude/agents/*.md` → `.cursor/agents/*.md`

1. Read each file in `.claude/agents/`.
2. Strip the YAML frontmatter block entirely.
3. Write remaining content to `.cursor/agents/<same-name>.md`.

---

## General Rules

- Always read existing files before writing to avoid overwriting manual edits.
- Preserve all meaningful content; only transform structure and metadata.
- English only in all output files.
- After migration, report a summary: files created, files updated, files skipped (already exist with same content).
- Ask for confirmation before writing if more than 5 files will be created or modified.
