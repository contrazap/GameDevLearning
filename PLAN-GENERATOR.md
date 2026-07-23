# Plan Generator

Reusable instruction set. One invocation generates **one** feature document into `features/` — a guided plan, a how-to plan, or a user story, **decided by rep counts**, not by request. Run it in a Claude Code session that can see this repo and the projects parent folder (`/home/pallav/MyFiles/Projects/GameDevLearningPractice/`) — real code beats assumptions.

**Format principles (inherited from GameDevPractice 2026-07-12, extended 2026-07-17):**
1. **Teaching lives at the point of use.** One document per feature. No separate primers — separated teaching decays before use. In story mode the "primer" shrinks to named concepts + references inside the story.
2. **Two-stage generation (guided/how-to only).** The container is generated up front; full session detail (Teach + Steps) is generated **just-in-time at the start of the session that runs it**, against the repo as it actually exists. Steps written against an imagined repo state ship fabricated paths. Stories have no steps, so no second stage — only the JIT reality check (procedure 14).
3. **The plan is also the progress record.** `**Next action:**` at the top, append-only `## Session log` at the bottom, Claude owns both (CONVENTIONS rule 10). Any fresh session is resumable with one read.
4. **The fade is the retention mechanism.** With no variation challenges and no drill days, rep-3+ skills *must* arrive as stories — softening a story back into steps quietly deletes the retrieval practice this system depends on.

## Invocation (copy, fill, paste)

```
Read PLAN-GENERATOR.md in the GameDevLearning repo and follow it exactly.
Feature: <ID, e.g. B1.2>
Notes: <optional — scope tweaks, what's already done, device on hand>
```

Mode is **not** an input — it is derived (procedure 2). To override (rare, say why): `Mode override: guided|howto|story`.
Mid-feature, no invocation needed: "read `features/<ID>-*.md` and continue" triggers session-detail generation or story session pickup.

## Procedure — every invocation

1. **Read first:** `CONVENTIONS.md` → the feature's paragraph in `projects/<ID>-*.md` → its ROADMAP row and neighbors → `SKILL-MATRIX.md` skill threads it touches → related `knowledge/` notes (especially `Had to look up:` lines) → prior `features/` plans that share threads → the live project repo if it exists.
2. **Derive the mode per skill thread:**
   - Count the thread's **completed** reps (SKILL-MATRIX rep path ∩ ✅ features). 0 prior → **guided**. 1 prior → **how-to**. 2+ prior → **story**.
   - **Demotion:** if the thread's latest KN note has a substantive `Had to look up:` entry for it, demote one mode.
   - **Feature shape = the mode of its dominant/new threads.** Repeated threads inside a guided feature appear as how-to/story steps; a new sub-skill inside a story becomes a **guided island** (one Teach block, nothing more).
   - Record the derivation in the doc header: `skills: [pooling(rep 2→howto), instancing(rep 0→guided)]`. If the derived shape contradicts the project brief's expectation, say so and reconcile before generating.
3. **Clarify or proceed:** at most 3 questions, only if the answer changes the document's shape.
4. **Size it:** features are 2–6 sessions (1-hour sessions). Bigger → propose a split (`B1.2a/b`), update brief + ROADMAP, generate the first part only. No line cap — the session budget is the budget.
5. **Verify UE 5.8:** engine APIs/limits the document relies on get checked against the installed engine or official 5.8 docs. Unverifiable → ⚠️ Verify list. Every literal is a claim.
6. **Prerequisites declared:** "Assumes you can: X, Y, Z" — each linked to a KN note or taught in a named Teach block. No silent competence assumptions.
7. **Budgets from CONVENTIONS** (📱 features only) — reference, don't invent.
8. **Design rationale is part of learning:** the document explains *why the reference game does it this way*, not just what to build.
9. **Write the file** `features/<ID>-<slug>.md` with `**Next action:**` top and empty `## Session log` bottom; bump ROADMAP ⬜ → 📋. Touch nothing else.

## Procedure — guided / how-to specifics

