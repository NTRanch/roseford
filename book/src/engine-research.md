# Rust — engine research for Roseford (entry 15)

| | |
|---|---|
| **Language** | Rust (pinned toolchain; estate pin `nightly-2026-09-25` for the main-game line — jam weeks use the same pin unless a week's preflight records otherwise) |
| **Role in the program** | Third Rust entry, after **W4 *Handfast*** (the two-body stress test) and **W11 *Withheld*** (the Governor control-law game). Rust is the **home language of the main game**: Torogao's native build is Rust, so every Rust jam entry is simultaneously a game build and a **port-back target** — findings land in Torogao with no translation layer. Roseford's port-back claim is its **state model**, which is plain Rust by design (see below). |
| **Delivery shape (jam)** | Compile to `wasm32-unknown-unknown`, inline the module (base64) in **one self-contained `index.html`**; JavaScript is shell and loader only. |
| **Researched** | Programme Rust research 2026-10-30 (shared chapter, W4/W11 repos), re-read at this entry's stand-up 2026-11-08. Pin-time verification of every version and licence below is still owed and is a preflight item, exactly as in the sibling entries. |

**Verdict up front.** Roseford takes the **macroquad stack** — the W11
stack — for the same reason Withheld did, one size up: its rendering
surface is portraits, chamber backdrops, text, and ledgers, not an engine
scene graph, and macroquad's small wasm keeps the single-file delivery
safe while the part that ports back — the corruption state model — is
framework-free Rust either way. The Bevy stack (the W4 stack) is rejected
for this entry: nothing here validates the rig path, and Bevy's wasm
weight (upwards of 15 MB size-optimised in the programme's research, plus
~37% base64 inflation) is spent on nothing this design uses.

**The state model is zero-dependency.** The corruption model (DESIGN.md
§4), the two-axis fight, the memory ladder, and the Chapel Record are
authored in this repo against no crates at all (book chapter: Write From
Scratch). That is a decision, not an omission: the model is the port-back
artefact, and a dependency inside it would be a translation owed later.
Data tables (prayers, invokes, fragments, ward stat-blocks) are authored
as Rust tables in the core for the jam cut; a data-file format is a
preflight decision if the tables outgrow the source.

## Parts matrix (deltas from the programme research)

| Part | Pick | Notes |
|---|---|---|
| Rendering 2D | **macroquad** (MIT OR Apache-2.0) | Immediate-mode 2D over miniquad/WebGL1; first-class HTML5 output; one `cargo build --target wasm32-unknown-unknown`, small output. Chamber screens and portraits are drawn, not scenegraphed. |
| Sprite/frame playback | Hand-rolled frame-index playback over macroquad textures | The face-state portraits are a small fixed set; benimator (programme research) stays the fallback if the set grows. |
| Audio | **rodio** on the macroquad stack (programme research) | Wasm rides cpal's WebAudio backend; the shell resumes the AudioContext from a user gesture. Estate rule unaffected: generated audio is verified by file metrics only; nothing is played aloud in testing. |
| UI & dialogue | macroquad's immediate-mode UI for dev/debug only; game UI and the line-runner are from scratch | The dialogue here is stateful in ways no stock runner models (fragment checks inside Tuning events, phrases that advance on defeat) — a small from-scratch line-runner over the state model, per the programme research's fallback note. |
| State machines & simulation | **From scratch, zero-dependency** (see above) | Fixed-step deterministic evaluation (D-197); the same command sequence from the same state must produce the same fight, which is a test, not a hope (DESIGN.md §9). |
| Persistence | Chapel Record as a versioned, checksummed record in the shell's storage | Save/load round-trip is roadmap R-202; the record format is designed with the state model, not after it. |

## Rejected, with reasons on record

- **Bevy stack** — validates nothing this entry exists to validate; wasm
  weight unjustified at this rendering surface (see verdict).
- **ggez** — no official web target (programme research); the jam delivery
  *is* the web build.
- **Raw wgpu** — a graphics API, not a framework; from-scratch windowing
  and batching is not what this entry is for.
- **A dialogue framework (Yarn-class)** — WIP status and wasm caveats in
  the programme research, plus the stateful-line problem above; the
  from-scratch runner is smaller than the integration.

## Pin-time checks owed (preflight)

- macroquad + miniquad versions current against the pinned toolchain;
  licences re-verified on the crates.io listings at pin time.
- wasm output size measured against the single-file budget before the
  first build commit (the W11 precedent: 48 KB core wasm; this entry's
  budget is set at preflight, not assumed).
