# A3 — Chess

**Folder/repo:** `A3_Chess` · **Clone of:** Chess · **Platform:** Windows · **Est:** 14 sessions · **Blender:** none (free piece meshes or primitives) · **UE template:** Blank (Blueprint), converted to C++ at A3.3

**Why this project:** game logic that owes nothing to engine features — a rules engine is pure thinking in data structures. It is also the planned **C++ entry point**: the rules engine is written in Blueprint first (A3.2), then ported to C++ (A3.3) — the port is a deliberate re-implementation rep, and hitting BP's ergonomic limits on algorithmic code first is what makes C++ feel like relief instead of ceremony.

**Scope — In:** full chess rules (castling, en passant, promotion, check/checkmate/stalemate), hotseat play, C++ rules engine + minimax AI, move animation, packaged build.
**Out:** online play, clocks, PGN import/export, opening books.
**Cut line:** AI strength — depth-limited minimax with material evaluation is the bar; alpha-beta pruning only if the sessions allow.

## Features

### A3.1 — Board & pieces (3)
The board as **data** (8×8 state structure) with actors as its *view* — the model/view separation is the feature's real lesson. Piece definitions from a DataTable (data thread rep 2 → how-to): mesh, movement pattern tag. Click to select, legal-shape highlighting (movement geometry only — real legality comes next), top-down/orbit camera. Enhanced Input rep 2 (→ how-to).

### A3.2 — Rules engine in Blueprint (4)
Legal move generation with blocking/capture, turn flow, check detection (does any enemy move hit the king?), checkmate/stalemate, and the three awkward rules: castling, en passant, promotion. Hotseat play at the end. Expect BP to feel increasingly wrong for this — nested loops over board state in graphs. That pain is scheduled, not accidental.

### A3.3 — C++ entry: port the rules engine (4)
**First C++ feature (→ guided):** convert the project to C++, then port A3.2's engine — board state, move generation, rule checks — into C++ classes with a clean BP-facing surface (the board view and input stay in Blueprint). Teach covers: class anatomy, UCLASS/UFUNCTION/USTRUCT, the build/Live-Coding loop, debugging with breakpoints. The port doubles as the retention rep of the rules themselves. Done means: BP calls the C++ engine and every A3.2 behavior still passes.

### A3.4 — Chess AI & polish (3)
Minimax with material evaluation in C++ (rep 2 → how-to), searching 2–3 plies; the AI plays legally and punishes blunders. Move animation (lerp + capture removal), move/capture/check sfx, packaged Windows build (packaging rep → story: no steps, just the criterion).

## Project DoD additions
- Perft-style sanity check: move-generation counts verified for 2–3 known positions (this is how chess engines are actually validated).
- The BP board view contains zero rules logic after A3.3 — grep-level check.