10. **Sessions are outlined, not detailed** in the container: per session a short paragraph — goal, end state, rough scope, first-encounter skills. Verified engine-stable facts may sit beneath as a **Teach seed** (`re-verify at session start`); never as numbered steps.
11. **Session detail JIT (at that session's start):** read container + log, then generate `### Teach` + `### Steps` in place of the outline. Resolve every path, class name, signature, and asset reference against the live repo/engine — inspection, not execution; the genuinely unknowable goes to ⚠️ Verify.
12. **Step grain by mode:** guided = atomic (one edit site or artifact per step, exact values, `**Done when:**` each; >2 edits or >1 file → split `Na/Nb`). How-to = goal + constraints + where it was learned; you find the path; still ends with `**Done when:**`.
13. **Steps carry no explanation and no choices.** Concepts live in Teach — if a step needs explaining, Teach is missing something. Exception: a genuine **design decision** is its own [You] step, options + trade-offs laid out, decision logged.

## Procedure — story specifics

14. **A story has no steps and no Teach.** It has: the story sentence ("As the player, …"), **acceptance criteria** (testable, 5–10, they *are* the DoD additions), **constraints** (what must be data-driven, budget rows, architecture seams to respect), **named concepts** (2–3, named not explained), and **references** (docs/samples per CONVENTIONS reference policy — where to look, never what to type). At the story's first session, Claude does a **reality check** (paths/API names the criteria mention still exist) — not a solution design.
15. **During story sessions Claude is a consultant** bound by the escalation ladder (CONVENTIONS): hint → concept → approach → pair, ~15–20 min stuck per level, never volunteering ahead. Concept answers may become an appended `## Consulted` section (they're KN raw material), never steps.
16. **Close-out review is part of the story:** against acceptance criteria + quality pass. Findings discussed; fixes are [You]. Review summary goes in the session log.

## Output templates

**Guided / how-to container** (story marks N/A sections as absent):

```markdown
---
id: B1.2
title: <name>
project: B1
mode: guided | howto | story
status: draft
skills: [<thread(rep n→mode)>, ...]
maps_to: [<reference games>]
est_sessions: <n>
mobile: yes|no
---

# <ID> — <Title>

**Next action:** <exactly where work resumes>

## Why & what
Goal, design rationale (why the reference game does it this way), scope In/Out/Cut lines, assets needed (free sources or Blender feature ref).
**Assumes you can:** <each linked to KN note or Teach>

## Mental model
3–5 organizing concepts + sketch. Ends with readiness self-check questions. (guided/how-to only)

## Session 1..n — <name>
Outline paragraph → JIT-expanded to ### Teach / ### Steps (procedures 10–13).

## Mobile & performance   (📱 features only)
Budget rows, expected costs, risks, fallbacks.

## Definition of Done
CONVENTIONS base checklist + feature-specific checks.

## Knowledge note prompts
3–6 questions for the close ritual.

## ⚠️ Verify list
Only what can't be checked before execution.

## Session log
Append-only; Claude writes per the trigger table.
```

**Story** (same frontmatter, `mode: story`):

```markdown
# <ID> — <Title>

**Next action:** ...

## Story
As the player, ... — and why the reference game shapes it this way.

## Acceptance criteria
- [ ] <testable> ...

## Constraints
Data-driven requirements, budgets, seams to respect. **Assumes you can:** <KN links>.

## Concepts you'll need (named, not explained)
- <concept> — see References

## References
<official docs / engine samples; videos flagged with watch time>

## Guided island: <topic>   (only if a genuinely new sub-skill exists)
### Teach — one block, scoped to the island.

## Definition of Done
Base checklist + "Close-out review passed".

## Knowledge note prompts
## ⚠️ Verify list
## Consulted   (appended during sessions — escalation answers land here)
## Session log
```

## Rationale trail (don't relitigate without new evidence)

- **2026-07-12 (a, GameDevPractice):** separate primers/variations/quizzes retired — separated teaching decayed before use; separately-invoked practice never ran → single teach-then-do doc.
- **2026-07-12 (b, GameDevPractice):** P0.2 execution audit → atomic steps for first encounters (mega-steps stall a beginner), methods-in-Teach not answers-in-steps (pre-cooked answers hid two generation errors), two-stage generation (steps can't be verified against a repo state that doesn't exist), `Next action:` + session log with Claude as bookkeeper.
- **2026-07-17:** teaching fades **per skill by rep count** (guided → how-to → story), grounded in worked-example fading / expertise-reversal / retrieval practice. Variation challenges and drill days retired *because* rep-3+ ladder features run as stories — the retrieval practice moved inside real progress. Consequences: softening stories back to steps is a system failure, and the escalation ladder (not helpfulness) governs story-mode assistance. Multiplayer sections dropped entirely (excluded from this roadmap); story acceptance criteria replace step-level Done-whens at the fade's end.
