# Architecture Research

**Domain:** AI-powered poker training web app
**Researched:** 2026-03-18
**Confidence:** MEDIUM

## Standard Architecture

### System Overview

```text
┌─────────────────────────────────────────────────────────────┐
│                    Presentation Layer                      │
├─────────────────────────────────────────────────────────────┤
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────────┐  │
│  │ Training UI  │  │ Onboarding   │  │ Progress Views   │  │
│  └──────┬───────┘  └──────┬───────┘  └────────┬─────────┘  │
│         │                 │                    │            │
├─────────┴─────────────────┴────────────────────┴────────────┤
│                     Application Layer                       │
├─────────────────────────────────────────────────────────────┤
│  ┌───────────────────────────────────────────────────────┐  │
│  │ Domain services: scenarios, evaluation, coaching,    │  │
│  │ session tracking, recommendation rules               │  │
│  └───────────────────────────────────────────────────────┘  │
├─────────────────────────────────────────────────────────────┤
│                     Data / AI Layer                         │
├─────────────────────────────────────────────────────────────┤
│  ┌────────────┐  ┌────────────┐  ┌──────────────────────┐  │
│  │ Postgres   │  │ Auth       │  │ OpenAI evaluation /  │  │
│  │ scenarios  │  │ + profiles │  │ explanation service  │  │
│  └────────────┘  └────────────┘  └──────────────────────┘  │
└─────────────────────────────────────────────────────────────┘
```

### Component Responsibilities

| Component | Responsibility | Typical Implementation |
|-----------|----------------|------------------------|
| Training experience | Presents scenario state, actions, and feedback loop | Next.js route with client components for interaction and server actions/API endpoints for persistence |
| Coaching engine | Turns scenario outcome into player-facing explanation | Domain service that combines deterministic scenario metadata with LLM prompting |
| Scenario catalog | Stores and retrieves curated poker situations | Postgres tables with normalized scenario, street, action, and tagging data |
| Progress tracker | Records attempts, mistakes, and level history | Postgres tables plus aggregation queries/views |
| Identity/profile layer | Handles auth, skill level, and preferences | Supabase Auth + profile table |

## Recommended Project Structure

```text
src/
├── app/                    # Next.js routes and server actions
│   ├── (marketing)/        # Landing and docs-facing pages
│   ├── (app)/              # Authenticated product flows
│   └── api/                # API routes for structured actions if needed
├── features/               # Vertical product modules
│   ├── training/           # Scenario player, action submission, feedback UI
│   ├── onboarding/         # Skill test and level selection
│   ├── progress/           # History, leaks, summaries
│   └── coaching/           # Explanation and follow-up chat surfaces
├── domain/                 # Poker rules, scoring, taxonomy, prompt shaping
├── data/                   # DB access, schema, repositories
├── lib/                    # Shared clients (OpenAI, Supabase, logging)
└── types/                  # Shared TypeScript types
```

### Structure Rationale

- **`features/`:** keeps UI, actions, and local business logic grouped by product capability instead of framework primitive.
- **`domain/`:** protects poker-specific logic from leaking into UI code and makes testing much easier.
- **`data/`:** isolates persistence and migration concerns from product logic.

## Architectural Patterns

### Pattern 1: Deterministic core, generative explanation

**What:** score or classify the decision with structured scenario data first, then let the model explain it.
**When to use:** for every core practice interaction.
**Trade-offs:** much safer and more testable than letting the model decide everything, but requires curated scenario metadata.

**Example:**
```typescript
const evaluation = evaluateDecision({ scenario, playerAction })
const explanation = await generateExplanation({ scenario, evaluation, playerLevel })
```

### Pattern 2: Vertical slice feature modules

**What:** organize code around onboarding, training, progress, coaching.
**When to use:** from the start of MVP.
**Trade-offs:** clearer ownership and evolution; slightly more upfront structure than dumping everything into `app/`.

