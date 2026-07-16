# C2 — Souls arena

**Folder/repo:** `C2_SoulsArena` · **Clone of:** Dark Souls 2 (combat loop) · **Platform:** Windows · **Est:** 20 sessions · **Blender:** yes (C2.5) · **UE template:** Third Person (C++)

**Why this project:** the melee-combat and enemy-AI first encounters, on top of C1's movement/animation base (character setup and AnimBP arrive as how-to/story — the rep design in action). The souls loop is chosen because it demands *systemic honesty*: stamina, i-frames, and AI turn-taking can't be faked with animation flash.

**Scope — In:** stamina-gated melee (light/heavy), weapon traces with proper damage windows, hit reactions, dodge with i-frames, lock-on with camera + movement mode change, Behavior-Tree enemies with perception, one boss with phases, death/respawn at a rest point, 2–3 own Blender weapons, first Niagara effects, packaged arena build.
**Out:** equipment/inventory systems (D2 owns that thread), poise/status effects, multiple weapon move-sets, NG+.
**Cut line:** boss phase count, then enemy variety (2 regular types is the floor) — melee core and lock-on are not cuttable.

## Features

### C2.1 — Melee core (5)
Attack montages with **damage windows driven by anim notifies**, weapon traces during windows only, damage/knockback application, directional hit reactions, stamina costs/regen gating actions, dodge roll with i-frames (→ guided; animation thread rep 2 → how-to). Done means: hitting and getting hit both read clearly and cost the right resources.

### C2.2 — Lock-on & camera (3)
Target acquisition (range/angle/visibility), target switching on input flick, lock-on camera framing both fighters, strafe movement mode while locked (character/camera rep 3 → how-to). The subtle part is the camera — it does the fight's storytelling.

### C2.3 — Enemy AI (5)
**Behavior Trees + AIPerception (first encounter → guided):** patrol/idle → aggro on sight/sound → approach with spacing → attack selection with cooldowns → recover/reposition → leash-reset with heal. Blackboard discipline, BT decorators/services, the perception config traps. Done means: two enemy types that fight differently and can be read and baited by a player.

### C2.4 — Boss, death loop & bonfire (4)
Boss with 2 phases (health-gated), telegraphed attacks with punish windows, arena gating; player death → respawn at rest point, world/boss state reset (save thread → story). Melee rep 2 (→ how-to) via the boss's expanded move handling. Done means: the fight is learnable — deaths feel like the player's fault.

### C2.5 — Blender weapons, VFX & package (3)
2–3 weapons in Blender (rep 3 → how-to: sockets, grip alignment, trace-socket placement), **first Niagara feature (→ guided):** hit sparks/blood puff, swing trails; impact/whoosh sfx from free packs; package (→ story).

## Project DoD additions
- Damage windows verifiably match visuals (debug-draw the traces; no hits outside windows).
- I-frames measurable and honest (log invulnerability spans against the roll montage).
- AI is legible: a first-time player can articulate each enemy's tell after 3 encounters.
