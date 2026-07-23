---
id: S0.1
title: Repos & the project spin-up ritual
project: S0
mode: howto
status: done
skills: [project-spinup(rep 2→howto)]
est_sessions: 1-2
mobile: no
---

# S0.1 — Repos & the project spin-up ritual

**Next action:** none — S0.1 closed 2026-07-20 (all DoD ✅). This file is now the Part 2 checklist for future spin-ups; knowledge delta in `knowledge/KN-repo-spinup.md`. Next feature: ~~A1.1~~ **[S0.2 — Arch Linux workstation setup](S0.2-arch-linux-setup.md)** (inserted 2026-07-23 by the Linux migration), then A1.1 in `A1_Flappy`.

**How-to grade** — you built this pattern once in GameDevPractice P0.1 (`knowledge/KN-project-source-control.md` in `github.com/contrazap/GameDevPractice` is the allowed reference — the old local Windows copy did not migrate; clone it if needed). Commands are listed as reference, not as blind steps: know what each does before running it. All git commands are [You] — always (CONVENTIONS repo rule 7).

## Why & what

Two repo kinds (CONVENTIONS §Repos): **this planning repo** (text only, no LFS content) and **one repo per UE project** under `/home/pallav/MyFiles/Projects/GameDevLearningPractice/`. Part 1 stands the planning repo up — done once. Part 2 is the **spin-up ritual** repeated for every project (~16×); by Stage B it should run from memory with this file as a checklist only.

## Part 1 — planning repo (once)

1. **Create the GitHub repo** `GameDevLearning` — empty: no README/gitignore/license (this folder already has files).
2. **Init + first push** (from `/home/pallav/MyFiles/Projects/GameDevLearning`):
   ```bash
   git init -b main
   git lfs install          # machine-wide once: installs the LFS filters; this repo itself tracks nothing via LFS
   git add .
   git commit -m "Roadmap v1 - fundamentals ladder"
   git remote add origin https://github.com/<you>/GameDevLearning.git
   git push -u origin main
   ```
   **Done when:** the repo renders on GitHub with README/ROADMAP visible.
3. ✅ **Check the LFS quota** (GitHub → Settings → Billing → Git LFS). *Resolved 2026-07-17 from the billing page:* free plan includes **10 GB LFS storage + 10 GB/month bandwidth** (metered, included-usage model; monthly reset). **0.3 GB storage already used** by older repos (`CrystalCavern_GameDevTv`, `GameDevPractice`). Quota is **account-level** — all project repos draw from it. Data-pack decision recast: with 10 GB included and import-lean discipline, no purchase expected before late ladder — **trigger: storage crossing ~7 GB** (Claude flags it when heavy imports land).
4. ✅ **Create the projects parent folder** — created 2026-07-17 as `C:\MyFiles\Projects\GameDevLearningPractice\` (user's naming; supersedes the original `GDL` suggestion — CONVENTIONS rule 2 updated, with a path-length watch item below).

## Part 2 — per-project spin-up ritual (repeat for every project)

Shown for `A1_Flappy`; substitute per project brief (folder name, template).

1. **Create the UE project:** UE 5.8 → New Project → template per the project brief → Location `/home/pallav/MyFiles/Projects/GameDevLearningPractice` → Name `A1_Flappy`. Open once (lets UE generate `Config/`), then close.
2. **Init the repo + copy the four template files:**
   ```bash
   cd /home/pallav/MyFiles/Projects/GameDevLearningPractice/A1_Flappy
   git init -b main
   P=/home/pallav/MyFiles/Projects/GameDevLearning/templates
   cp $P/ue-project.gitignore     .gitignore
   cp $P/ue-project.gitattributes .gitattributes
   cp $P/ue-project.clang-format  .clang-format
   cp $P/ASSETS.md                ASSETS.md
   ```
   Copies, never links — if a template improves later, updating existing projects is a deliberate act.
3. **Verify before the first add** — the P0.1 discipline:
   ```bash
   git check-ignore -v Intermediate Saved DerivedDataCache   # a rule prints for each dir that exists
   git add -n .                                              # dry run: expect .uproject, Config/, Content/,
                                                             # the four copied files (+ Source/ on C++ projects)
                                                             # and NOTHING from the ignored dirs
   ```
   **Done when:** both outputs match expectations. Anything unexpected → stop and read, don't add.
4. **First commit, remote, push:**
   ```bash
   git add .
   git commit -m "A1_Flappy bootstrap"
   # create empty GitHub repo A1_Flappy first, then:
   git remote add origin https://github.com/<you>/A1_Flappy.git
   git push -u origin main
   ```
5. **LFS sanity:** `git lfs ls-files` lists the project's `.uasset`/`.umap` files (a Blank-template project may have few — any at all proves routing works).
   **Done when:** pushed; LFS list sane; ritual took under 15 minutes (by B1 it should).

## Definition of Done

- [x] Planning repo live on GitHub, pushed from this folder (verified in sync 2026-07-20)
- [x] LFS quota numbers recorded (10 GB storage / 10 GB/mo bandwidth included; 0.3 GB pre-used); data-pack trigger set at ~7 GB storage
- [x] Projects parent folder exists — `C:\MyFiles\Projects\GameDevLearningPractice\` (2026-07-17, Windows); re-established as `/home/pallav/MyFiles/Projects/GameDevLearningPractice/` on the Linux migration (2026-07-23)
- [x] Ritual executed once end-to-end (A1_Flappy, 2026-07-20 — its project can start A1.1 immediately)
- [x] Knowledge note: **update** GameDevPractice's source-control knowledge into `knowledge/KN-repo-spinup.md` here — what changed (per-project repos, commit-all-content policy) and why (2026-07-20, Claude-drafted delta note, user-approved)
- [x] ROADMAP S0.1 → ✅ (2026-07-20)

## ⚠️ Verify list

- ~~**Current LFS quota/pricing**~~ — resolved 2026-07-17 (step 3): 10 GB storage + 10 GB/mo bandwidth included on the free plan; 0.3 GB pre-used.
- ~~**UE 5.8 new-project dialog**~~ — resolved 2026-07-20: accepted `C:\MyFiles\Projects\GameDevLearningPractice` as Location and created the `A1_Flappy` subfolder as expected.
- ~~**Path length under the longer parent**~~ — retired 2026-07-23 by the Linux migration: ext4 has no `MAX_PATH`, so `Intermediate/` and Android gradle depths are a non-issue. Replaced by a **case-sensitivity** watch (CONVENTIONS rule 2) — wrong-cased asset refs and `#include`s that passed silently on NTFS now fail.
- **Linux toolchain unknowns (new 2026-07-23)** — UE 5.8 Linux editor install route, `git-lfs` presence on a fresh Arch box, and the Blender-flatpak → MCP path are all unverified on this machine; first Android package (A2.4) and first C++ build (A3.3) are the checkpoints that will actually exercise them.
- **`git check-ignore` on dirs that don't exist yet** returns nothing — only check dirs the editor has actually generated.
- **BP-only projects have no `Source/`** — expected; it appears when the project converts to C++ (A3.3).

