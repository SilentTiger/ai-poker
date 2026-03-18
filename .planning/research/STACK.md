# Stack Research

**Domain:** AI-powered poker training web app
**Researched:** 2026-03-18
**Confidence:** MEDIUM

## Recommended Stack

### Core Technologies

| Technology | Version | Purpose | Why Recommended |
|------------|---------|---------|-----------------|
| Next.js | 16.x | Full-stack React app, routing, SSR, API boundary | Officially current major release; strong fit for content-heavy AI products, auth flows, and progressive web UX. |
| React | 19.x | UI rendering and modern interaction patterns | Current React generation used by Next.js 16, with strong support for modern async UI and transition patterns. |
| TypeScript | 5.8.x | End-to-end type safety | Mature default for Next.js apps and especially useful when modeling poker states, AI payloads, and scenario schemas. |
| Node.js | 22.x LTS | Runtime for local/dev/server workloads | Stable LTS line for production use; safer baseline than non-LTS releases. |
| Supabase | Managed platform | Auth, Postgres, Storage, RLS, realtime primitives | Good speed-to-market choice for an MVP that needs auth, structured data, file storage, and row-level access without assembling many vendors. |
| OpenAI Responses API | Current API | Natural-language coaching, structured evaluation, tool-capable analysis | OpenAI’s current primary API for multi-turn model workflows and tool use; better long-term fit than building on deprecated Assistants primitives. |

### Supporting Libraries

| Library | Version | Purpose | When to Use |
|---------|---------|---------|-------------|
| `ai` / Vercel AI SDK | 5.x | Streaming chat and structured AI integration | Use for coaching/explanation interfaces, typed message transport, and provider abstraction in Next.js. |
| `zod` | 4.x | Runtime validation for scenario definitions and AI outputs | Use anywhere the model or admin tools emit structured payloads. |
| `@supabase/supabase-js` | 2.x | Auth, DB, and storage access | Use across client/server boundaries with SSR-safe patterns. |
| `drizzle-orm` or `prisma` | current stable | Typed schema access and migrations | Use if the team wants stronger app-level modeling than raw SQL helpers alone. |
| `tailwindcss` | 4.x-compatible setup | Fast UI iteration | Use for MVP speed, especially if the app needs many training states and responsive overlays quickly. |
| `pgvector` | current extension | Store embeddings for semantic retrieval | Use only if personalized coaching later needs semantic recall over prior hands, notes, or explanations. |

### Development Tools

| Tool | Purpose | Notes |
|------|---------|-------|
| ESLint | Code quality | Keep rules aligned with Next.js and React 19 patterns. |
| Vitest | Unit and domain logic testing | Good fit for fast testing of hand evaluation logic, scenario scoring, and prompt shaping utilities. |
| Playwright | End-to-end verification | Important for validating scenario flow, auth, and coaching output rendering. |
| Supabase CLI | Local backend workflows | Useful if local auth/database parity matters before production deploys. |

## Installation

```bash
# Core
npm install next@^16 react@^19 react-dom@^19 typescript@^5.8

# Supporting
npm install ai@^5 openai @supabase/supabase-js zod

# Optional data layer
npm install drizzle-orm drizzle-zod

# Dev dependencies
npm install -D vitest @playwright/test eslint
```

## Alternatives Considered

| Recommended | Alternative | When to Use Alternative |
|-------------|-------------|-------------------------|
| Next.js 16 | Astro + API backend | Better if the product is mostly content and only lightly interactive, which is not this project’s likely direction. |
| Supabase | Firebase | Reasonable if the team prefers Firebase’s ecosystem, but Postgres is usually a better fit for structured poker-domain data and analytics. |
| OpenAI Responses API | Direct provider SDK calls only | Works if AI usage stays extremely simple, but becomes less ergonomic once conversation state and tools grow. |
| Vercel AI SDK | Hand-rolled SSE/chat plumbing | Use only if minimizing dependencies matters more than development speed. |

## What NOT to Use

| Avoid | Why | Use Instead |
|-------|-----|-------------|
| Building v1 around deprecated Assistants API flows | OpenAI has published a migration path away from Assistants and a shutdown date for that API family | Responses API |
| A microservices-first architecture | Massive overhead for an MVP with one product loop and a small team | Modular monolith in Next.js + Supabase |
| Custom auth from scratch | Reinvents security-sensitive flows and slows MVP | Supabase Auth |
| Running solver-grade computation in the request path for v1 | High complexity and latency for an MVP focused on explanation-first guided practice | Pre-authored scenarios plus AI explanation layer |

## Stack Patterns by Variant

**If v1 stays web-first only:**
- Use Next.js + Supabase + OpenAI Responses API
- Because it minimizes moving parts while still supporting auth, progress tracking, and AI coaching

**If later adding native mobile clients:**
- Keep Supabase and the domain API stable
- Because auth, progress, and scenario data can be reused while new clients are added gradually

## Version Compatibility

| Package A | Compatible With | Notes |
|-----------|-----------------|-------|
| `next@16` | `react@19` | Next.js 16’s release notes explicitly reference React 19.2 support. |
| `ai@5` | OpenAI Responses models | AI SDK 5 documents provider-executed tools and typed chat patterns that fit this use case. |
| `@supabase/supabase-js@2` | Supabase hosted platform | Current documented JS client generation for auth/database/storage access. |

## Sources

- https://nextjs.org/blog/next-16 — verified current Next.js major and React 19 support
- https://nodejs.org/en/blog/release/v22.11.0/ — verified Node.js 22 as LTS line
- https://devblogs.microsoft.com/typescript/announcing-typescript-5-8/ — verified TypeScript 5.8 release
- https://supabase.com/docs/ — verified current Supabase product surface (Auth, Database, Storage, Realtime, Edge Functions)
- https://supabase.com/docs/guides/auth/passwords — verified password auth and email verification flow details
- https://supabase.com/docs/guides/database/extensions/pgvector — verified pgvector availability for later personalization/search
- https://platform.openai.com/docs/api-reference/responses/retrieve — verified Responses API as current primary interface
- https://platform.openai.com/docs/assistants/how-it-works — verified Assistants deprecation and migration guidance
- https://vercel.com/blog/ai-sdk-5 — verified AI SDK 5 capabilities and typed chat/tool patterns

---
*Stack research for: AI poker coaching MVP*
*Researched: 2026-03-18*
