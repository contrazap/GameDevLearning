# D2 — Survival

**Folder/repo:** `D2_Survival` · **Clone of:** Don't Starve Together (3D topdown) + Project Zomboid · **Platform:** Linux · **Est:** 20 sessions · **Blender:** props as needed (→ story) · **UE template:** Top Down or Third Person (C++) — decide at planning

**Why this project:** the systems-integration boss fight of the ladder — inventory, crafting, needs, time-of-day, and spawn direction all *interlocking*, then the deepest save/load of the roadmap persisting it all. Individually most threads arrive as stories; the integration is the new skill.

**Scope — In:** top-down character + camera, harvestable resource nodes with tools, full data-driven inventory (slots/stacking/containers) in C++, equipment with effects, crafting with stations, placeable structures, hunger + a darkness danger, day/night cycle, spawn director, complete world save/load.
**Out:** procedural world generation (fixed hand-built map — procgen is a post-roadmap elective), farming (D1 owns it), sanity/temperature simulation depth, zombies-as-hordes (D3 owns mass).
**Cut line:** structure variety, then needs count (hunger floor) — inventory depth and world save are not cuttable.

## Features

### D2.1 — Top-down core & harvesting (4)
Top-down controller/camera (character thread → story), resource nodes (trees/rocks/bushes) with health, tool-typed gathering (melee thread rep 3 → story: an axe swing is a damage window you already know), yields to inventory-to-be. 

### D2.2 — Inventory & equipment (5)
**The system rep that PUBG/Zomboid/DST all share:** items as data (DataTable/DataAssets → story), a C++ inventory component — slots, stacking, moving, splitting, containers (chests share the component) — equipment slots applying stat/tool effects, drag-drop UMG inventory (UI → story with a **guided island** only if drag-drop widget mechanics demand it). Acceptance criteria are strict: this component must be reusable by D3/F1 conceptually, not by copy-paste.

### D2.3 — Crafting & building (4)
Recipes as data consuming inventory contents; crafting UI with availability states; stations gating recipe tiers; placeable structures on a placement grid (rep 2 of D1.1's island → story: ghost preview, validity checks, build). 

### D2.4 — Needs, day/night & spawn director (3)
Hunger draining/restored by food, day/night cycle driving light + danger (night monsters near the player — DST's core threat), a **spawn director** pacing hostiles by time-of-day and player location (spawning thread rep 2 → how-to). Done means: night one is scary, night five is manageable — because the player progressed.

### D2.5 — World save/load (4)
**The deepest save rep — story with a guided island on serialization architecture:** every actor's relevant state (nodes' remaining health, dropped items, containers' contents, structures, needs, time-of-day, director state) captured and restored — quit anywhere, resume identically. The island teaches the architecture decision (what is state vs. what is content); the implementation is yours.

## Project DoD additions
- Save/load round-trip is provably lossless: scripted checklist of 15 world facts verified after reload.
- Inventory component contains zero game-specific item knowledge (grep check: no item names in C++).
- A 20-minute session has a survival arc: scarcity → tooling → security.
