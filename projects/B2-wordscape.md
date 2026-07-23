# B2 — Wordscape 📱

**Folder/repo:** `B2_Wordscape` · **Clone of:** Words of Wonders · **Platforms:** Android-first (+ Linux) · **Est:** 8 sessions · **Blender:** none · **UE template:** Blank (Blueprint)

**Why this project:** a pure mobile-UI game as the consolidation project for the UI/data/touch/save threads before Stage C's big 3D climb — most of it should already arrive in how-to or story mode. Portrait orientation, finger-first design throughout.

**Scope — In:** letter wheel + crossword board from level data, drag-to-select word building, validation + bonus words, level progression with stars, save, Android package.
**Out:** hints/coins economy, daily puzzles, dictionary breadth beyond the shipped word list.
**Cut line:** bonus-words pool, then star thresholds — the drag-select feel and data pipeline are the point.

## Features

### B2.1 — Word data & board generation (3)
Level data as assets/DataTable (data thread rep 3 → how-to→story boundary): target words, grid layout, letter set. The crossword board rendered from data in UMG (grid panel), the letter wheel laid out radially. Done means: any valid level row renders a correct, empty board.

### B2.2 — Drag select & validation (3)
Touch drag across wheel letters (touch rep 3 → story): path line rendering, letter capture order, release-to-submit; validation against level words + a bonus-word list; correct/duplicate/invalid feedback and tile-fill animation. Acceptance criteria carry the feel requirements (no missed letters at speed, no accidental doubles).

### B2.3 — Progression & Android (2)
Level completion → stars → next level unlock; progress save (rep → story); level-select screen; Android package (rep 3 → story) with portrait lock and safe zones. Done means: a phone-holding stranger can play levels 1–10 without instructions.

## Project DoD additions
- Word/level content provably data-driven: a new level row is playable with zero graph/widget edits.
- Drag selection tested on-device at speed — the feel bar is the real Words of Wonders.
