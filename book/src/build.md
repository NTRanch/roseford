# Build & Delivery — Roseford

**Language:** Rust (tiger-style-rust)

**Delivery shape:** Compile to wasm32, inline the module (base64) in the single index.html; JS is loader and DOM bridge only. Toolchain home: sandbox.

**Jam rule:** one self-contained `index.html`, ≥6 screens (18+ gate / Title / How to Play / Chapel / Descent-and-battle / Pause-Settings / Ending — this entry's set, DESIGN.md §8), documented process (GAMEOTRON orchestrates; the language build chain is part of the documentation).

**Book:** `mdbook build book` renders this planning book to `book/html/`
with the NTRanch theme (dark background, hot pink).