**Example:**
```typescript
// src/features/training/server/submit-action.ts
export async function submitTrainingAction(input: SubmitActionInput) {
  const evaluation = evaluateDecision(input)
  return persistAndExplain(evaluation)
}
```

### Pattern 3: Rule-first recommendations, ML later

**What:** generate “what to practice next” from tagged mistakes and simple heuristics before attempting advanced personalization.
**When to use:** MVP and v1.x.
**Trade-offs:** less magical than full AI personalization, but dramatically easier to validate and debug.

## Data Flow

### Request Flow

```text
[User chooses action]
    ↓
[Training UI] → [Submit handler] → [Evaluation service] → [Postgres]
    ↓                  ↓                    ↓                ↓
[Rendered feedback] ← [Explanation service] ← [OpenAI] ← [Stored attempt]
```

### State Management

```text
[Server state in DB]
    ↓
[Route loader / server component]
    ↓
[Client interaction state]
    ↔
[Submit actions / optimistic UI]
```

### Key Data Flows

1. **Scenario attempt flow:** load scenario → player acts → deterministic evaluation → AI explanation → persist result.
2. **Progress flow:** aggregate attempts by category / mistake tag → display trends → feed future recommendations.
3. **Skill adaptation flow:** onboarding or manual level selection → profile update → explanation tone and scenario difficulty adapt.

## Scaling Considerations

| Scale | Architecture Adjustments |
|-------|--------------------------|
| 0-1k users | Single Next.js app + Supabase backend is sufficient |
| 1k-100k users | Optimize hot queries, cache scenario reads, separate heavy AI jobs from request path when needed |
| 100k+ users | Consider dedicated background workers, analytics pipelines, and queue-backed explanation/recommendation workloads |

### Scaling Priorities

1. **First bottleneck:** AI latency/cost per action — fix with scoped prompts, caching, and structured evaluation before generation.
2. **Second bottleneck:** progress aggregation queries — fix with summary tables/materialized views rather than premature service splits.

## Anti-Patterns

### Anti-Pattern 1: Letting the LLM be the game engine

**What people do:** send an entire hand to the model and trust it to decide correctness.
**Why it's wrong:** inconsistent scoring, weak testability, and poor product trust.
**Do this instead:** keep scenario truth and scoring deterministic; use AI for explanation and adaptation.

### Anti-Pattern 2: Designing for every poker format immediately

**What people do:** model cash, tournament, multi-table, live reads, and hand import all at once.
**Why it's wrong:** schema and UX complexity explode before the core loop is proven.
**Do this instead:** choose a narrow first scenario universe and extend only after validation.

## Integration Points

### External Services

| Service | Integration Pattern | Notes |
|---------|---------------------|-------|
| OpenAI | Server-side structured calls through Responses API | Keep prompts server-side and log structured inputs/outputs for QA. |
| Supabase Auth | SSR-safe auth session handling | Needed early if progress history is user-specific. |
| Supabase Storage | Static assets and future media | Useful later for hand assets or richer content, but not a phase-1 dependency. |

### Internal Boundaries

| Boundary | Communication | Notes |
|----------|---------------|-------|
| training ↔ domain | direct function calls | Domain must own poker semantics and scoring rules. |
| coaching ↔ domain | structured DTOs | Explanations should consume evaluated facts, not raw UI state. |
| progress ↔ data | repositories / queries | Keep aggregation logic out of React components. |

## Sources

- https://nextjs.org/blog/next-16 — framework capabilities and app architecture direction
- https://supabase.com/docs/ — backend capability surface for auth/data/storage
- https://platform.openai.com/docs/api-reference/responses/retrieve — model/tool integration model
- https://vercel.com/blog/ai-sdk-5 — typed chat and streaming architecture patterns
- Local product docs in `docs/` — primary source for product modules and boundaries

---
*Architecture research for: AI poker coaching MVP*
*Researched: 2026-03-18*
