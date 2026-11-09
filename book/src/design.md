# Design — Roseford

**Canon core:** A resurrected shrine maiden descends a sealed dungeon whose wards tune her — corruption is her power curve, her memory, and her price.

The full game design document — state model, floors, battle shape,
endings, scope fence, gates — is **`DESIGN.md` in the repo root** and is
the design of record. This chapter carries the mechanism group and the
validation claim, in the programme's shape.

## Mechanism group

- The Tuning core (every ward-boss fights on two axes: her HP and her Tuning Exposure; bosses win by tuning her, not killing her — defeat and victory both raise Corruption, at different prices)
- Corruption as the power curve (corrupted prayers unlock as Corruption rises and scale with it; the pure kit decays floor by floor, so purity is a real strategy with a real cost curve)
- The memory ladder (12 fragments; revelation runs Hinted → Glimpsed → Known; the deepest fragments are gated behind high Corruption — the full truth is learnable only by letting the tuning in)
- The Chapel Record (cross-run bookkeeping: fragments found, tunings taken, endings reached — carried between runs like Withheld's denial book)
- Face-state and weather coupling (her face state and the dungeon's weather ride the same Corruption bands, so the state is read on her, not on a meter alone)

## What this entry validates

A persistent, monotonic state system as the whole game: whether corruption
as *measured state* — one integer, five bands, priced sources — can carry
power, narrative revelation, and ending structure at once, in Torogao's
native language, so the state model ports back without translation.
