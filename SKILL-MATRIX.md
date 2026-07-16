# Skill Matrix

Two maps: the 18 reference games → where their load-bearing mechanics are covered, and the **skill threads** → their rep paths across the ladder. The rep paths drive teaching-mode selection (PLAN-GENERATOR procedure 2). Games aren't cloned 1:1 — their mechanics become ladder features; the capstone (F1) clones one of them properly.

## Reference games → coverage

| Game | What we take from it | Covered in |
|---|---|---|
| Flappy Bird | Minimal complete game: input, collision, flow, score | **A1** |
| Cookie Clicker | Idle economy, big numbers, offline progress, UI-first game | **A2** |
| Chess | Turn-based rules engine, board data model, minimax AI | **A3** |
| Subway Surfers | Endless runner, segment streaming, pooling, mobile feel | **B1** |
| Words of Wonders | Word-puzzle data, mobile-first UMG, touch drag | **B2** |
| Prince of Persia: WW | Traversal (vault/ledge/wall-run), movement & camera feel | **C1** (touch-friendly mobile variant = post-roadmap elective) |
| Dark Souls 2 | Lock-on melee, stamina, i-frames, enemy AI, boss & bonfire loop | **C2** |
| Project IGI | FPS gunplay, stealth AI, alert states | **C3** |
| GTFO (solo aspects) | Darkness/flashlight, scarcity, objectives, dread pacing | **C3** (coop = multiplayer roadmap) |
| PUBG | Weapon feel, ADS/ammo discipline, loot instincts | **C3** + D2.2 inventory (BR scale = multiplayer roadmap) |
| HayDay | Production chains, real-time timers, soft economy | **D1** |
| Project Zomboid (3D) | Survival systems, needs, crafting, world persistence | **D2** |
| Don't Starve Together (3D topdown) | Top-down survival, day/night, harvesting | **D2** (coop later) |
| Vampire Survivors | Mass enemies, run upgrades, meta progression, performance | **D3** |
| SnowRunner | Offroad physics, winch, terrain reading, recovery loop | **E1** |
| Chained Together | Physics coupling, constraint platforming (solo) | **E2** (player-to-player chain = multiplayer roadmap) |
| Star Citizen | Landmark-driven world design ("recognizable patterns to find places"), simple/complex/assisted control modes, streaming performance | **E3** |
| Age of Empires | RTS camera/selection, pathing at scale, economy, fog of war | **E4** |

## Skill threads → rep paths

Letters are the **expected** mode at that encounter (G guided · H how-to · S story); the generator derives the live mode from ✅ features + KN `Had to look up:` demotions. `G*` = guided island inside a story feature.

| Thread | Rep path |
|---|---|
| Project spin-up & source control | S0 G → A1.1 H → A2.1 S → every project S |
| Enhanced Input (desktop) | A1.1 G → A3.1 H → B1.1 S → C1.1 S |
| Touch input | A2.4 G → B1.1 H → B2.2 S → D1.1 S |
| Game framework & flow (GameMode/State/restart) | A1.2 G → A2.1 H → B1.5 S → every project S |
| UMG / UI | A1.3 G → A2.1 G(depth) → A2.2 H → B2.1 H → B2.2 S → D1.1 S → onward S |
| Save & persistence | A1.3 G → A2.3 H → B2.3 S → C1.4 S → C2.4 S → D1.4 S → D2.5 G*(world serialization) → D3.4 S |
| Data-driven design (DataTables/DataAssets) | A2.2 G → A3.1 H → B2.1 H → D1.3 S → D2.2 S → E4.3 S |
| C++ engineering | A3.3 G → A3.4 H → C1.1 H → C2.1 S → D2.2 S → D3.2 S → E4.2 S |
| 3D character & camera | B1.1 G → C1.1 G(feel deep-dive) → C2.2 H(lock-on) → D2.1 S → D3.1 S |
| Animation pipeline | C1.2 G → C2.1 H(montages/hit reacts) → C3.1 H(first-person) → D3.1 S |
| Traversal mechanics | C1.3 G → C1.4 H → F1 S(if the title needs it) |
| Melee combat | C2.1 G → C2.4 H → D2.1 S(tool use) |
| Ranged weapons | C3.1 G → D3.1 S(auto-fire) |
| Enemy AI (BT/perception) | C2.3 G → C3.2 H → D2.4 S → D3.2 S(swarm logic) → E4.4 S |
| Spawning, pooling & spawn direction | B1.2 G → D2.4 H(director) → D3.2 H + G*(instancing) → E4.5 S(waves) |
| Profiling & optimization | A2.4 G(first device capture) → D3.3 G(Insights deep) → E3.4 H → F1.5 S |
| Physics constraints | E1.3 G → E2.1 H → E2.2 S |
| Vehicles (Chaos) | E1.2 G → F1 S(if the title needs it) |
| Landscape & world building | E1.1 G → E3.1 G(World Partition) → E3.2 H(landmark design) → F1 S |
| Niagara VFX | C2.5 G → C3.5 H → D3.5 S |
| Audio | A1.2 (cue basics inside guided feature) → C3.5 G(MetaSounds) → D3.5 S → E1.2 S(vehicle loops) |
| Blender asset pipeline | B1.4 G → C1.5 H → C2.5 H(weapons/sockets) → E-stage props S |
| Android packaging | A2.4 G → B1.5 H → B2.3 S → D1.4 S → D3.5 S |
| RTS systems (selection/orders/fog) | E4.1 G → E4.2 G(crowds) → E4.3 H → E4.4 H |
| Flight & control-mode abstraction | E3.3 G → F1 S(if the title needs it) |

**Reading it:** a thread's first entry is always guided no matter the stage — Chaos Vehicles at E1.2 is a first encounter even though it's late. Conversely, by Stage C the everyday threads (input, framework, UI, save, packaging) are stories — if a Stage D plan arrives with steps for a save system, the generator misfired (PLAN-GENERATOR principle 4).
