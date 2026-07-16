---
id: S0.1
title: Repos & the project spin-up ritual
project: S0
mode: howto
status: ready
skills: [project-spinup(rep 2→howto)]
est_sessions: 1-2
mobile: no
---

# S0.1 — Repos & the project spin-up ritual

**Next action:** Part 1, steps 1–2 — create the `GameDevLearning` repo on GitHub and push this folder. (Steps 3–4 ✅ 2026-07-17: quota recorded, parent folder created.) Then Part 2 for `A1_Flappy` opens the first morning session.

**How-to grade** — you built this pattern once in GameDevPractice P0.1 (`C:\MyFiles\Projects\GameDevPractice\knowledge\KN-project-source-control.md` is the allowed reference). Commands are listed as reference, not as blind steps: know what each does before running it. All git commands are [You] — always (CONVENTIONS repo rule 7).

## Why & what

Two repo kinds (CONVENTIONS §Repos): **this planning repo** (text only, no LFS content) and **one repo per UE project** under `C:\MyFiles\Projects\GameDevLearningPractice\`. Part 1 stands the planning repo up — done once. Part 2 is the **spin-up ritual** repeated for every project (~16×); by Stage B it should run from memory with this file as a checklist only.

## Part 1 — planning repo (once)

1. **Create the GitHub repo** `GameDevLearning` — empty: no README/gitignore/license (this folder already has files).
2. **Init + first push** (from `c:\MyFiles\Projects\GameDevLearning`):
   ```powershell
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

1. **Create the UE project:** UE 5.8 → New Project → template per the project brief → Location `C:\MyFiles\Projects\GameDevLearningPractice` → Name `A1_Flappy`. Open once (lets UE generate `Config/`), then close.
2. **Init the repo + copy the four template files:**
   ```powershell
   cd C:\MyFiles\Projects\GameDevLearningPractice\A1_Flappy
   git init -b main
   Copy-Item c:\MyFiles\Projects\GameDevLearning\templates\ue-project.gitignore    .gitignore
   Copy-Item c:\MyFiles\Projects\GameDevLearning\templates\ue-project.gitattributes .gitattributes
   Copy-Item c:\MyFiles\Projects\GameDevLearning\templates\ue-project.clang-format  .clang-format
   Copy-Item c:\MyFiles\Projects\GameDevLearning\templates\ASSETS.md               ASSETS.md
   ```
   Copies, never links — if a template improves later, updating existing projects is a deliberate act.
3. **Verify before the first add** — the P0.1 discipline:
   ```powershell
   git check-ignore -v Intermediate Saved DerivedDataCache   # a rule prints for each dir that exists
   git add -n .                                              # dry run: expect .uproject, Config/, Content/,
                                                             # the four copied files (+ Source/ on C++ projects)
                                                             # and NOTHING from the ignored dirs
   ```
   **Done when:** both outputs match expectations. Anything unexpected → stop and read, don't add.
4. **First commit, remote, push:**
   ```powershell
   git add .
   git commit -m "A1_Flappy bootstrap"
   # create empty GitHub repo A1_Flappy first, then:
   git remote add origin https://github.com/<you>/A1_Flappy.git
   git push -u origin main
   ```
5. **LFS sanity:** `git lfs ls-files` lists the project's `.uasset`/`.umap` files (a Blank-template project may have few — any at all proves routing works).
   **Done when:** pushed; LFS list sane; ritual took under 15 minutes (by B1 it should).

## Definition of Done

- [ ] Planning repo live on GitHub, pushed from this folder
- [x] LFS quota numbers recorded (10 GB storage / 10 GB/mo bandwidth included; 0.3 GB pre-used); data-pack trigger set at ~7 GB storage
- [x] `C:\MyFiles\Projects\GameDevLearningPractice\` exists (2026-07-17)
- [ ] Ritual executed once end-to-end (A1_Flappy — its project can then start A1.1 immediately)
- [ ] Knowledge note: **update** GameDevPractice's source-control knowledge into `knowledge/KN-repo-spinup.md` here — what changed (per-project repos, commit-all-content policy) and why
- [ ] ROADMAP S0.1 → ✅

## ⚠️ Verify list

- ~~**Current LFS quota/pricing**~~ — resolved 2026-07-17 (step 3): 10 GB storage + 10 GB/mo bandwidth included on the free plan; 0.3 GB pre-used.
- **UE 5.8 new-project dialog** — confirm it accepts `C:\MyFiles\Projects\GameDevLearningPractice` as Location and creates the named subfolder (expected; verify on first use).
- **Path length under the longer parent** — the folder name adds ~17 chars over the original suggestion; deep paths (`Intermediate/`, Android gradle) may near Windows limits. Watch at first C++ build (A3.3) and first Android package (A2.4); fixes if hit: enable Windows long paths or shorten the parent (logged decision).
- **`git check-ignore` on dirs that don't exist yet** returns nothing — only check dirs the editor has actually generated.
- **BP-only projects have no `Source/`** — expected; it appears when the project converts to C++ (A3.3).

## Session log

*Append-only; Claude writes per the trigger table.*

**2026-07-17 — pre-session bookkeeping (steps 3–4 ✅).** User provided the GitHub billing screenshot: GitHub Free, Git LFS **10 GB storage + 10 GB/month bandwidth included** (metered model, monthly reset), **0.3 GB storage used** by `CrystalCavern_GameDevTv` + `GameDevPractice`, $0 billable. Data-pack trigger recast from "first heavy import" to **storage ~7 GB** — far looser than planned thanks to the 10 GB allowance.
- *Decision:* projects parent folder created by user as **`C:\MyFiles\Projects\GameDevLearningPractice\`** (supersedes the `GDL` suggestion). All plan files updated (CONVENTIONS rule 2, README, PLAN-GENERATOR, this file). Path-length consequence logged as a Verify item (watch A3.3 / A2.4).
- *Remaining:* Part 1 steps 1–2 (create + push planning repo); Part 2 runs in the first morning session (user will confirm).
