---
id: KN-repo-spinup
feature: S0.1
date: 2026-07-20
---
# Per-project repo spin-up (UE + Git LFS)

**Supersedes** GameDevPractice's `KN-project-source-control` for repo standing-up. That note's Target/Module and LFS-mechanics sections remain valid reference; what changed here is the repo *model*. (Drafted by Claude as approved bookkeeping — S0.1 is a rep-2 how-to close, not a full from-memory ritual; the aloud ritual resumes with A1's feature notes.)

## What was built

- Planning repo `GameDevLearning` live at `github.com/contrazap/GameDevLearning` (text only, no LFS).
- First project repo `A1_Flappy` at `github.com/contrazap/A1_Flappy`: UE 5.8 Blank (Blueprint), Starter Content off, bootstrap commit `3aa665c` = `.uproject` + 4 `Config/*.ini` + the four template files (`.gitignore`, `.gitattributes`, `.clang-format`, `ASSETS.md`). No `Content/` in the commit — it holds only empty dirs at this point; no `Source/` — BP-only.
- Ritual executed end-to-end 2026-07-20; reference checklist is [features/S0-repos-and-spinup.md](../features/S0-repos-and-spinup.md) Part 2.

## How it works (the ritual)

1. UE 5.8 → New Project (template per project brief) → Location = projects parent folder → open once so `Config/` generates, close.
2. `git init -b main`, copy the four templates from `templates/` — **copies, never links** (template improvements propagate to existing projects only as a deliberate act).
3. Verify **before** first add: `git check-ignore -v Intermediate Saved DerivedDataCache` (a rule per existing dir) and `git add -n .` (dry run — expect uproject, Config/, Content/, the four files, nothing ignored).
4. `git add . && git commit` → create empty GitHub repo → `git remote add origin …` → `git push -u origin main`.
5. LFS sanity: `git lfs ls-files` — and if the project has zero assets yet, prove routing with `git check-attr filter diff merge -- Content/X.uasset` (expect `filter: lfs`).

## What changed vs GameDevPractice, and why

- **One repo per UE project** (was: one shared repo, UE rules scoped inside the project subtree). Why: clone = resume per project, bounded repo size, a finished project can be archived/deleted independently. Consequence: ignore/attributes now live at repo **root**, unscoped.
- **Templates instead of hand-drafting** the ignore/attributes/clang-format/ASSETS files — the P0.1 drafting work is banked; spin-up is a 15-minute ritual, not a research task.
- **Commit-all-content policy explicit** (CONVENTIONS rule 4): authored work *and* imported asset copies go in (binaries via LFS); asset sources (Fab, zips) stay outside all repos. Guarded by import-lean (rule 5) + account-level quota watch (rule 6: 10 GB storage / 10 GB/mo bandwidth, 0.3 GB pre-used, revisit at ~7 GB).
- **Planning repo carries no LFS** — all binary weight lives in project repos.

## Gotchas & fixes

- **Empty `git lfs ls-files` after bootstrap — second encounter, recognized this time.** Blank BP + no starter content = zero `.uasset`/`.umap` exist, so there's nothing to list (same lesson as P0.1's empty Content/). Proof without creating an asset: `git check-attr` on a hypothetical path. Real end-to-end proof = first map save in A1.1.
- **Git doesn't track empty dirs** — hence no `Content/` in the bootstrap commit; it appears with the first saved asset. (P0.1 used `.gitkeep`; this ladder just lets `Content/` arrive naturally.)
- **`git remote add` on an existing name errors** (`remote origin already exists`) — fix the URL with `git remote set-url origin <url>` instead. Hit during the repo-rename detour (repo first created as `GDLPractice_A1_Flappy`, recreated as `A1_Flappy` per CONVENTIONS naming).
- **`git add -n` without a pathspec is a no-op** — the dry run is `git add -n .`.
- **CRLF warnings on the copied templates** ("LF will be replaced by CRLF") are harmless Windows line-ending normalization — not a corruption signal.

## Would do differently

- Create the GitHub repo with its final conventions-checked name **before** `git remote add` — skips the rename detour.
- Run the dry-run exactly as written; the commit file list caught it this time, but the whole point of step 3 is catching junk *before* it's staged.

## Links (code paths, docs, related notes)

- Feature plan + session log: [features/S0-repos-and-spinup.md](../features/S0-repos-and-spinup.md)
- Templates: [templates/](../templates/) · Repo rules: [CONVENTIONS.md §Repos & filesystem](../CONVENTIONS.md)
- Predecessor note (Target/Module, LFS verify commands, secrets pattern): `C:\MyFiles\Projects\GameDevPractice\knowledge\KN-project-source-control.md`
- Next encounter: A2's spin-up (rep 3) — should run from memory with the feature file as checklist only.

## Had to look up

- `git remote set-url` (vs `remote add`) when repointing origin — asked mid-session.
- `git add -n` needing the `.` pathspec.
- Everything else ran from the S0.1 checklist as designed for a how-to rep; UE template choice came from the project brief (by design, not a gap).
