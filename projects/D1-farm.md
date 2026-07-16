# D1 — Farm 📱

**Folder/repo:** `D1_Farm` · **Clone of:** HayDay · **Platforms:** Android-first (+ Windows) · **Est:** 12 sessions · **Blender:** props as needed (→ story) · **UE template:** Blank (C++ where systems warrant)

**Why this project:** the economy-simulation threads (timers, production chains, soft currency) at mobile scale — and the first Stage D project on purpose: after C-stage intensity, most of D1 arrives as how-to/story, proving the fade works. HayDay's craft is *pacing* — everything is a timer whose length is a design decision.

**Scope — In:** grid field placement, crop grow/harvest cycles, processing buildings with queues, storage limits, coins + order board, offline progress, drag-drop touch UX, Android package.
**Out:** social/co-op anything, premium currency, animals beyond one (scope, not sentiment), town/expansion metas.
**Cut line:** order-board variety, then building count (2 processors floor) — the chain fields→goods→orders→coins must close.

## Features

### D1.1 — Grid placement & crops (4)
Tap-to-place on a field grid (touch → story; grid placement is a **guided island** — it returns in D2.3 and E4.3), crop plots with growth timers, ripe → harvest → storage. Drag-to-plant across multiple plots (the HayDay feel). Done means: the plant-wait-harvest loop is pleasant with one crop, before breadth.

### D1.2 — Production chains (3)
Processing buildings consuming inputs → queued outputs over time (wheat → feed → eggs …), queue UI, storage capacity pressure (the actual game design of HayDay). Timer architecture rep (→ story): world timers that survive app death arrive as acceptance criteria, not steps.

### D1.3 — Economy & orders (3)
Coins, an order board requesting good combinations for rewards, order refresh, price/reward balance **fully DataTable-driven** (data thread → story): rebalancing the economy = editing tables, zero code.

### D1.4 — Offline progress & Android (2)
Offline accrual for crops/queues on load (rep 2 of the A2.3 pattern, now multi-system → story), welcome-back summary, autosave; Android package (→ story) with drag-drop verified on-device.

## Project DoD additions
- Economy closes: a new player reaches the second processor unlock in one sitting without dead ends.
- Kill the app mid-queue, reboot the device: every timer resolves correctly.
- All balance values in tables; a designer (you, next month) can retune without opening graphs/code.
