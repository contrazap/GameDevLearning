# Roadmap

Status legend: ⬜ not started · 📋 plan generated · 🔨 in progress · ✅ done
Estimates are in **1-hour sessions** (Claude-assisted pace). 📱 = the project also ships an Android package. Details per project live in [projects/](projects/).

## Sequencing & pace

- **One track, strict order.** Work the next ⬜ feature, top to bottom. No skipping, no side quests, no variation challenges — repetition comes from the ladder's structure itself ([SKILL-MATRIX.md](SKILL-MATRIX.md)).
- **Pace is 5 sessions/week (weekday mornings).** A missed morning shifts everything; nothing is "behind" because there are no dates.
- **Estimates are provisional.** At each project close, Claude re-estimates the remainder from actual pace (bookkeeping trigger, CONVENTIONS rule 10). Expect the full ladder to be in the 12–18 month range.
- **Teaching mode fades within each thread**: a feature's plan arrives as guided steps, a how-to, or a user story depending on rep counts — see [PLAN-GENERATOR.md](PLAN-GENERATOR.md). Later stages are mostly story mode; that is by design, not thinning effort.

## S0 — Setup — [features/S0-repos-and-spinup.md](features/S0-repos-and-spinup.md)

- ✅ **S0.1** Planning repo on GitHub + the per-project spin-up ritual (templates, verification, first dry run) (1–2)

## Stage A — Engine foundations (Blueprint, placeholder art) — [projects/A1-flappy.md](projects/A1-flappy.md) · [A2](projects/A2-clicker.md) · [A3](projects/A3-chess.md)

**A1 — Flappy** (Flappy Bird · Windows · 8)
- ⬜ **A1.1** Project bootstrap & flap core: pawn, Enhanced Input, gravity impulse, collision death (3)
- ⬜ **A1.2** Pipes, scoring & game flow: spawner, overlap scoring, start/death/restart states (3)
- ⬜ **A1.3** UI, save & first package: UMG HUD + menus, high-score SaveGame, packaged Windows build (2)

**A2 — Clicker 📱** (Cookie Clicker · 10)
- ⬜ **A2.1** Click core & big numbers: UMG-first project, currency, number formatting (2)
- ⬜ **A2.2** Data-driven upgrades: DataTable of buildings/upgrades, purchase logic, per-second income (3)
- ⬜ **A2.3** Timers & offline progress: real-time accrual, timestamped saves, welcome-back summary (2)
- ⬜ **A2.4** First Android package: SDK pipeline, touch input, safe zones, on-device budget capture (3)

**A3 — Chess** (Chess · Windows · 14)
- ⬜ **A3.1** Board & pieces: board data model, 3D board visuals, select + move highlighting (3)
- ⬜ **A3.2** Rules engine in Blueprint: legal moves, check/checkmate, castling/en passant/promotion, hotseat (4)
- ⬜ **A3.3** C++ entry — port the rules engine: first C++ classes, BP↔C++ boundary, the port as a repetition (4)
- ⬜ **A3.4** Chess AI & polish: minimax with material eval in C++, move animation, package (3)

## Stage B — 3D core, Blender enters — [projects/B1-runner.md](projects/B1-runner.md) · [B2](projects/B2-wordscape.md)

**B1 — Runner 📱** (Subway Surfers · 14)
- ⬜ **B1.1** Third-person core & lanes: Character, chase camera, lane switching, swipe + keyboard input (3)
- ⬜ **B1.2** Track streaming & pooling: segment spawn/recycle ahead of the player, object pooling, speed ramp (4)
- ⬜ **B1.3** Obstacles, pickups & powerups: collision responses, coin patterns, timed powerups (3)
- ⬜ **B1.4** Blender kit #1: obstacle + coin + props — model, UV, export/import pipeline, collision setup (2)
- ⬜ **B1.5** Game flow, UI & Android: score/best, death/restart, Android package (2)

**B2 — Wordscape 📱** (Words of Wonders · 8)
- ⬜ **B2.1** Word data & board generation: word-list asset, crossword grid from level data, letter wheel (3)
- ⬜ **B2.2** Drag select & validation: touch drag across letters, word validation, fill/bonus feedback (3)
- ⬜ **B2.3** Progression & Android: level select, stars, save, package (2)

## Stage C — Third-person action (C++ default for systems) — [projects/C1-traversal.md](projects/C1-traversal.md) · [C2](projects/C2-souls-arena.md) · [C3](projects/C3-stealth-ops.md)

**C1 — Traversal** (Prince of Persia: WW · Windows · 20)
- ⬜ **C1.1** Movement & camera feel: C++ character base, CharacterMovement tuning, camera boom/lag (4)
- ⬜ **C1.2** Animation pipeline: retarget free anim sets, AnimBP, locomotion blendspace, montages (5)
- ⬜ **C1.3** Vault & ledge climb: traces, climb states, root motion / motion warping (5)
- ⬜ **C1.4** Wall run & checkpoints: wall-run movement mode, checkpoint save/restore (3)
- ⬜ **C1.5** Blender kit #2 & gauntlet level: modular greybox kit on grid, a traversal gauntlet, package (3)

**C2 — Souls arena** (Dark Souls 2 · Windows · 20)
- ⬜ **C2.1** Melee core: weapon traces, damage, hit reactions, stamina, dodge i-frames (5)
- ⬜ **C2.2** Lock-on & camera: target acquisition/switching, lock-on camera and movement mode (3)
- ⬜ **C2.3** Enemy AI: Behavior Trees, perception, patrol/aggro/reset, attack selection (5)
- ⬜ **C2.4** Boss, death loop & bonfire: boss phases + telegraphs, death/respawn, rest point saves (4)
- ⬜ **C2.5** Blender weapons, VFX & package: 2–3 weapons with sockets, first Niagara impacts, package (3)

