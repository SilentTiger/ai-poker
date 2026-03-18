# Requirements: AI Poker

**Defined:** 2026-03-18
**Core Value:** Help beginner-to-intermediate poker players understand their decisions in plain language fast enough that independent practice feels easier and more useful than studying theory alone.

## v1 Requirements

Requirements for initial release. Each maps to roadmap phases.

### Accounts

- [ ] **ACCT-01**: User can create an account with email and password
- [ ] **ACCT-02**: User can sign in and stay signed in across sessions
- [ ] **ACCT-03**: User can sign out safely from the product

### Player Profile

- [ ] **PROF-01**: User can choose a starting skill level manually before training
- [ ] **PROF-02**: User can complete a short onboarding assessment to set an initial skill level
- [ ] **PROF-03**: User profile stores the player’s current level for future sessions

### Scenario Training

- [ ] **SCEN-01**: User can open a curated poker training scenario with visible position, stack, pot, street, board, and prior action context
- [ ] **SCEN-02**: User can choose from the allowed actions for the current training scenario
- [ ] **SCEN-03**: User can complete scenario practice across at least beginner and intermediate difficulty levels
- [ ] **SCEN-04**: User can move to the next practice scenario without leaving the training flow

### Coaching Feedback

- [ ] **COACH-01**: User receives immediate feedback after each decision
- [ ] **COACH-02**: Feedback explains why the action was good, bad, or weaker in natural language
- [ ] **COACH-03**: Feedback language adapts to the player’s current skill level
- [ ] **COACH-04**: First-release coaching stays scoped to the current decision instead of requiring a long freeform chat

### Progress Tracking

- [ ] **PROG-01**: User can view their recent training attempts
- [ ] **PROG-02**: User can see basic performance trends such as completion count and correctness rate
- [ ] **PROG-03**: The system records mistake categories for each attempt so repeated weaknesses can be identified later

### Experience

- [ ] **EXPR-01**: User can use the training experience comfortably on both desktop and mobile web
- [ ] **EXPR-02**: The product returns feedback fast enough to preserve a continuous training rhythm
- [ ] **EXPR-03**: The product does not provide real-time in-game assistance during live poker play

## v2 Requirements

Deferred to future release. Tracked but not in current roadmap.

### Session Review

- **REVW-01**: User can review the most costly mistakes from a completed training session
- **REVW-02**: User receives a short session summary describing recurring leaks

### Personalized Coaching

- **PERS-01**: User receives recommendations for what concept to practice next based on prior mistakes
- **PERS-02**: User receives a small recommended drill set tailored to recurring weaknesses

### Conversational Coaching

- **CHAT-01**: User can ask follow-up “why” questions about a completed scenario
- **CHAT-02**: User can request additional examples when they do not understand an explanation

### AI Opponent Practice

- **BTTL-01**: User can play a multi-hand training session against AI opponents with distinct styles
- **BTTL-02**: User can review flagged key hands after an AI opponent session

## Out of Scope

| Feature | Reason |
|---------|--------|
| Real-time live-play assistance | Violates poker platform rules and conflicts with the learning-first product boundary |
| Automated poker bot play | Opposes the goal of making the user stronger at decision-making |
| Solver-style raw charts/numbers as the primary experience | Weakens the plain-language coaching differentiation |
| Broad “analyze any hand tree” freeform engine in v1 | Adds major complexity before the guided training loop is proven |

## Traceability

Which phases cover which requirements. Updated during roadmap creation.

| Requirement | Phase | Status |
|-------------|-------|--------|
| ACCT-01 | Phase 1 | Pending |
| ACCT-02 | Phase 1 | Pending |
| ACCT-03 | Phase 1 | Pending |
| PROF-01 | Phase 1 | Pending |
| PROF-02 | Phase 1 | Pending |
| PROF-03 | Phase 1 | Pending |
| SCEN-01 | Phase 2 | Pending |
| SCEN-02 | Phase 2 | Pending |
| SCEN-03 | Phase 2 | Pending |
| SCEN-04 | Phase 2 | Pending |
| COACH-01 | Phase 3 | Pending |
| COACH-02 | Phase 3 | Pending |
| COACH-03 | Phase 3 | Pending |
| COACH-04 | Phase 3 | Pending |
| PROG-01 | Phase 4 | Pending |
| PROG-02 | Phase 4 | Pending |
| PROG-03 | Phase 4 | Pending |
| EXPR-01 | Phase 2 | Pending |
| EXPR-02 | Phase 3 | Pending |
| EXPR-03 | Phase 2 | Pending |

**Coverage:**
- v1 requirements: 20 total
- Mapped to phases: 20
- Unmapped: 0

---
*Requirements defined: 2026-03-18*
*Last updated: 2026-03-18 after initialization*
