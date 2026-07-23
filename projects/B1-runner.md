# B1 — Runner 📱

**Folder/repo:** `B1_Runner` · **Clone of:** Subway Surfers · **Platforms:** Linux + Android · **Est:** 14 sessions · **Blender:** yes (B1.4 — first Blender feature) · **UE template:** Third Person (Blueprint)

**Why this project:** the bridge into 3D — a real character, a chase camera, and the spawn/recycle/pool pattern that later scales into hordes (D3) and waves (E4). First appearance of the Blender pipeline, feeding assets into a live game instead of abstract exercises. The Third Person template is used deliberately: its mannequin + anims keep the focus on systems, not animation authoring (that's C1).

**Scope — In:** 3-lane auto-runner, jump/slide, segment streaming with pooling, 3 obstacle types, coins + 2 powerups, own Blender prop kit, score/best, Android package.
**Out:** missions/characters/shops, curved world shader, procedural set-dressing beyond slot-based placement.
**Cut line:** powerup count, then obstacle variety — the streaming/pooling core and the Blender kit are the point and are not cuttable.

## Features

### B1.1 — Third-person core & lanes (3)
Auto-run forward; lane switching as smooth interpolation between 3 lanes; jump and slide with collision capsule changes. Character & camera thread starts (→ guided): what the Character class gives you, chase-camera boom setup. Input: keyboard (rep 3 → story) + swipe gestures (touch rep 2 → how-to) through Enhanced Input contexts.

### B1.2 — Track streaming & pooling (4)
Track segments spawned ahead, recycled behind — an **object pool** (first pooling encounter → guided), not spawn/destroy churn: this pattern is load-bearing again in D3 and E4. Obstacle/coin *slots* on each segment filled from simple weighted rules; global speed ramp over distance. Done means: 10+ minutes of running with flat memory and no hitches on segment boundaries.

### B1.3 — Obstacles, pickups & powerups (3)
Three obstacle interactions (jump-over, slide-under, full-lane block), coin lines/arcs placed via segment slots, magnet + score-multiplier powerups with timers and stacking rules. Collision channels/responses done properly (query vs physics, overlap vs block) — the informal collision knowledge from A1 gets formalized here (→ how-to).

### B1.4 — Blender kit #1 (2)
**First Blender feature (→ guided):** model the obstacle set, coin, and 2 track props; UV unwrap; simple texturing per the CONVENTIONS ceiling; export per the Blender contract — **this feature pins the export preset** (units/axes/smoothing verified via a UE round-trip cube) and records it in `KN-blender-export.md`, which every later Blender feature references. Import, `UCX_` collision, material setup, replace the placeholders in-game.

### B1.5 — Game flow, UI & Android (2)
Run flow (start → death → results → restart), score/best with save (rep 3+ → story), HUD + results screen (UI rep → story), Android package (rep 2 → how-to): orientation, touch verification, quick device sanity capture against budgets.

## Project DoD additions
- Pool proven: `stat game`/actor counts flat across 10 minutes; zero runtime SpawnActor for pooled types after warm-up.
- Every visible placeholder replaced by the B1.4 kit or a free asset with an `ASSETS.md` line.
- Swipe and keyboard verified equivalent (same actions, same feel windows).
