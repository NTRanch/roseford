---
name: roseford
description: Build and validate Roseford (Torogao Jam Program entry 15, Rust). Use when working on the Roseford jam entry — its corruption state model, Rust build chain, single-file delivery, and port-back.
---

# Roseford — entry 15 jam entry

**Canon core:** A resurrected shrine maiden descends a sealed dungeon whose wards tune her — corruption is her power curve, her memory, and her price.
**Cast:** Isolde (original heroine) · **Language:** Rust (tiger-style-rust)
**Design of record:** `DESIGN.md` in the repo root — the state model's numbers are contracts.

## Mechanism group

- The Tuning core (ward-bosses fight on HP + Tuning Exposure; defeat and victory both raise Corruption, at different prices)
- Corruption as the power curve (Invokes unlock and scale with Corruption; the pure kit decays floor by floor)
- The memory ladder (12 fragments; Hinted → Glimpsed → Known; F11 at C ≥ 550, F12 at C ≥ 750)
- The Chapel Record (cross-run bookkeeping: fragments, tunings, endings)
- Face-state and weather coupling (face band and dungeon weather derive from the same Corruption bands)

## Build

- Delivery: Compile to wasm32, inline the module (base64) in the single index.html; JS is loader and DOM bridge only. Toolchain home: sandbox.
- Planning book: `book/` (mdBook; `mdbook build book`).
- Engine/library pins: book chapter "Engine Research" — read before adding
  any dependency; the from-scratch register (book chapter "Write From
  Scratch") names what must NOT be replaced by a library. The state model
  is zero-dependency by design.

## Gates

1. bloch: start the roadmap item before work; `bloch task done` earns green.
2. Single-file assembly runs offline with all ≥6 screens.
3. State-model gate: half-validation / half-adversarial tests on DESIGN.md §4 (monotonicity, clamping, fragment gates, ending exclusivity).
4. Seahawk playtest pass; breakage filed to bloch.
5. Visual gate (D-221) against the Laplace3D quality bar (book chapter).
6. Port-back note + language verdict + §9 filing (book chapter "Port-Back").

## Standing law

D-292 keeper art only (brand art excepted, D-1123) · audio silence (metrics only, Owner presses play) ·
18+ surfaces flagged (GJ-07) · clean-room fence (D-1123: premise skeleton only) · restricted lane.
