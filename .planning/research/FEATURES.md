# Feature Research

**Domain:** AI-powered poker training web app
**Researched:** 2026-03-18
**Confidence:** MEDIUM

## Feature Landscape

### Table Stakes (Users Expect These)

| Feature | Why Expected | Complexity | Notes |
|---------|--------------|------------|-------|
| Structured hand/scenario practice | Modern poker trainers center on practicing specific spots, not only reading theory | MEDIUM | Should cover hand context, stack depth, positions, actions, and board texture. |
| Instant decision feedback | Competitors repeatedly emphasize immediate evaluation after each move | MEDIUM | Feedback must arrive fast enough to preserve learning flow. |
| Progress tracking / leak visibility | Users expect to see where they are weak and whether they are improving | MEDIUM | MVP can start with lightweight stats rather than full dashboards. |
| Difficulty segmentation | Beginner and advanced players need very different material | MEDIUM | Closely matches your source docs and onboarding test idea. |
| Mobile-friendly training flow | Many poker learners train casually on phones between sessions | MEDIUM | Web-first responsive design is enough for v1; native app can wait. |

### Differentiators (Competitive Advantage)

| Feature | Value Proposition | Complexity | Notes |
|---------|-------------------|------------|-------|
| Plain-language AI coaching | Converts confusing theory into explanations players can actually act on | HIGH | This is the clearest product wedge in your source docs. |
| Adaptive terminology by skill level | Keeps beginners from bouncing while still respecting stronger users | HIGH | Best implemented as a product-wide explanation policy, not as a separate mode users must configure manually. |
| Personalized next-best training recommendation | Turns scattered sessions into a learning loop | HIGH | Can begin with rule-based recommendations before advanced personalization. |
| AI chat follow-up on why a move is right/wrong | Bridges training and deeper understanding without exposing raw solver complexity | MEDIUM | Strong complement to instant feedback if tightly scoped to the current hand. |
| Lightweight post-session recap | Helps users remember patterns instead of isolated mistakes | MEDIUM | Can be session summary first, full long-term coaching later. |

### Anti-Features (Commonly Requested, Often Problematic)

| Feature | Why Requested | Why Problematic | Alternative |
|---------|---------------|-----------------|-------------|
| Real-time in-game assistance | Sounds like the fastest route to winning more | Violates platform rules, creates compliance risk, and fights the learning mission | Practice mode plus post-hand review |
| Full solver clone in v1 | Serious players recognize solver authority | Expensive, complex, and weakens your plain-language differentiation | Curated scenarios plus clear explanation |
| Open-ended “analyze any possible hand tree” from day one | Feels powerful on paper | Blows up QA surface, latency, and pedagogy | Start with curated scenario libraries and structured hand review later |

## Feature Dependencies

```text
Skill assessment / manual level selection
    └──requires──> user profile and progress state

Scenario practice
    └──requires──> scenario content model
                       └──requires──> poker hand state representation

Instant AI feedback
    └──requires──> scenario practice
                       └──enhances──> session recap

Session recap
    └──requires──> captured hand results

Personalized training push
    └──requires──> progress history
                       └──requires──> consistent tagging of mistake types

Real-time assistance
    └──conflicts──> product integrity / fair-play boundary
```

### Dependency Notes

- **Scenario practice requires a stable scenario content model:** without structured hand data, explanation quality and analytics drift quickly.
- **Instant AI feedback depends on scoped context:** the model should explain a bounded decision, not improvise across an unstructured hand history.
- **Personalized recommendation depends on mistake tagging:** weak taxonomy means weak coaching later.
- **Real-time assistance conflicts with the product boundary:** document this early so it never sneaks into MVP scope.

## MVP Definition

### Launch With (v1)

- [ ] Scenario practice across beginner and intermediate difficulty — core training loop that proves users can learn independently
- [ ] Instant natural-language feedback on each decision — validates the “AI coach that speaks human” promise
- [ ] Skill onboarding or manual level selection — ensures explanation style and scenario difficulty fit the player
- [ ] Basic progress history and recurring-mistake tagging — enough to show improvement and prepare for later personalization
- [ ] Responsive web UI for focused training sessions — web-first delivery is sufficient for initial validation

### Add After Validation (v1.x)

- [ ] Session recap with top mistakes and pattern summary — add once the single-hand loop feels solid
- [ ] Follow-up “ask why” coaching chat — add once baseline explanation quality is trusted
- [ ] Terminology helper with contextual tooltips — add when beginner adoption becomes a clear driver

### Future Consideration (v2+)

- [ ] AI opponent battle mode — valuable, but much broader than the initial learning loop
- [ ] Personalized daily drill push engine — wait until enough progress data exists
- [ ] Hand-history import and deeper leak detection — add after core scenario training proves sticky
- [ ] Native mobile app — defer until web usage validates enough demand

## Feature Prioritization Matrix

| Feature | User Value | Implementation Cost | Priority |
|---------|------------|---------------------|----------|
| Scenario practice loop | HIGH | MEDIUM | P1 |
| Instant AI explanation | HIGH | HIGH | P1 |
| Skill-level adaptation | HIGH | MEDIUM | P1 |
| Progress and mistake tracking | HIGH | MEDIUM | P1 |
| Session recap | MEDIUM | MEDIUM | P2 |
| Follow-up AI coaching chat | MEDIUM | MEDIUM | P2 |
| AI opponent battle mode | MEDIUM | HIGH | P3 |
| Long-term personalized drill push | HIGH | HIGH | P3 |

**Priority key:**
- P1: Must have for launch
- P2: Should have, add when possible
- P3: Nice to have, future consideration

## Competitor Feature Analysis

| Feature | Competitor A | Competitor B | Our Approach |
|---------|--------------|--------------|--------------|
| Instant feedback | GTO Wizard emphasizes instant feedback and customizable training | DTO emphasizes GTO-bot practice with evaluation after each decision | Keep instant feedback, but bias toward clarity over raw theory exposure |
| Practice spots | DTO and GTO Wizard both organize training around spots/scenarios | Preflop Wizard focuses narrowly on one training surface | Start with curated spots and level-based progression instead of broad solver coverage |
| Explainability | Poker Sense leans into “Ask Why” plain-English explanation | Traditional tools often prioritize EV/frequency detail | Make explanation-first the default, with deeper detail only when useful |
| Progress tracking | Many trainers expose leak tracking and score history | Consumer-facing apps emphasize streaks and levels | Use progress as a coaching aid, not gamification for its own sake |

## Sources

- https://gtowizard.com/en — current trainer positioning and feature expectations
- https://www.dto.poker/pricing-dto-postflop/ — scenario/spot-based training and instant feedback expectations
- https://www.dto.poker/pricing-dto-cash/ — expectations around evaluation, repeat practice, and range access
- https://pokersense.app/ — plain-English AI coaching and “ask why” interaction pattern
- https://www.preflopwizard.app/ — training + progress tracking + mobile-friendly expectation
- https://www.instapokerpro.com/ — instant feedback loop and crafted training hands
- Local product docs in `docs/` — primary source for product differentiation and boundaries

---
*Feature research for: AI poker coaching MVP*
*Researched: 2026-03-18*
