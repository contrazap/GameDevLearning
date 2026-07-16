# C1 — Traversal

**Folder/repo:** `C1_Traversal` · **Clone of:** Prince of Persia: Warrior Within (traversal half) · **Platform:** Windows · **Est:** 20 sessions · **Blender:** yes (C1.5) · **UE template:** Third Person (**C++**)

**Why this project:** Stage C's foundation — movement feel and the animation pipeline are the two deepest first-encounters left, and everything after (souls combat, FPS, top-down games) stands on them. From here, **C++ is the default for systems** (CONVENTIONS rule 3): the character and its movement logic live in C++, Blueprint holds assets and tuning. Combat is deliberately absent — it gets its own project (C2).

**Scope — In:** tuned run/sprint/jump feel, chase camera with lag/zones, retargeted free animation set, AnimBP with locomotion blendspace + montages, vault, ledge grab/climb, wall run, checkpoints, a greybox traversal gauntlet from an own Blender kit, packaged build.
**Out:** combat of any kind, time-rewind mechanic, mobile controls (PoP touch variant = post-roadmap elective).
**Cut line:** wall run, then ledge-shimmy breadth — vault + ledge climb + feel are not cuttable.

## Features

### C1.1 — Movement & camera feel (4)
C++ character base (C++ rep 3 → how-to): CharacterMovement deep-dive — what the component actually simulates, and tuning acceleration/braking/gravity/air control until stopping, turning, and jumping *feel intentional*. Camera boom lag, socket offsets, FOV kick on sprint. Character & camera thread rep 2 (→ guided, this is the feel deep-dive). Done means: a greybox loop that's fun to just run around in.

### C1.2 — Animation pipeline (5)
**The big first encounter (→ guided):** bring in a free humanoid animation set (Game Animation Sample / Fab packs — pin the choice at planning, ⚠️ verify availability), retarget to the project skeleton, build the AnimBP: locomotion state machine, blendspace (speed/direction), jump states, montage slots for one-off actions. This is the pipeline every later character project reuses; the KN note here becomes the most-referenced note in the repo.

### C1.3 — Vault & ledge climb (5)
Traces detect vaultable obstacles and ledge edges; climb states move the character with **root motion / motion warping** (→ guided, ⚠️ verify Motion Warping plugin state in 5.8): mantle-up, ledge hang, climb-over. The state handoffs (movement mode ↔ montage ↔ collision) are the real lesson. Done means: approach any kit obstacle at speed and the right move fires without jank.

### C1.4 — Wall run & checkpoints (3)
Wall run as a custom movement behavior (wall detection, gravity reduction, arc, dismount) — traversal rep 2 (→ how-to). Checkpoints: touch → save transform/state, death (kill volumes) → restore. Save thread rep 4+ (→ story).

### C1.5 — Blender kit #2 & gauntlet level (3)
Modular greybox kit in Blender (Blender rep 2 → how-to): wall/ledge/platform pieces on a strict grid so they snap in UE; export per the pinned B1.4 contract. Assemble a traversal gauntlet that chains every mechanic, add checkpoint pacing, package (→ story).

## Project DoD additions
- Feel sign-off: sprint-jump-vault-climb-wallrun chain executable without stopping, and it *feels* like PoP, not like a checklist.
- AnimBP has no logic that belongs in C++ (anim graph reads state, doesn't decide it).
- Kit pieces snap on grid with zero manual nudging.
