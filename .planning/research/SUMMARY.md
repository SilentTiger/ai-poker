# Project Research Summary

**Project:** AI Poker
**Domain:** AI-powered poker training web app
**Researched:** 2026-03-18
**Confidence:** MEDIUM

## Executive Summary

This product sits closest to the modern poker trainer category, but your differentiation is not “more solver power.” It is a plain-language coaching layer that helps beginner-to-intermediate players understand their decisions through guided practice. Research suggests the most credible launch path is a web-first training product built around curated scenarios, immediate feedback, and lightweight progress tracking, not a generalized solver or real-time assistant.

The recommended implementation approach is a modular Next.js 16 application backed by Supabase for auth and structured data, with OpenAI’s Responses API and AI SDK 5 used for tightly scoped explanation and coaching interactions. The main product risk is letting the AI become the source of poker truth; the safest path is a deterministic evaluation layer plus AI explanation.

## Key Findings

### Recommended Stack

Use a modern TypeScript web stack: Next.js 16 + React 19 + Node 22 LTS on the app side, Supabase for auth/data/storage, and OpenAI Responses API for explanation generation. This combination is current, documented, and optimized for shipping a rich AI web app quickly without fragmenting the architecture too early.

**Core technologies:**
- Next.js 16: full-stack web app framework — strong fit for SSR, auth flows, and product iteration speed
- Supabase: auth + Postgres + storage backbone — fast MVP path with structured data and access control
- OpenAI Responses API: coaching/explanation engine — current long-term API surface for multi-turn AI workflows

### Expected Features

The market expects spot-based practice, immediate feedback, progress visibility, and mobile-friendly access. Your strongest competitive edge is adaptive plain-language coaching that meets players where they are instead of forcing them into solver-native language.

**Must have (table stakes):**
- Scenario-based practice loop — users expect guided spot training
- Instant feedback after each action — core training behavior across the category
- Progress and weakness tracking — needed to show improvement

**Should have (competitive):**
- Skill-level-aware explanation — your clearest wedge
- Follow-up “why” coaching — deepens understanding without overwhelming users
- Lightweight session recap — turns single decisions into pattern learning

**Defer (v2+):**
- AI opponent battle mode — valuable but much broader than the MVP wedge
- Full personalization engine — best added after enough attempt data exists
- Native mobile app — unnecessary before web validation

### Architecture Approach

Build a modular monolith with four core domains: onboarding, training, coaching, and progress. Keep poker-state evaluation deterministic, then use AI only to explain the result in user-appropriate language. This preserves trust, testability, and product clarity.

**Major components:**
1. Scenario engine — loads structured poker situations and accepted actions
2. Evaluation/coaching service — scores the move, then explains it
3. Progress tracker — stores attempts, mistake tags, and history

### Critical Pitfalls

1. **Letting AI invent poker truth** — keep scoring deterministic and explanations bounded
2. **Trying to ship every module at once** — lock MVP to one end-to-end practice loop
3. **Explaining above the player’s level** — persist player level and QA for comprehension
4. **Weak content taxonomy** — tag scenarios and mistakes before scaling content

## Implications for Roadmap

Based on research, suggested phase structure:

### Phase 1: Foundations and Training Domain
**Rationale:** The product cannot validate anything until scenarios, user profiles, and deterministic evaluation exist.
**Delivers:** App foundation, auth/profile basics, scenario schema, seed content, evaluation pipeline
**Addresses:** core training loop prerequisites
**Avoids:** scope explosion and AI-as-truth pitfalls

### Phase 2: Guided Practice Experience
**Rationale:** The first real user value is completing a scenario and understanding the explanation immediately.
**Delivers:** Playable training UI, action submission, AI explanation layer, responsive product flow
**Uses:** Next.js app routes, OpenAI integration, bounded prompts
**Implements:** training and coaching components

### Phase 3: Progress and Adaptation
**Rationale:** Once the base loop works, progress visibility and level-aware adaptation make the coach feel real.
**Delivers:** onboarding skill assessment/manual level selection, progress history, mistake tagging, adaptive explanation tone

### Phase 4: Recap and Next-Step Coaching
**Rationale:** This phase begins the learning loop beyond isolated drills without expanding into a full battle system.
**Delivers:** session summaries, repeated-mistake surfacing, next recommended drills

### Phase Ordering Rationale

- Scenario and evaluation infrastructure must exist before explanation quality can be trusted.
- Progress and personalization depend on stable attempt data and tagging from earlier phases.
- Session recap and recommendations are more useful after the core drill flow is already instrumented.

### Research Flags

Phases likely needing deeper research during planning:
- **Phase 2:** prompt/evaluation contract design and cost-latency tradeoffs
- **Phase 4:** recommendation heuristics and summary generation quality controls

Phases with standard patterns (skip research-phase):
- **Phase 1:** auth, app scaffolding, basic relational schema
- **Phase 3:** user profile persistence and progress dashboards

## Confidence Assessment

| Area | Confidence | Notes |
|------|------------|-------|
| Stack | HIGH | Based mostly on current official documentation |
| Features | MEDIUM | Based on competitor public positioning plus your product docs |
| Architecture | MEDIUM | Derived from standard AI app patterns plus product constraints |
| Pitfalls | MEDIUM | Based on common AI-product failure modes and this domain’s boundaries |

**Overall confidence:** MEDIUM

### Gaps to Address

- Scenario source-of-truth format: define how hands, accepted actions, and evaluation rules are authored and versioned
- Explanation QA: define what makes an explanation “good enough” for beginners before large-scale content creation
- Scope of poker formats: lock the first scenario universe before requirements finalize

## Sources

### Primary (HIGH confidence)
- https://nextjs.org/blog/next-16 — framework baseline
- https://supabase.com/docs/ — backend capability baseline
- https://platform.openai.com/docs/api-reference/responses/retrieve — current OpenAI integration surface
- https://platform.openai.com/docs/assistants/how-it-works — deprecation/migration guardrail
- https://vercel.com/blog/ai-sdk-5 — typed AI app integration guidance

### Secondary (MEDIUM confidence)
- https://gtowizard.com/en — modern trainer capability expectations
- https://www.dto.poker/pricing-dto-postflop/ — spot training and instant feedback expectation
- https://pokersense.app/ — plain-language AI coaching pattern
- Local docs in `docs/` — product-specific vision and scope

---
*Research completed: 2026-03-18*
*Ready for roadmap: yes*
