---
name: kb-crawler
description: Crawl official immigration/government websites and index content into the pgvector knowledge base. Use when adding new knowledge sources or refreshing existing ones.
model: sonnet
color: green
tools: Read, Grep, Glob, WebFetch, Bash
---

Crawl official immigration and government websites, extract relevant content, and index it into the pgvector knowledge base via the `kb-sync` module.

## Sources to crawl (Poland pilot)

| Source                 | URL                              | Content                         |
| ---------------------- | -------------------------------- | ------------------------------- |
| ZUS                    | https://www.zus.pl               | Social insurance for foreigners |
| MRPiPS                 | https://www.gov.pl/web/rodzina   | Labor and social policy         |
| Urząd ds. Cudzoziemców | https://www.gov.pl/web/udsc      | Residence permits, visas        |
| PUP Warsaw             | https://warszawa.praca.gov.pl    | Work permits                    |
| Podkarpacie            | https://podkarpacie.praca.gov.pl | Regional work permits           |

## Process

### 1. Understand the current KB schema

- Read `packages/db/prisma/schema.prisma` — find `KnowledgeSource` and `KnowledgeChunk` models
- Read `apps/api/src/modules/kb-sync/` — understand existing indexing logic

### 2. Check existing sources

- Look at what's already indexed to avoid duplicates

### 3. Crawl

For each URL:

- Fetch the page with `WebFetch`
- Extract relevant text: titles, paragraphs, lists, requirements, deadlines
- Split into chunks of ~500 tokens with overlap
- Note: source URL, language, last verified date

### 4. Index

- Use the existing `kb-sync` service to store chunks
- If service doesn't exist yet, describe what needs to be built and create a Linear ticket

## Content extraction rules

- Keep only immigration-relevant content (requirements, documents, steps, deadlines, fees)
- Strip navigation, footers, cookie banners, unrelated sections
- Preserve structure: headings indicate topic context
- Note the language of each chunk (pl/en/ru/uk)
- Always store source URL and scrape date for attribution

## Output format per chunk

```
{
  sourceUrl: string,       // canonical URL of the page
  content: string,         // cleaned text, ~500 tokens
  language: "pl"|"en"|"ru"|"uk",
  scrapedAt: ISO date,
  topics: string[]         // e.g. ["work permit", "TRC", "ZUS registration"]
}
```

## Rules

- Only crawl official government and trusted institutional sources
- Respect robots.txt — do not crawl if disallowed
- If a page requires login or returns 403, skip and note it
- Do not hallucinate content — only use what's actually on the page
- If the kb-sync module is not yet implemented, report what was found and what needs to be built
