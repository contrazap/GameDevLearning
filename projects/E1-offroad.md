# E1 — Offroad

**Folder/repo:** `E1_Offroad` · **Clone of:** SnowRunner · **Platform:** Linux · **Est:** 16 sessions · **Blender:** attachments/props (→ story) · **UE template:** Vehicle or Third Person (C++) — decide at planning against 5.8's vehicle template state

**Why this project:** physics as the gameplay — Chaos Vehicles, terrain that punishes, and constraint-based tools (winch). SnowRunner's genius is that *the map is the enemy*; that needs real landscape skills, which also open Stage E's world-building thread.

**Scope — In:** sculpted/painted landscape with mud/traction zones, one drivable truck (free/Fab vehicle asset; own Blender attachments), Chaos Vehicles rig + tuning, winch with physics constraint + cable, stuck-detection and recovery loop, cargo load/deliver missions, landmark-based map reading (no minimap — signposts and silhouettes), package.
**Out:** vehicle roster, damage simulation, fuel economy depth, seasons/DLC anything, deformable mud (fake it with material + physics zones).
**Cut line:** cargo physics (strapped-static floor), then mission count — the drive-stuck-winch-recover loop is the point.

## Features

### E1.1 — Landscape & terrain materials (4)
**Landscape first encounter (→ guided):** sculpt a terrain with roads, slopes, water crossings, and trouble; paint layers (dirt/grass/rock/mud) with a landscape material; mud zones as gameplay via physical materials modifying traction. Foliage-lite for readability. Done means: you can *read* where it's safe to drive from the driver's seat.

### E1.2 — Chaos vehicle (5)
**Chaos Vehicles first encounter (→ guided):** wheel setup, torque curves, differential/gearing basics, tire friction against the E1.1 physical materials, chase + hood cameras, engine audio loops (audio → story). Tuning until slow, deliberate offroading feels tense rather than sluggish (the SnowRunner feel bar). ⚠️ Verify Chaos Vehicles API state in 5.8 at planning.

### E1.3 — Winch & recovery (4)
**Physics constraints first encounter (→ guided):** winch as a constraint between truck and anchor points (trees/rocks/other), visual cable (spline or cable component), tension limits, attach/detach interaction; stuck detection (wheel slip vs. movement) surfacing the recovery loop. Blender rep (→ story): anchor/attachment props. Done means: getting stuck is recoverable and *satisfying*.

### E1.4 — Cargo missions & package (3)
Cargo pickup → strapped load → delivery objectives, load affecting handling (mass), mission flow (→ story), and **landmark-based navigation**: the map readable by silhouettes, signage, and terrain features — a deliberate warm-up for E3.2's landmark design thread. Package (→ story).

## Project DoD additions
- Traction zones provably differ (measured wheel-slip on each surface type).
- The winch works on every anchor type and never explodes the physics (constraint tuning documented in KN).
- A first-time driver can find the delivery point without a GPS overlay — landmarks suffice.
