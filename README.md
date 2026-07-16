# Game Dev Learning

The planning repo for a **fundamentals-first, single-player** game development learning path in **UE 5.8 + Blender**. One hour every weekday morning; no calendar deadlines — progression is completion-gated. Created 2026-07-17.

This repo holds the roadmap, plans, knowledge notes, and templates — **text only, no LFS**. The UE projects themselves live outside it, one folder + one GitHub repo per project (parent folder defined in [CONVENTIONS.md](CONVENTIONS.md); default `C:\MyFiles\Projects\GDL\`). During sessions this repo stays checked out beside the active project so plans and notes are updated in place.

**The goal:** after finishing the ladder, be able to take up any of the 18 reference games ([SKILL-MATRIX.md](SKILL-MATRIX.md)) as a clone project *without a step-by-step plan* — i.e. operate permanently in what this repo calls story mode.

**Multiplayer is deliberately excluded.** It gets its own roadmap later; the parked `GameDevPractice` repo (EOS sessions/voice work, mid-P0.2) is its seed. Android **packaging** is in scope — cross-platform *play* is not.

## Locked design decisions (2026-07-17 — don't relitigate without new evidence)

1. **Repetition through structure, not side exercises.** ~16 fresh UE projects; core scaffolding is re-implemented every time (no-copy rule, CONVENTIONS rule 1); each skill thread recurs 3–6× across the ladder. No variation challenges, no drill days — **pure ladder, 5 sessions/week**.
2. **Teaching fades with rep count**: Guided (teach + atomic steps) → How-to (goal + constraints) → **Story** (requirement + acceptance criteria, no steps). Mode is chosen per skill from [SKILL-MATRIX.md](SKILL-MATRIX.md) rep counts; story mode *is* the retrieval practice. The capstone (F1) runs entirely in story mode — it is the graduation exam.
3. **Blueprint first; C++ enters at A3.3** (porting the chess rules engine — the port itself is a repetition) and becomes the default for systems from Stage C. Split: logic in C++, content/tuning in Blueprint, layout in UMG.
4. **Blender at game-asset-support level** (props, modular kits, UVs, collision, simple rig/skin/anim loops, retarget) entering at B1.4. No character modeling — free assets cover characters.
5. **One repo per project; clone = resume.** Each UE project is its own git repo with bounded size; this planning repo is separate and text-only. Everything a project needs to open and play is committed to *its* repo (binary assets via LFS). Asset *sources* (Fab library, downloads) stay outside all repos; once imported into a project, the imported copies are committed. Git commands are always run by you, both repos, on your timing.
6. **"2D" games are built as camera-constrained 3D** (no Paper2D detour — the skills must transfer to the 3D ladder).

## Folder map

| File / folder | Purpose |
|---|---|
| [ROADMAP.md](ROADMAP.md) | Level 0 — all projects and features as one-liners with status. The single track. |
| [projects/](projects/) | Level 1 — one brief per ladder project: goal, scope, a paragraph per feature. |
| [features/](features/) | Level 2 — feature plans / user stories, generated on demand via the generator. |
| [PLAN-GENERATOR.md](PLAN-GENERATOR.md) | Reusable instruction set: one invocation → one feature plan or story, mode auto-selected. |
| [CONVENTIONS.md](CONVENTIONS.md) | The 60-minute session protocol, teaching modes & escalation, working rules, repo/LFS rules, Blender pipeline, budgets, DoD, knowledge-note ritual. |
| [SKILL-MATRIX.md](SKILL-MATRIX.md) | The 18 reference games → projects, and skill-thread rep paths that drive teaching-mode selection. |
| [knowledge/](knowledge/) | Personal wiki — one note per finished feature (closed via the from-memory ritual). |
| [templates/](templates/) | `.gitignore` / `.gitattributes` / `.clang-format` / `ASSETS.md` — copied into each new UE project repo (S0 ritual), so nothing is hunted from other repos. |

**Where the UE projects live:** `C:\MyFiles\Projects\GDL\<ProjectFolder>\` — a deliberately short parent path (UE + Windows path-length limits bite in `Intermediate/` and Android builds). Each project is its own GitHub repo named after its folder (`A1_Flappy`, `A2_Clicker`, …). Morning sessions run in either the project folder or this repo; the other side is reached by absolute path.

## The loop (per feature)

1. Pick the **next** feature in [ROADMAP.md](ROADMAP.md) — strict order, no skipping.
2. Generate its plan/story — invocation block in [PLAN-GENERATOR.md](PLAN-GENERATOR.md). The generator decides guided / how-to / story per skill from the matrix.
3. Build it across 1-hour sessions (session protocol in [CONVENTIONS.md](CONVENTIONS.md)). Stuck in story mode → the escalation ladder, never straight to code.
4. Run the Definition of Done; story features additionally get a Claude review against the acceptance criteria.
5. Close the knowledge note — from memory, aloud; Claude transcribes.
6. Claude bumps the ROADMAP status and re-estimates the remainder at project close.

## Relation to GameDevPractice

That repo rehearsed a production model (unified app, titles-as-DLC, EOS coop) and evolved the planning methodology this repo inherits (two-stage plans, fading granularity, atomic steps, knowledge notes, Claude-owned bookkeeping). It is **parked, not dead**: its EOS plugin work resumes as the seed of the multiplayer roadmap after this ladder completes. Nothing here depends on it — the templates and conventions were copied in, adapted.
