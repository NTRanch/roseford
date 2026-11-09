# Write From Scratch — Roseford

No library sells these. Each item below is designated **FROM SCRATCH**:
authored in this repo, in Rust, on top of the pinned libraries in the
Engine Research chapter. (Estate-shared systems — the arousal engine, the
F-code face states, the culmination package — are re-implemented or ported
per this week's language rule, and divergences are filed as findings.)

- The corruption state model (one integer, five bands, priced sources,
  monotonic within a run — DESIGN.md §4; zero dependencies, fixed-step,
  deterministic, and the entry's whole port-back claim)
- The two-axis boss fight (HP and Tuning Exposure, with the Tuning event
  as a first-class outcome rather than a damage variant)
- The memory ladder (fragment gating, the Hinted → Glimpsed → Known
  reveal stages, the Chapel Reading assembly)
- The Chapel Record (cross-run bookkeeping and its persistence format)

## Estate systems this entry also carries

- **Face-state system (F-codes):** F-00 composed, F-03 edge, F-05 peak,
  F-10 daze — data-driven expressions, gaze and blush channels; here the
  face band is *derived from the corruption state* (DESIGN.md §4.2), which
  is this entry's variation on the system and a filed finding either way.
- **State weather:** the dungeon's weather is the same band read on the
  room (Clear / Humming / Resonant / Drowned / Rosedeep) — the estate's
  slow-state vocabulary applied to a place instead of a person.
- **Arousal engine (arousal-engine/1):** tiered build with canon durations
  (T1 4+4 / T2 7+6 / T3 11+9 / T4 16+12 s), exactly-once culmination —
  carried where the tuning scenes call for it, at scene scale.
