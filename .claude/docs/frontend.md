# Frontend Rules Reference

<!-- TODO: Add your framework-specific rules below the universal section -->

## Component Architecture

- **Keep components small and focused** — one responsibility per component
- **Lift state up** only when necessary; prefer local state
- **Composition over nesting** — avoid deeply nested prop drilling; use context or state manager for shared state
- Extract reusable logic into custom hooks / composables

## Data Fetching

<!-- Fill in your data fetching approach, e.g.:

### REST
- Use a typed API client; never call fetch() directly in components
- Centralize base URL and auth headers in one place

### GraphQL
- Use generated typed hooks (codegen)
- Separate query/mutation files from component logic

### tRPC / React Query / SWR
- [Your conventions here]
-->

- Validate all API responses before use (Zod / Yup / etc.)
- Handle loading, error, and empty states explicitly — never leave UI undefined

## Forms

- Use a form library (React Hook Form / Formik / VeeValidate / etc.) + schema validation
- Validate on the client AND server — never trust client-only validation

## Styling

<!-- Fill in your styling approach, e.g.:

### Tailwind CSS
- Utility-first, mobile-first, no inline styles
- Custom tokens in theme config / CSS variables

### CSS Modules / styled-components / etc.
- [Your conventions here]
-->

- No inline styles except for truly dynamic values
- Use design tokens / CSS variables for colors, spacing, typography

## Images & Assets

- Always specify dimensions for images to avoid layout shift
- Lazy load images below the fold
- Use optimized formats (WebP / AVIF) where possible

## Accessibility

- Use semantic HTML elements
- All interactive elements must be keyboard-navigable
- Images require descriptive `alt` text
- Sufficient color contrast (WCAG AA minimum)

## Framework-Specific Notes

<!-- Add your framework conventions here, e.g.:

### Next.js
- Server Components by default; `"use client"` only for interactivity
- Use `<Image>` component, not `<img>`
- i18n: [your locale setup]

### React (SPA / Vite)
- Router: [React Router / TanStack Router]
- State: [Zustand / Redux / Jotai]

### Vue / Nuxt / Angular / etc.
- [Your conventions here]
-->
