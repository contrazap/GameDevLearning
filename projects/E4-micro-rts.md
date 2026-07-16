# E4 — MicroRTS

**Folder/repo:** `E4_MicroRTS` · **Clone of:** Age of Empires · **Platform:** Windows · **Est:** 18 sessions · **Blender:** none required (free low-poly packs fit) · **UE template:** Top Down (C++)

**Why this project:** the ladder's integration finale before the capstone — many-entity control, pathing at scale, economy, and fog of war, composed. RTS code is where the C++/data-driven/AI threads prove they've compounded: most arrives as stories.

**Scope — In:** RTS camera, marquee selection + control groups, order routing (move/gather/build/attack), navmesh crowd movement with formation-lite group moves, one resource economy (gather → dropoff), building placement + training queues, auto-acquire combat, simple fog of war, a skirmish vs. wave-based AI with win/lose, package.
**Out:** multiple factions/ages, tech trees, walls/siege, real opponent AI (waves suffice), unit variety beyond ~4.
**Cut line:** fog of war visual polish (binary reveal floor), then formation quality — selection/orders/pathing at scale are not cuttable.

## Features

### E4.1 — RTS camera & selection (4)
**RTS-specific first encounter (→ guided):** edge-scroll/zoom camera pawn, marquee selection (screen→world), selection decals and UI, control groups, order routing to many units at once (the command → units seam that everything else plugs into). Enhanced Input rep (→ story).

### E4.2 — Unit movement at scale (5)
**Crowds (→ guided on the crowd layer, C++ → story):** navmesh movement for dozens of units without clumping or lane-fighting — avoidance approach (⚠️ verify 5.8 options at planning: detour crowd / custom steering), arrival spreading, formation-lite group moves (line/box), and the perf reality of many movers (pooling/instancing thread rep → story from D3's lessons). Done means: 50 units cross the map and arrive like an army, not a centipede.

### E4.3 — Economy & production (4)
Gatherer loop (resource → carry → dropoff, auto-reassign), building placement (placement-grid rep 3 → story), training queues with costs (data thread → story: units/buildings/costs all table-driven), population-lite cap. 

### E4.4 — Combat & fog of war (3)
Auto-acquire combat with stances-lite (AI thread rep 5 → story), target priorities; **fog of war (→ guided island):** vision-based reveal, hidden vs. shroud states, an implementation honest about its cost (⚠️ approach options at planning: RT-based vs. grid). 

### E4.5 — Skirmish loop & package (2)
Win/lose conditions, timed enemy wave assaults (spawn-direction thread → story), a 15-minute skirmish arc, package (→ story).

## Project DoD additions
- The 50-unit order stress: select-all → cross-map move → gather reassignment, no stuck units, frame budget held.
- Adding a unit type is a data exercise (table row + assets), zero new code paths.
- A full skirmish is winnable and losable — the waves actually threaten the economy.
