# A1 — Flappy

**Folder/repo:** `A1_Flappy` · **Clone of:** Flappy Bird · **Platform:** Linux · **Est:** 8 sessions · **Blender:** none · **UE template:** Blank (Blueprint)

**Why this project:** the smallest thing that is still a *complete* game — input, physics, collision, states, score, UI, save, package. Every thread that later carries a 20-session project starts here at its simplest. Built as camera-constrained 3D (fixed side-view camera), not Paper2D (locked decision 6).

**Scope — In:** one bird, endless pipes, score + high score, start/death/restart flow, packaged Linux build, free/placeholder art and sfx.
**Out:** Android (starts at A2.4), parallax art passes, medals/missions.
**Cut line:** if 8 sessions bust, ship without menu polish — flow and save are not cuttable.

## Features

### A1.1 — Project bootstrap & flap core (3)
Spin up the project per the S0 ritual (rep 2 → how-to). Blank Blueprint template, fixed side-view camera, a pawn with placeholder mesh, gravity and a flap impulse bound through **Enhanced Input** (first encounter → guided), ground/ceiling/pipe collision ending the run. Done means: the bird flies and dies believably with tunable gravity/impulse values.

### A1.2 — Pipes, scoring & game flow (3)
Timer-driven pipe spawner with randomized gap, movement toward the player, overlap-based scoring, and the game-state flow — waiting → playing → dead → restart — owned by the **game framework** (GameMode/state, first encounter → guided). First audio cues (score blip, death thud) from free sfx. Done means: an endless, restartable run with a correct score.

### A1.3 — UI, save & first package (2)
UMG (first encounter → guided): in-game score HUD, start screen, game-over panel with score/best. High score persisted via **SaveGame** (first encounter → guided). Then the first **packaged Linux build** — packaging is part of finishing, every project ends with it. Done means: a stranger could download the zip and play.

## Project DoD additions
- Tuning values (gravity, impulse, pipe speed/gap) live as editable defaults, not magic numbers in graphs.
- The packaged build runs on a machine without the engine installed.
