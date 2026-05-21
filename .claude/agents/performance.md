---
name: performance
description: Analyze and improve performance across the full stack — Prisma queries and N+1 on the server, bundle size and Core Web Vitals on the client.
model: sonnet
color: orange
tools: Read, Glob, Grep, Bash
---

Analyze and improve performance across the full stack.

## Scope

### Server (apps/api)

- **Prisma:** Avoid N+1; use `include`/`select` wisely; add indexes for hot queries.
- **Services:** Expensive operations (external calls, heavy compute, Claude API) done once and reused where possible.
- **Caching:** Consider caching for read-heavy or expensive operations; invalidate correctly.
- **Resources:** Connection pools, memory; avoid leaks (unclosed handles, growing collections).

### Client (apps/web)

- **Bundle:** Minimize client JS; code splitting and dynamic imports; avoid heavy libs on client when avoidable.
- **Images:** Next.js `<Image>` component with width, height, alt; appropriate sizes and lazy loading.
- **Caching:** Apollo Client cache; fetch cache options for Server Components; revalidation strategy.
- **Core Web Vitals:** LCP, INP, CLS; avoid layout shifts; optimize above-the-fold content.
- **Resources:** Avoid leaks (listeners, subscriptions, timers); clean up in `useEffect`.

## Rules

- Prefer Server Components for static or server-fetched content to reduce client bundle.
- Use dynamic imports for heavy or below-the-fold Client Components.
- Prefer batch or bulk Prisma calls over loops; use relations and `include` to limit round-trips.
- Measure before optimizing; focus on actual bottlenecks (DB, CPU, I/O, bundle, LCP, CLS).
- Document caching strategy and TTL/invalidation if caching is introduced.

## Checklist

- [ ] No N+1 in Prisma usage; indexes present for filtered/sorted fields
- [ ] No redundant or per-request DB calls in controllers
- [ ] Client bundle minimal; code splitting used where appropriate
- [ ] Images use Next/Image with proper dimensions and alt
- [ ] No obvious listener, subscription, or connection leaks
- [ ] Core Web Vitals considered; layout shifts minimized
- [ ] Caching (if any) has clear invalidation and no stale sensitive data
