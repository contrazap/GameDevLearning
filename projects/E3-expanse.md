# E3 — Expanse

**Folder/repo:** `E3_Expanse` · **Clone of:** the Star Citizen notes — landmark navigation + control-mode abstraction · **Platform:** Windows · **Est:** 14 sessions · **Blender:** landmark props (→ story) · **UE template:** Blank or Flying (C++) — decide at planning

**Why this project:** your two explicit Star Citizen asks, made buildable: (1) *"make the world's areas have recognizable patterns, to find places, quests etc."* — that's landmark-driven world design plus streaming to hold a big space; (2) *simple/complex/automated control systems* — a control-mode abstraction over a flight pawn. No space-sim scope creep: one large zone, one flyable craft, quest-lite tasks.

**Scope — In:** World Partition zone big enough to need streaming, landmark grammar (silhouettes, color codes, skyline anchors) making districts identifiable, POIs with discovery, waypoint/quest-lite tasks navigated by landmarks, flight pawn with three control modes (simple/assisted/complex), streaming perf pass, package.
**Out:** space/planets, NPCs/dialogue, economy, combat, interiors beyond one hangar.
**Cut line:** complex flight mode (simple+assisted floor), then POI count — the landmark grammar working is the point.

## Features

### E3.1 — World Partition zone (4)
**World Partition first encounter (→ guided):** streaming setup, cell/loading-range reasoning, HLOD awareness, and layout planning at distance scales where streaming matters (landscape rep 2 → how-to). Blockout the zone's macro shapes first — distances that read from the air. Done means: fly border to border, streaming invisible, memory sane.

### E3.2 — Landmarks, POIs & waypoints (4)
**The landmark grammar (→ how-to on world-building thread, but the design thinking is the feature):** each district gets a recognizable pattern — silhouette, palette, one skyline anchor visible from neighbors; POIs discovered on approach (name reveal, log entry); quest-lite tasks ("deliver to the red gantry district") navigable **without a minimap** — E1.4's warm-up at full scale. Blender (→ story): 2–3 landmark props. Done means: after 10 minutes of flying, you can be dropped anywhere and know roughly where you are.

### E3.3 — Flight & control modes (4)
**Flight pawn + the control abstraction (→ guided):** 6DOF-lite physics flight; then three input interpretations over the same craft — *simple* (auto-level, speed-clamped, forgiving), *assisted* (stability augmentation, envelope protection), *complex* (direct thruster/attitude authority) — switchable in flight, structured so a mode is a strategy layer, not three hardcoded pawns (the architecture is the lesson; input thread → story). Done means: the same course flown in all three modes feels like three skill ceilings.

### E3.4 — Streaming perf & package (2)
Profiling rep 3 (→ how-to): captures while flying fast across cell boundaries, hitch hunting, budget documentation; package (→ story).

## Project DoD additions
- The no-minimap navigation test: three delivery tasks completed by a player using landmarks only.
- Control modes share one flight model (grep-level check: one physics path, three input strategies).
- Streaming hitches under a stated ms budget in the committed traces.
