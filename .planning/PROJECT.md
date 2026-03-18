# AI Poker

## What This Is

AI Poker is a plain-language AI poker coach for Texas Hold'em players who want to improve without getting buried in solver charts, jargon, or expensive one-on-one coaching. The first release focuses on guided scenario practice with instant AI explanation so beginner-to-intermediate players can learn why a decision is right or wrong and build real intuition instead of playing by feel.

## Core Value

Help beginner-to-intermediate poker players understand their decisions in plain language fast enough that independent practice feels easier and more useful than studying theory alone.

## Requirements

### Validated

(None yet — ship to validate)

### Active

- [ ] Players can complete skill-leveled poker training scenarios and receive immediate natural-language feedback on their decisions.
- [ ] The product adapts explanations to the player's level so beginners are not overwhelmed and improving players are not talked down to.
- [ ] Players can learn through self-directed practice without needing live opponents, fixed schedules, or expensive human coaching.

### Out of Scope

- Real-time in-game advice during live poker sessions — violates platform rules and conflicts with fair-play constraints.
- Automated poker bots that play on the user's behalf — directly opposes the goal of helping users improve their own decision-making.
- Solver-style output that only returns charts, numbers, or raw ranges — the product's differentiation is explanation and understanding, not dumping analysis output.

## Context

The target audience spans three segments: beginners who just learned the rules and do not know how to study, intermediate players who know they are making mistakes but cannot diagnose them, and stronger players who already use advanced tools and want faster strategy internalization. The near-term focus is beginners to intermediates because that best matches the product promise of "speaking human" and lowering the learning barrier.

The product idea comes from a clear market gap in poker training: existing tools assume prior theory knowledge, solver outputs are hard to interpret, human coaching is expensive, and normal play does not provide enough hands or enough targeted repetition to build intuition quickly. The v1 wedge is scenario practice with instant AI feedback, while broader ideas like AI opponents, session review, and personalized training recommendations remain part of the longer-term vision described in the source documents.

The experience should feel like a coach, not a calculator. Users should see a realistic hand context, make a decision, and immediately understand what happened and why in language matched to their current level. Terminology support and adaptive explanation style are important differentiators, especially for new players who would otherwise bounce off technical tools.

## Constraints

- **Domain**: No real-time assistance during live play — poker platforms prohibit this behavior and it would create compliance and account-risk issues.
- **Product Scope**: v1 centers on scenario practice with instant explanation — this is the fastest path to validating the core coaching value before expanding into full AI battle or post-session review loops.
- **Audience**: Optimize first for beginner-to-intermediate players — this is where plain-language teaching and structured guidance create the most leverage.
- **Experience**: Explanations must be understandable without solver literacy — otherwise the product collapses into the same complexity that current tools already impose.

## Key Decisions

| Decision | Rationale | Outcome |
|----------|-----------|---------|
| Start v1 with scenario practice plus instant AI analysis | Fastest way to validate whether users learn better with plain-language coaching | — Pending |
| Prioritize beginner-to-intermediate players first | Best fit for the core differentiation of adaptive explanation and reduced jargon | — Pending |
| Treat AI battle, review, and personalized push as later-scope modules | Valuable long-term loop, but not required to prove the initial product value | — Pending |
| Explicitly exclude real-time assistance and botting | Required for product integrity, compliance, and alignment with learning goals | — Pending |

---
*Last updated: 2026-03-18 after initialization*
