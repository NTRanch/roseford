# Planning — Roseford

- **Program:** Torogao Jam Program (D-333), entry 15 (week 15), Wave E — Systems (proposed at stand-up under D-1123, adopted D-1130; Waves A–D closed at week 14 — this entry validates a whole state system rather than a sense or a feature)
- **Cast:** Isolde (original heroine, new to the programme — see DESIGN.md §2)
- **Language:** Rust (tiger-style-rust)
- **Canon core:** A resurrected shrine maiden descends a sealed dungeon whose wards tune her — corruption is her power curve, her memory, and her price.

## Mechanism group (D-334: primary + coupled + persistence/revelation + feel)

- The Tuning core (every ward-boss fights on two axes: her HP and her Tuning Exposure; bosses win by tuning her, not killing her — defeat and victory both raise Corruption, at different prices)
- Corruption as the power curve (corrupted prayers unlock as Corruption rises and scale with it; the pure kit decays floor by floor, so purity is a real strategy with a real cost curve)
- The memory ladder (12 fragments; revelation runs Hinted → Glimpsed → Known; the deepest fragments are gated behind high Corruption — the full truth is learnable only by letting the tuning in)
- The Chapel Record (cross-run bookkeeping: fragments found, tunings taken, endings reached — carried between runs like Withheld's denial book)
- Face-state and weather coupling (her face state and the dungeon's weather ride the same Corruption bands, so the state is read on her, not on a meter alone)

## Validates

A persistent, monotonic state system as the whole game: whether corruption
as *measured state* — one integer, five bands, priced sources — can carry
power, narrative revelation, and ending structure at once, in Torogao's
native language, so the state model ports back without translation.

## Port-back

The corruption state model (bands, priced sources, exposure axis) as a
Torogao state-layer candidate; the reveal-ladder table; Rust verdict,
third pass.

## Delivery

Compile to wasm32, inline the module (base64) in the single index.html; JS is loader and DOM bridge only. Toolchain home: sandbox.

## Open preflight items

- Wave E assignment ADOPTED (D-1130, 2026-11-09): week 15, Wave E —
  Systems. The Owner may still re-wave or re-week this entry at the
  week-15 word.
- GJ-06-class start gate for this week's toolchain (later weeks gate their
  own preflight; only W1's gate covers the program start).
- GJ-07: 18+ flag, content warnings listed, itch ToS screen — verified live
  at entry (the NSFW allowance clause is Owner-reported; re-verify on page).
- Engine-research chapter in the book: confirm the pinned library versions
  before the first build commit.
- Repo publication (GitHub under NTRanch) is a separate Owner call; this
  stand-up is local-only.
