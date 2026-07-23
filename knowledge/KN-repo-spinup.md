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
5. LFS sanity: `git lfs ls-files` — and if the project has zero assets yet, prove routing with `git check-attr filter diff merge -- Content/X.uasset` (expect `filter: lfs`). Also confirm `.git/hooks/pre-push` exists — see the no-hooks gotcha below.

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
- **A repo cloned before the machine's `git lfs install` has no LFS hooks — and the failure is silent.** *(S0.2 delta, 2026-07-24, first Arch-box encounter.)* Machine-wide `git lfs install` sets global *filters* but does not retrofit hooks into repos that already exist: commits still become pointers, `git lfs env` looks clean — but without `.git/hooks/pre-push` a push uploads pointers and never the binary objects. GitHub ends up holding pointers-to-nothing, and the break surfaces at the *next clone*, not at push time — exactly the clone-=-resume property this ritual exists to protect. Fix: run `git lfs install` *inside* each repo cloned before git-lfs landed on the machine; proof is `.git/hooks/pre-push` existing (step 5 amended). Applies to every machine migration. ("LF will be replaced by CRLF") are harmless Windows line-ending normalization — not a corruption signal. *(Obsolete from 2026-07-23: the ladder moved to Linux, where the copies stay LF and this warning never appears. Kept because the reasoning — a filter warning is not corruption — is the transferable part.)*

## Would do differently

- Create the GitHub repo with its final conventions-checked name **before** `git remote add` — skips the rename detour.
- Run the dry-run exactly as written; the commit file list caught it this time, but the whole point of step 3 is catching junk *before* it's staged.

## Links (code paths, docs, related notes)

- Feature plan + session log: [features/S0-repos-and-spinup.md](../features/S0-repos-and-spinup.md)
- Templates: [templates/](../templates/) · Repo rules: [CONVENTIONS.md §Repos & filesystem](../CONVENTIONS.md)
- Predecessor note (Target/Module, LFS verify commands, secrets pattern): `knowledge/KN-project-source-control.md` in `github.com/contrazap/GameDevPractice` (local Windows copy did not migrate — clone to read)
- Next encounter: A2's spin-up (rep 3) — should run from memory with the feature file as checklist only.

## Had to look up

- `git remote set-url` (vs `remote add`) when repointing origin — asked mid-session.
- `git add -n` needing the `.` pathspec.
- Everything else ran from the S0.1 checklist as designed for a how-to rep; UE template choice came from the project brief (by design, not a gap).
