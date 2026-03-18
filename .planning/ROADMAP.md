# Roadmap: AI Poker

**Created:** 2026-03-18
**Depth:** standard
**Coverage:** 20/20 v1 requirements mapped

## Phases

- [ ] **Phase 1: Player Access and Level Setup** - Players can create an account, establish a starting skill level, and return with that level preserved.
- [ ] **Phase 2: Guided Scenario Practice** - Players can work through curated poker scenarios across supported difficulty levels on desktop and mobile web.
- [ ] **Phase 3: Instant Coaching Feedback** - Players receive immediate, plain-language decision feedback matched to their current skill level.
- [ ] **Phase 4: Progress Visibility and Mistake Tracking** - Players can review attempts, see basic trends, and retain structured mistake data for future improvement loops.

## Progress

| Phase | Plans Complete | Status | Completed |
|-------|----------------|--------|-----------|
| 1. Player Access and Level Setup | 0/0 | Not started | - |
| 2. Guided Scenario Practice | 0/0 | Not started | - |
| 3. Instant Coaching Feedback | 0/0 | Not started | - |
| 4. Progress Visibility and Mistake Tracking | 0/0 | Not started | - |

## Phase Details

### Phase 1: Player Access and Level Setup
**Goal**: Players can enter the product, set an initial skill level, and keep that profile across sessions.
**Depends on**: Nothing
**Requirements**: ACCT-01, ACCT-02, ACCT-03, PROF-01, PROF-02, PROF-03
**Success Criteria** (what must be TRUE):
1. A new player can create an account with email and password, then sign in successfully.
2. A signed-in player stays signed in across browser sessions until they choose to sign out.
3. A new player can either choose a starting skill level manually or complete a short onboarding assessment before training.
4. A returning player sees their previously stored skill level applied in later sessions.
5. A player can sign out safely from the product at any time.
**Plans**: TBD

### Phase 2: Guided Scenario Practice
**Goal**: Players can move through realistic, self-directed poker training scenarios in a continuous web practice flow.
**Depends on**: Phase 1
**Requirements**: SCEN-01, SCEN-02, SCEN-03, SCEN-04, EXPR-01, EXPR-03
**Success Criteria** (what must be TRUE):
1. A player can open a curated training scenario and see position, stack, pot, street, board, and prior action context before choosing a move.
2. A player can choose from the allowed actions for the current scenario and submit a decision within the training flow.
3. A player can practice across at least beginner and intermediate scenario difficulty levels.
4. A player can continue directly to the next scenario without leaving the practice loop.
5. The training flow is usable on both desktop and mobile web and only offers offline training scenarios, not live-play assistance.
**Plans**: TBD

### Phase 3: Instant Coaching Feedback
**Goal**: Players immediately understand the quality of their decision in plain language matched to their current level.
**Depends on**: Phase 2
**Requirements**: COACH-01, COACH-02, COACH-03, COACH-04, EXPR-02
**Success Criteria** (what must be TRUE):
1. After each scenario decision, a player receives feedback fast enough that practice still feels continuous.
2. Feedback tells the player whether the chosen action was good, bad, or weaker for the spot.
3. Feedback explains the reasoning in natural language rather than solver-style raw output.
4. The explanation style adjusts to the player’s current skill level so beginners and improving players both get appropriate coaching.
5. Coaching stays scoped to the current decision instead of requiring a long freeform chat to continue.
**Plans**: TBD

### Phase 4: Progress Visibility and Mistake Tracking
**Goal**: Players can see evidence of improvement and the product retains structured mistake data for future coaching loops.
**Depends on**: Phase 3
**Requirements**: PROG-01, PROG-02, PROG-03
**Success Criteria** (what must be TRUE):
1. A player can review their recent training attempts from within the product.
2. A player can see basic performance trends including practice volume and correctness rate.
3. Each attempt stores mistake categories so repeated weaknesses can be identified later.
**Plans**: TBD
