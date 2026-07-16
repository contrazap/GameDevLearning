# Conventions

Shared rules for all plans and sessions. The plan generator reads this file — change it here and every future plan follows. Adapted from GameDevPractice's conventions (the rules born from real friction are kept; multiplayer rules are dropped).

## IDs, files, statuses

- Project ID: `A1`…`F1` (stage letter + number). Feature ID: `A1.2`. Sub-split: `A1.2a/b`.
- Project brief: `projects/A1-flappy.md`. Feature plan/story: `features/A1.2-short-slug.md`. Knowledge note: `knowledge/KN-short-topic.md`.
- UE project folder & GitHub repo name: `A1_Flappy` style — stage prefix keeps folders sorted in ladder order.
- ROADMAP statuses: ⬜ not started · 📋 plan generated · 🔨 in progress · ✅ done.
- A **session** = one 60-minute weekday-morning block. All estimates are in these.

## Repos & filesystem

1. **Two kinds of repo.** This planning repo (text only, **no LFS**) and one repo **per UE project**. Never nest: no UE project inside this repo, no `.git` inside a project other than its own.
2. **Projects parent folder — single source of truth:** `C:\MyFiles\Projects\GDL\`. Short on purpose: UE + Windows path-length limits bite in `Intermediate/` and Android builds. Plans and notes reference project files as `A1_Flappy/Source/...` — always relative to this parent.
3. **Per-project repo contract (S0 ritual):** created from [templates/](templates/) — `.gitignore`, `.gitattributes` (LFS routing), `.clang-format`, `ASSETS.md` at the project repo root. Verified with `git check-ignore` + `git add -n` before the first commit.
4. **Clone = resume.** Everything the project needs to open and play is committed to its repo: authored work *and* imported asset copies (binaries via LFS). Asset sources (Fab library, zips, Quixel) stay outside all repos.
5. **Import lean.** When adding a marketplace/Fab pack, migrate only the folders the project actually uses. Keeps repos, LFS quota, and editor load times sane. Each import gets one line in the project's `ASSETS.md` (source, version, license, folders taken).
6. **LFS quota is per GitHub account, not per repo.** Splitting repos bounds repo *size*, not quota. Expect to need a paid LFS data pack around Stage B–C; the check lives in S0.
7. **Git is [You], always.** Claude never commits or pushes. Recommended minimum: commit at each session close, push both repos at each feature close — the clone-anywhere property depends on it.
8. **Sessions run beside both folders.** Work from the project folder or from this repo; the other side is reached by absolute path. Claude updates plans/KN notes here and code there in the same session.

## The 60-minute session

| Minutes | What happens |
|---|---|
| 0–5 | **Orient.** Claude reads the active plan's `Next action:` + session log and states today's goal in two sentences. You don't re-read anything. |
| 5–55 | **Work.** One focus. Story mode: you drive, escalation ladder when stuck. Guided/how-to: follow the plan's steps. |
| 55–60 | **Close.** Claude updates the session log + `Next action:`, pre-generates the next session's detail if one is due; you commit (push when ready). |

- **End every session runnable.** Never leave a broken build overnight; if a change can't finish, stash the last step into `Next action:` and revert to green.
- **C++ builds at the edges.** Full rebuilds happen at session start or after close — mid-session prefer Live-Coding-compatible edits. New classes/UFUNCTIONs → plan them as the session's first or last act.
- **No mid-session scope changes.** New ideas go to the session log's `Later:` line; Claude carries them into the project brief at feature close.

## Teaching modes (the fade)

Mode is selected **per skill, per feature** from [SKILL-MATRIX.md](SKILL-MATRIX.md) rep counts and knowledge-note `Had to look up:` lines. One feature document always; its shape varies. Full mechanics in [PLAN-GENERATOR.md](PLAN-GENERATOR.md).

| Mode | When (per skill) | Document contains | Claude's role |
|---|---|---|---|
| **Guided** | 1st encounter | Teach blocks + atomic steps, `Done when:` each | Explains, verifies literals, reviews — **you type** |
| **How-to** | 2nd encounter | Goal + constraints + pointers to your own KN notes; coarse steps | Answers questions, reviews |
| **Story** | 3rd+ encounter | User story + acceptance criteria + references — **no steps** | Consultant on request + mandatory close-out review |

- **Demotion rule:** a skill whose KN note ends with a fat `Had to look up:` gets its next encounter demoted one mode. The fade adapts; it is not a ratchet.
- **Guided islands:** a story feature that touches one genuinely new sub-skill gets a Teach block for that island only — the rest stays story.
- **Escalation ladder (story mode, in order):** ① *Hint* — which system/doc to look at → ② *Concept* — how the mechanism works → ③ *Approach* — design together, you implement → ④ *Pair* — build together. Stuck on the **same wall ~15–20 min** → escalate one level. Claude never jumps to code, and never volunteers a level you didn't reach.
- **Story close-out review is mandatory:** Claude reviews the implementation against the acceptance criteria + a quality pass (naming, data-driven where it should be, perf smells). Findings are discussed, not silently fixed — the fix is yours.
- **References policy:** official docs and engine sample content first; videos only when uniquely good, with watch time stated (a 40-minute video is most of a session).

## Working rules

1. **No-copy rule (the structural rep).** Core scaffolding — input setup, game framework wiring, HUD shell, save flow, packaging config — is re-implemented in each new project. Allowed references: your own knowledge notes, official docs. Not allowed: opening the old project's implementation side-by-side, pasting from it, or "Claude, do it like last time". Your own Blender assets and downloaded packs may be reused freely — art is not the rep target.
2. **Learning split.** [You] = new concepts, core architecture, every design decision. [Claude] = boilerplate, second instances, debug assistance. [Pair] = hairy integrations. A plan where [Claude] does the interesting parts is a failed plan. The split tilts toward [You] as modes fade — in story mode, [Claude] writes nothing unless the ladder reaches ④.
3. **Implementation split (staged).** Stage A–B: Blueprint throughout, C++ from A3.3 where the plan says. Stage C on: **logic in C++** (systems, save/load, perf-sensitive code), **Blueprint** for content wiring and tuning (`BP_` subclasses holding assets/values), **UMG** for layout (`WBP_`, logic in a C++ `UUserWidget` base), **data** in DataTables/`DA_` assets, never hardcoded.
4. **Editors.** Visual Studio for C++ (IntelliSense/build straight from UBT); VS Code for plans, markdown, Claude Code. Create source files on disk → right-click `.uproject` → Generate VS project files. Never hand-edit `.sln`. VS Code shows red squiggles on engine includes — **ignore them; the build is the source of truth.**
5. **`.clang-format` at each project repo root** (from templates/) — Epic style; `SortIncludes: false` is load-bearing (include order is semantic in UE).
6. **Verify against UE 5.8.** Any engine API/limit a plan relies on is checked against the installed engine or official 5.8 docs; the unverifiable goes to the plan's ⚠️ Verify list. Never silently trust training data.
7. **Evidence before hypothesis** when debugging tooling/build/editor problems: read the actual error text and on-disk state before proposing fixes. One diagnostic question beats three plausible fixes.
8. **Relevance gate on detours.** Before fixing anything environmental: does it block the current `Done when:`? What's the recurring cost? Not blocking → ask first. Recurring cost for a nicety → don't build it.
9. **Free assets first.** Characters, animations, sounds, and anything outside the Blender ceiling come from free sources (Fab, Epic samples, Mixamo, Kenney, freesound). Blender features exist to learn the pipeline, not to author everything.
10. **Claude owns all bookkeeping** (files, never git). Trigger table — Claude writes these **without being asked**:

| When this happens | Claude writes |
|---|---|
| A step/criterion passes | ✅ it; move `Next action:` |
| A design decision is made | Session log → decision + why |
| Reality contradicts the plan | Fix the plan in place + log the deviation |
| A trap costs more than one round-trip | Session log → trap + fix (KN raw material) |
| You ask a concept question | The answer lands in that feature's Teach/notes — the plan self-heals |
| A ⚠️ Verify item resolves | Strike it, record the outcome |
| Scope changes | Brief's In/Out/Cut lines |
| DoD passes | KN conversation → note → ROADMAP bump |
| A project closes | Re-estimate remaining ROADMAP sessions from actual pace |
| You state a preference about how we work | Claude memory + here if it's a rule |

## Blender pipeline (the ceiling and the contract)

**In scope:** hard-surface props · modular kits on a power-of-two grid · UV unwrap + simple texturing (flat/trim/atlas) · custom collision (`UCX_` naming) · sockets · simple rig + skin for props/accessories · short anim loops · retargeting free character anims inside UE. **Out of scope:** character modeling/sculpting, hair/cloth, photorealism, rendering.

- Source `.blend` files live in the project repo under `<Project>/SourceArt/` and are committed (LFS) — clone = resume includes art sources.
- Export contract (pin exact presets at B1.4, the first Blender feature, and record them in `KN-blender-export.md`): metric units at the UE scale, apply transforms, FBX with smoothing data, axis convention verified against a UE round-trip cube before anything real is exported.
- Naming into UE: `SM_` static mesh, `SK_` skeletal, `T_` texture, `M_`/`MI_` material/instance, `UCX_<mesh>` collision.

## Mobile budgets (📱 projects only — PROVISIONAL until A2.4's device capture)

Targets: 30 fps floor on the mid-range Android test device; 60 fps desktop.

| Item | Budget |
|---|---|
| Character / enemy | 8–20k tris, ≤ 2k atlas, lean skeleton, ≤ 4 skin influences/vertex |
| Hero prop 2–8k · standard prop 0.5–3k · modular piece ≤ 2k tris | |
| Textures | props ≤ 1k, hero ≤ 2k, channel-packed, no 4k on the mobile path |
| Materials | mobile base-pass instructions in the low hundreds; ≤ 2 slots/prop; atlas the kits |
| Scene | ≤ ~500 draw calls, ≤ ~750k on-screen tris (provisional) |
| Lighting | ≤ 1 dynamic shadow-casting light; static/baked wherever possible |

Deviations allowed, stated and justified in the plan's Mobile section. A2.4 validates this table against the real device and updates it.

## Definition of Done — base checklist (every feature)

- [ ] Runs clean in PIE; feature's acceptance criteria / `Done when:`s all pass
- [ ] Story features: Claude close-out review done, findings addressed or logged
- [ ] Packaged build verified when the feature says so (every project's final feature packages; 📱 features on-device)
- [ ] 📱 projects: budgets respected or deviation documented
- [ ] Compiles clean; no new warning/error spam in logs
- [ ] Knowledge note closed via the from-memory ritual (below)
- [ ] ROADMAP status bumped; session log final entry written
- [ ] Committed; both repos pushed at feature close ([You])

## Knowledge notes (retention ritual — kept from GameDevPractice, it worked)

At feature close, **as a conversation, not homework**: Claude asks the plan's KN prompts one at a time; **you answer aloud from memory** — no docs, no code, no session log open; Claude must not read answers back from the log first. Claude transcribes into *Decisions & why / Gotchas & fixes / Would do differently*, drafts *What was built / How it works* from the code, both verify against the code, and the note ends with **`Had to look up:`** — what memory didn't hold. That line is signal, not failure: it drives the demotion rule and steers future Teach blocks. You never type the note.

```markdown
---
id: KN-<slug>
feature: <A1.2>
date: <YYYY-MM-DD>
---
# <Topic>
## What was built                           <!-- [Claude] drafts from the code -->
## How it works (key classes & flow)        <!-- [Claude] drafts from the code -->
## Decisions & why                          <!-- [You] aloud; [Claude] transcribes -->
## Gotchas & fixes                          <!-- [You] aloud; [Claude] transcribes -->
## Would do differently                     <!-- [You] aloud; [Claude] transcribes -->
## Links (code paths, docs, related notes)  <!-- [Claude] drafts, you prune -->
## Had to look up                           <!-- drives the demotion rule -->
```
