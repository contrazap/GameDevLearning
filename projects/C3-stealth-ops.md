# C3 — StealthOps

**Folder/repo:** `C3_StealthOps` · **Clone of:** Project IGI + GTFO (solo) + PUBG gunplay · **Platform:** Windows · **Est:** 18 sessions · **Blender:** props as needed (→ story) · **UE template:** First Person (C++)

**Why this project:** ranged combat and *stateful* stealth AI — the other half of action-game literacy. GTFO contributes the darkness/scarcity/objective pressure (its coop is excluded — multiplayer roadmap); IGI the patrol-stealth loop; PUBG the weapon-handling discipline (ADS, ammo scarcity, recoil control).

**Scope — In:** first-person weapon handling (hitscan + projectile, ADS, reload, ammo scarcity), stealth AI with alert states and propagation, darkness + flashlight as a mechanic, objective-driven mission with alarm consequences and extraction, MetaSounds + Niagara pass, packaged mission build.
**Out:** inventory/loot systems (D2), multiple missions, difficulty modes, any coop hooks.
**Cut line:** projectile weapon (hitscan-only floor), then search-state richness — alert-state correctness is not cuttable.

## Features

### C3.1 — FPS core & weapons (5)
First-person camera/arms (animation rep 3 → how-to), weapon base in C++ (ranged first encounter → guided): hitscan with spread/recoil patterns, one projectile weapon with drop, ADS with FOV/sensitivity shift, reload discipline (magazines, not pools — GTFO-style scarcity), damage falloff. Done means: shooting feels deliberate and ammo feels precious.

### C3.2 — AI alert states (5)
The stealth brain (AI rep 2 → how-to, but the *state machine* is the new part): unaware → suspicious (investigate stimulus) → alerted (combat) → searching (lost target) → return-to-post, with sight cones affected by light level, hearing events from shots/footsteps, and **alert propagation** between nearby guards (GTFO's wake-the-room dread). Done means: a patrol can be ghosted, distracted, or erupted — player's choice.

### C3.3 — Darkness & flashlight (3)
Darkness as the mission's resource: lighting strategy for a dark facility, player flashlight (the one dynamic shadow light — budget honesty even on desktop), AI sight scaled by illumination (→ guided island inside a how-to feature), light-discipline gameplay (using light reveals you). 

### C3.4 — Objectives & mission flow (3)
Objective chain (reach → interact → retrieve → extract), alarms with consequences (reinforcement waves, locked-down doors), extraction trigger, mission results screen (time, kills, alarms). Game-flow thread (→ story). Done means: a 10-minute mission with a beginning, decisions, and an end.

### C3.5 — Audio/VFX pass & package (2)
**MetaSounds first encounter (→ guided):** gunshot layers, tails by room size (simple), footsteps by surface; Niagara rep 2 (→ how-to): muzzle flash, impacts by material; package (→ story).

## Project DoD additions
- Alert-state transitions logged and provably correct (no teleporting knowledge, no stuck searchers).
- A full-ghost run and a full-loud run are both completable — the mission respects both verbs.
- Flashlight ON measurably changes AI detection distance.