## Session log

*Append-only; Claude writes per the trigger table.*

**2026-07-17 — pre-session bookkeeping (steps 3–4 ✅).** User provided the GitHub billing screenshot: GitHub Free, Git LFS **10 GB storage + 10 GB/month bandwidth included** (metered model, monthly reset), **0.3 GB storage used** by `CrystalCavern_GameDevTv` + `GameDevPractice`, $0 billable. Data-pack trigger recast from "first heavy import" to **storage ~7 GB** — far looser than planned thanks to the 10 GB allowance.
- *Decision:* projects parent folder created by user as **`C:\MyFiles\Projects\GameDevLearningPractice\`** (supersedes the `GDL` suggestion). All plan files updated (CONVENTIONS rule 2, README, PLAN-GENERATOR, this file). Path-length consequence logged as a Verify item (watch A3.3 / A2.4).
- *Remaining:* Part 1 steps 1–2 (create + push planning repo); Part 2 runs in the first morning session (user will confirm).

**2026-07-20 — Part 2 ritual executed end-to-end for A1_Flappy ✅.** UE 5.8 Blank (Blueprint) project created at the correct location, Starter Content off, no `Source/` (BP-only, as expected). `git check-ignore -v` printed rules for all three generated dirs; bootstrap commit `3aa665c` held exactly 9 files (uproject + 4 Config inis + 4 template files), nothing leaked from ignored dirs; pushed to `github.com/contrazap/A1_Flappy`, `main` tracking `origin/main`.
- *LFS sanity resolved:* `git lfs ls-files` was empty — verified **expected**, not a failure: `Content/` holds zero files (empty dirs only; git doesn't track them, hence no `Content/` in the commit either). Routing proven instead via `git check-attr` — `.uasset`/`.umap` → `filter: lfs`. Real end-to-end proof lands with the first map save in A1.1: glance at `git lfs ls-files` after that commit.
- *Detour:* GitHub repo initially created as `GDLPractice_A1_Flappy`; user deleted and recreated as `A1_Flappy` per CONVENTIONS rule 2, fixed origin with `git remote set-url` (learned: `remote add` fails on an existing name; `set-url` rewrites it).
- *Also:* dry-run step ran as `git add -n` (no pathspec → no-op); commit file list served as the same verification. CRLF warnings on template files are harmless Windows line-ending normalization. Part 1 confirmed pushed and in sync (done earlier, commit "github repo setup done for plan repo").
- *Remaining for S0.1 close:* `knowledge/KN-repo-spinup.md`, then ROADMAP tick.

**2026-07-20 — S0.1 closed ✅.** `knowledge/KN-repo-spinup.md` written (delta note vs GameDevPractice's KN-project-source-control; Claude-drafted as user-approved bookkeeping — the from-memory ritual resumes with A1 feature notes). ROADMAP S0.1 → ✅, frontmatter `status: done`. Real `Had to look up:` items recorded from the session: `git remote set-url`, `git add -n` pathspec. Planning-repo commit + push remain [You] at session close.
