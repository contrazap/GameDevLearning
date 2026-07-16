# A2 — Clicker 📱

**Folder/repo:** `A2_Clicker` · **Clone of:** Cookie Clicker · **Platforms:** Windows + Android · **Est:** 10 sessions · **Blender:** none · **UE template:** Blank (Blueprint)

**Why this project:** a UI-first game that forces UMG depth, data-driven design, and real persistence — and it is the ideal first Android ship (no 3D perf risk, touch input is trivial). Idle economies also teach the timer/timestamp patterns HayDay (D1) later builds on.

**Scope — In:** click currency, generator/upgrade shop from a DataTable, per-second income, offline progress, autosave, Android package with touch + safe zones, first on-device performance capture.
**Out:** prestige layers, achievements, juice art passes (a little count-up animation is enough).
**Cut line:** offline progress ships before shop breadth — 4 generators with correct math beat 12 with broken curves.

## Features

### A2.1 — Click core & big numbers (2)
The clickable, the currency, and number formatting that survives large values (K/M/B suffixes — the big-number problem is real in idle games). Game framework rep (rep 2 → how-to) even though it's UI-first: GameMode/PlayerController still own the game, widgets present it. UMG layout depth continues guided here (anchors, scale boxes — this must survive phone aspect ratios).

### A2.2 — Data-driven upgrades (3)
**DataTable-driven** generators and upgrades (first data-driven encounter → guided): row structs for cost/base income/growth factor, purchase logic with exponential cost curves, aggregated income per second, and a shop list UI *generated from the table* — adding a row adds a shop entry with zero graph edits. This pattern recurs through D1/D2/E4; learn it clean now.

### A2.3 — Timers & offline progress (2)
Real-time accrual while playing; on save, store a timestamp; on load, pay out the offline delta with a welcome-back summary. Save thread rep 2 (→ how-to): autosave on interval + on quit, load on boot. Done means: kill the app, come back later, the math is right.

### A2.4 — First Android package (3)
First Android encounter (→ guided): validate the SDK toolchain against UE 5.8, package, install, run on the real device. Touch input, finger-sized hit targets, safe-zone handling. Ends with the first **on-device budget capture** (`stat unit`, memory) — this validates/updates the provisional budget table in CONVENTIONS. Done means: the game plays correctly on the phone and the budget table reflects measured reality.

## Project DoD additions
- Shop content is provably data-driven: add a test row, it appears and works with no other edits.
- Offline progress verified against a wall clock, including device reboot.
- CONVENTIONS mobile-budget table updated from the device capture (bookkeeping trigger).