**C3 — StealthOps** (Project IGI, GTFO solo, PUBG gunplay · Windows · 18)
- ⬜ **C3.1** FPS core & weapons: first-person camera/arms, hitscan + projectile, ADS, ammo/reload (5)
- ⬜ **C3.2** AI alert states: sight/hearing perception, patrol → investigate → combat → search (5)
- ⬜ **C3.3** Darkness & flashlight: lighting strategy, light-aware detection (3)
- ⬜ **C3.4** Objectives & mission flow: objectives, alarm consequences, extraction, results screen (3)
- ⬜ **C3.5** Audio/VFX pass & package: MetaSounds basics, muzzle/impact effects, package (2)

## Stage D — Systems & simulation — [projects/D1-farm.md](projects/D1-farm.md) · [D2](projects/D2-survival.md) · [D3](projects/D3-horde.md)

**D1 — Farm 📱** (HayDay · 12)
- ⬜ **D1.1** Grid placement & crops: tap-to-place, growth timers, harvest loop, touch UX (4)
- ⬜ **D1.2** Production chains: processing buildings, queues, recipes, storage limits (3)
- ⬜ **D1.3** Economy & orders: coins, order board, data-driven balance (3)
- ⬜ **D1.4** Offline progress & Android: offline accrual, package (2)

**D2 — Survival** (Don't Starve Together 3D topdown, Zomboid · Windows · 20)
- ⬜ **D2.1** Top-down core & harvesting: top-down controller/camera, resource nodes, tool gathering (4)
- ⬜ **D2.2** Inventory & equipment: data-driven inventory in C++, slots/stacking, equip effects, containers (5)
- ⬜ **D2.3** Crafting & building: recipes, crafting UI, placeable structures (4)
- ⬜ **D2.4** Needs, day/night & spawn director: hunger/sanity-lite, darkness danger, paced spawning (3)
- ⬜ **D2.5** World save/load: full world-state serialization — the deepest save rep (4)

**D3 — Horde 📱** (Vampire Survivors · 16)
- ⬜ **D3.1** Top-down core & auto-attack: fixed camera, movement, auto-targeting weapon (3)
- ⬜ **D3.2** Hordes at scale: mass spawning, pooling, instanced rendering, C++ hot paths (5)
- ⬜ **D3.3** Profiling reps: Unreal Insights, stat toolkit, find-and-fix bottleneck cycles (3)
- ⬜ **D3.4** Level-ups & meta progression: upgrade draft, run currency, persistent unlocks (3)
- ⬜ **D3.5** Juice & package: numbers, screen feedback, sfx; Android package (2)

## Stage E — Vehicles, worlds & scale — [projects/E1-offroad.md](projects/E1-offroad.md) · [E2](projects/E2-chained.md) · [E3](projects/E3-expanse.md) · [E4](projects/E4-micro-rts.md)

**E1 — Offroad** (SnowRunner · Windows · 16)
- ⬜ **E1.1** Landscape & terrain materials: sculpt, paint layers, mud/traction zones (4)
- ⬜ **E1.2** Chaos vehicle: rig, torque/traction tuning, vehicle camera, engine audio (5)
- ⬜ **E1.3** Winch & recovery: physics constraints, cable, stuck-detection, recovery loop (4)
- ⬜ **E1.4** Cargo missions & package: load/deliver loop, landmark-based map reading, package (3)

**E2 — Chained** (Chained Together, solo · Windows · 8)
- ⬜ **E2.1** Chain physics & constraints: player↔object chain, constraint tuning, stability (4)
- ⬜ **E2.2** Momentum puzzles & package: swing/drag puzzles, small level, package (4)

**E3 — Expanse** (Star Citizen notes: landmarks + control modes · Windows · 14)
- ⬜ **E3.1** World Partition zone: streaming setup, layout planning, distances that read (4)
- ⬜ **E3.2** Landmarks, POIs & waypoints: recognizable-pattern zone design, discovery, quest-lite tasks (4)
- ⬜ **E3.3** Flight & control modes: flight pawn with simple/complex/assisted control abstraction (4)
- ⬜ **E3.4** Streaming perf & package: budgets while flying, package (2)

**E4 — MicroRTS** (Age of Empires · Windows · 18)
- ⬜ **E4.1** RTS camera & selection: edge-scroll camera, marquee select, selection decals, order routing (4)
- ⬜ **E4.2** Unit movement at scale: navmesh crowds, avoidance, formation-lite group moves (5)
- ⬜ **E4.3** Economy & production: gather/dropoff, build placement, training queues (4)
- ⬜ **E4.4** Combat & fog of war: auto-acquire combat, simple fog-of-war (3)
- ⬜ **E4.5** Skirmish loop & package: win/lose, wave-based enemy AI, package (2)

## Stage F — Capstone — [projects/F1-capstone.md](projects/F1-capstone.md)

**F1 — Capstone** (your pick of the 18 · 20) — **entirely story mode; this is the graduation exam**
- ⬜ **F1.1** Concept & spec: pick the title, write the slice spec with cut lines (2)
- ⬜ **F1.2** Core loop slice: the 10 minutes that make it *that game* (6)
- ⬜ **F1.3** Content & systems pass: enemies/levels/data to make the loop repeatable (6)
- ⬜ **F1.4** Front end, save & settings: menus, options, persistence (3)
- ⬜ **F1.5** Perf, polish & ship: profiling pass, budgets, packaged Windows (+📱 if the title fits) (3)
