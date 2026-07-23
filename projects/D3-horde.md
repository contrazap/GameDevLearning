# D3 — Horde 📱

**Folder/repo:** `D3_Horde` · **Clone of:** Vampire Survivors · **Platforms:** Linux + Android · **Est:** 16 sessions · **Blender:** none required (free/flat assets fit the genre) · **UE template:** Top Down (C++)

**Why this project:** performance engineering as gameplay — hundreds of simultaneous enemies force the pooling/instancing/profiling disciplines that separate shipped games from tech demos. Also the meta-progression pattern (run upgrades + persistent unlocks) that modern game design leans on.

**Scope — In:** top-down auto-attacking character, hordes (target: hundreds on desktop, device-measured ceiling on Android), pooled + instanced enemies, XP gems → level-up upgrade draft, run timer + boss waves, persistent meta unlocks, deliberate profiling feature, juice pass, packages for both platforms.
**Out:** weapon evolution matrices, character roster, stage variety — one character, ~6 weapons/passives, one stage is the scope.
**Cut line:** weapon count, then meta breadth — the horde-at-scale core and the profiling reps are the point and are not cuttable.

## Features

### D3.1 — Top-down core & auto-attack (3)
Movement + fixed camera (→ story), auto-targeting weapon firing on cooldown at nearest enemy (ranged rep 2 → story), damage numbers, XP gems with magnet pickup (character/animation threads → story: flipbook-style or simple anims — genre-appropriate). 

### D3.2 — Hordes at scale (5)
The scale feature: continuous edge-of-screen spawning from pools (pooling rep 2 → how-to), enemies as lightweight movers (full Character class is too heavy at this count — the architecture decision *is* the lesson), **instanced rendering (guided island):** ISM/HISM or vertex-animation approaches, collision strategy at density (⚠️ verify the 5.8-appropriate technique at planning; consider but don't presume Mass). C++ hot paths (→ story). Done means: target counts hold frame rate, measured not vibed.

### D3.3 — Profiling reps (3)
**Deliberate profiling feature (→ guided):** Unreal Insights traces, `stat` toolkit fluency, GPU vs game-thread diagnosis — then find-and-fix cycles on the real project (and one planted bottleneck if the real ones run out). The skill is *diagnosis*, not memorized fixes. Budget capture on the Android device sets the mobile enemy ceiling honestly.

### D3.4 — Level-ups & meta progression (3)
Level-up pauses → draft of 3 upgrade choices (weapons/passives as data → story), run-end results, persistent currency + permanent unlock shop (save thread → story). The upgrade pool must be table-driven: adding an upgrade row = it appears in drafts.

### D3.5 — Juice & package (2)
The feel pass: hit flashes, damage numbers settling, screen shake (restrained), kill sfx layering, gem vacuum moments; Niagara rep 3 (→ story); packages for Linux + Android with per-platform enemy ceilings from D3.3's measurements (→ story).

## Project DoD additions
- Perf proven by traces committed with the close: desktop target count and device ceiling documented in the KN note.
- Zero per-frame allocations in the horde path (Insights-verified) after warm-up.
- A full run (spawn → scale → boss → death/win → meta spend) completes without editor.
