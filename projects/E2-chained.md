# E2 — Chained

**Folder/repo:** `E2_Chained` · **Clone of:** Chained Together (solo variant) · **Platform:** Linux · **Est:** 8 sessions · **Blender:** none required · **UE template:** Third Person (C++)

**Why this project:** constraint physics under continuous player stress — a chain that must *never* explode while being yanked, swung, and snagged. The original's player-to-player chain is a multiplayer mechanic; the solo variant (player chained to a heavy companion object) keeps every physics lesson and stays in scope. Short project by design: Stage E's breather that still adds a thread rep.

**Scope — In:** segmented physics chain between player and a heavy object, constraint tuning for stability at speed, chain interactions (snagging, wrapping-lite, weight to haul), momentum/swing puzzles in a small vertical level, package.
**Out:** multiplayer chain, chain cutting/length upgrades, ragdoll gymnastics.
**Cut line:** wrapping behavior (snag-only floor) — chain stability under abuse is not cuttable.

## Features

### E2.1 — Chain physics & constraints (4)
The chain as constrained bodies (physics constraints rep 2 → how-to): segment count vs. stability trade-offs, iteration/substep tuning, mass ratios that don't fight the character, attachment to the character without corrupting movement. The physical companion object (a weight/anchor with real mass the player drags). Done means: sprint, jump, and yank for 5 minutes — no explosion, no soft-lock.

### E2.2 — Momentum puzzles & package (4)
A small level of chain-verbs (physics thread rep 3 → story): haul the weight uphill, swing it for momentum, lower it as a counterweight, snag hazards to avoid. Checkpoints (→ story), package (→ story). Done means: three puzzles each forced a different chain verb.

## Project DoD additions
- Stability torture test scripted and passing (automated 2-minute abuse sequence, no NaNs/explosions in logs).
- Constraint tuning decisions (segment count, iterations, damping) recorded in the KN note with the *why* — this is reference material for any future physics feature.
