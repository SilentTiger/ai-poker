# Pitfalls Research

**Domain:** AI-powered poker training web app
**Researched:** 2026-03-18
**Confidence:** MEDIUM

## Critical Pitfalls

### Pitfall 1: Letting AI invent poker truth

**What goes wrong:**
The product gives confident explanations that do not match the intended scenario logic or strategy baseline.

**Why it happens:**
Teams ask the model both to judge the move and explain it, instead of separating evaluation from explanation.

**How to avoid:**
Build a deterministic scenario/evaluation layer first. Pass the model structured facts, not raw authority over correctness.

**Warning signs:**
Same decision gets different judgments on retry; QA can’t predict expected output; prompt tweaks change “truth.”

**Phase to address:**
Phase 1

---

### Pitfall 2: Trying to ship the whole poker product at once

**What goes wrong:**
MVP scope expands from guided drills into AI battle, full review, recommendation engine, and generalized solver behavior before the core loop is usable.

**Why it happens:**
The problem space is rich, and adjacent features all sound valuable.

**How to avoid:**
Lock v1 around one learning loop: scenario → decision → immediate explanation → progress capture.

**Warning signs:**
Requirements list grows across every module from the source docs; no single end-to-end flow feels complete.

**Phase to address:**
Phase 1

---

### Pitfall 3: Explaining above the player’s level

**What goes wrong:**
Beginners still bounce because the “coach” speaks like a solver user, not a human teacher.

**Why it happens:**
Teams optimize for correctness and depth but not pedagogy.

**How to avoid:**
Capture skill level explicitly, maintain explanation policies per level, and QA feedback copy against beginner comprehension.

**Warning signs:**
Outputs overuse jargon, frequencies, and theory terms without context; new users hesitate or abandon early.

**Phase to address:**
Phase 2

---

### Pitfall 4: Weak scenario tagging ruins later personalization

**What goes wrong:**
You collect lots of attempt data but cannot reliably tell what the player is bad at.

**Why it happens:**
Scenario content is created without a clear taxonomy for street, position, error type, or concept.

**How to avoid:**
Design content schema and mistake tags before bulk authoring scenarios.

**Warning signs:**
Progress dashboards show only generic scores; recommendations feel random or repetitive.

**Phase to address:**
Phase 1

---

### Pitfall 5: AI latency breaks the training loop

**What goes wrong:**
Users make a decision and wait too long for feedback, turning practice into friction.

**Why it happens:**
Prompts are too large, explanation generation is synchronous and verbose, or every request rebuilds too much context.

**How to avoid:**
Constrain prompt scope, keep explanation templates tight, and stream feedback where possible.

**Warning signs:**
Feedback times feel inconsistent; users click away before reading; costs rise faster than usage.

**Phase to address:**
Phase 2

## Technical Debt Patterns

| Shortcut | Immediate Benefit | Long-term Cost | When Acceptable |
|----------|-------------------|----------------|-----------------|
| Hardcoding scenario JSON without schema discipline | Faster prototype | Painful migration, unreliable analytics | Acceptable only for a tiny seed set if schema is stabilized immediately after |
| Storing only raw chat transcripts | Easy logging | Hard to audit, score, and personalize | Rarely acceptable |
| Skipping attempt/mistake taxonomy | Faster launch | Personalized coaching becomes guesswork | Never for this product |

## Integration Gotchas

| Integration | Common Mistake | Correct Approach |
|-------------|----------------|------------------|
| OpenAI | Sending overly broad unstructured prompts with no schema | Use structured inputs and narrow explanation tasks |
| Supabase Auth | Treating local defaults as production-safe email behavior | Configure production email/redirect settings explicitly |
| Progress analytics | Computing all metrics in UI code | Precompute or query server-side summaries |

## Performance Traps

| Trap | Symptoms | Prevention | When It Breaks |
|------|----------|------------|----------------|
| Recomputing large prompt context on every move | Slow or costly feedback | Keep scenario context bounded and reusable | Early, even at low traffic |
| Querying full attempt history for every dashboard render | Sluggish profile/progress screens | Add summary tables and filtered queries | Usually after moderate usage |
| Heavy client-side poker state logic everywhere | UI complexity and hydration pain | Keep domain logic centralized and mostly server/shared | As soon as flows multiply |

## Security Mistakes

| Mistake | Risk | Prevention |
|---------|------|------------|
| Leaking prompts or internal evaluation rules to the client | Easier abuse and brittle product trust | Keep prompts and evaluation policy server-side |
| Weak row-level access control on attempt history | Users can access other players’ progress data | Use Supabase RLS from the start |
| Building custom auth flows unnecessarily | Credential and session risk | Use managed auth patterns |

## UX Pitfalls

| Pitfall | User Impact | Better Approach |
|---------|-------------|-----------------|
| Showing only “correct/incorrect” without reasoning | Users memorize, not learn | Always explain why and what to notice next time |
| Dumping advanced metrics too early | Beginners feel stupid or lost | Reveal detail progressively by player level |
| Over-gamifying learning | Users chase streaks instead of understanding | Keep metrics tied to concepts and recurring mistakes |

## "Looks Done But Isn't" Checklist

- [ ] **Scenario player:** Often missing complete poker context — verify positions, stacks, pot, street, and available actions are all visible.
- [ ] **Instant feedback:** Often missing stable factual grounding — verify explanation matches deterministic evaluation.
- [ ] **Skill adaptation:** Often missing persistent user level — verify language changes after onboarding and remains consistent.
- [ ] **Progress tracking:** Often missing concept tags — verify attempts can be grouped into actionable leak categories.

## Recovery Strategies

| Pitfall | Recovery Cost | Recovery Steps |
|---------|---------------|----------------|
| AI invents poker truth | HIGH | Freeze prompts, add deterministic scoring layer, re-baseline QA cases |
| Scope explosion | MEDIUM | Cut backlog to one end-to-end loop, rewrite requirements around launch goal |
| Weak taxonomy | HIGH | Backfill scenario tags, rebuild analytics mappings, simplify recommendation logic temporarily |

## Pitfall-to-Phase Mapping

| Pitfall | Prevention Phase | Verification |
|---------|------------------|--------------|
| AI invents poker truth | Phase 1 | Same scenario produces consistent judgment across test runs |
| Scope explosion | Phase 1 | Requirements and roadmap stay centered on one MVP loop |
| Player-level mismatch | Phase 2 | Beginner QA can explain outputs back in their own words |
| Weak taxonomy | Phase 1 | Every scenario and attempt has usable category tags |
| Latency breaks loop | Phase 2 | Feedback returns fast enough to preserve training cadence |

## Sources

- https://platform.openai.com/docs/api-reference/responses/retrieve — current model/tool behavior and integration shape
- https://platform.openai.com/docs/assistants/how-it-works — migration and API-boundary caution
- https://supabase.com/docs/guides/auth/passwords — auth flow details and production email caveats
- Competitor public product pages from GTO Wizard, DTO, Poker Sense, Preflop Wizard — feature expectations and training UX patterns
- Local product docs in `docs/` — primary source for product boundary and differentiation

---
*Pitfalls research for: AI poker coaching MVP*
*Researched: 2026-03-18*
