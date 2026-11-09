# Design — Roseford

**Status:** design of record at stand-up (Owner ruling D-1123, 2026-11-08). Wave E slot and heroine Isolde adopted as canon by Owner ruling D-1130 (2026-11-09).
No playable build exists yet; the build is a later rung gated on this design
and the week-15 preflight. Numbers in §4 are contracts: changing a band, a
price, or a gate is a design change and is recorded in the CHANGELOG.

**Canon core:** A resurrected shrine maiden descends a sealed dungeon whose
wards tune her — corruption is her power curve, her memory, and her price.

## 1. Premise

Isolde, keeper-maiden of the Roseford shrine, is found collapsed at the
dungeon stair by a passing pilgrim and wakes in the abandoned chapel above
the seal — alive again, with no memory of her death or of the rite that
sealed Roseford a generation ago. The seal is failing. She descends to
learn what she was, what the wards are for, and who raised her.

The dungeon's five seals are **hypnotic wards**: they were written to tune
whoever passes them — to slow a mind, bend it, and set it in the ward's
shape. The ward-bosses do not guard the floors by killing intruders. They
tune them. Every passage through Roseford changes her, whether she wins
or loses; the only question the game asks is how much of the tuning she
takes, and what she buys with it.

**Clean-room statement (D-1123):** the model source for this entry
contributed a premise skeleton only — a resurrected, amnesiac maiden; a
sealed dungeon; a return to learn the truth; mind-control and
transformation as genre tags. Everything below — cast, systems, floors,
text, numbers — is estate-original. No outside text, art, character
design, or scene content is used or stored in this repo.

## 2. Cast

- **Isolde** — the heroine. **26 years old, an adult**, keeper-maiden of
  the Roseford shrine, resurrected and amnesiac. Original character, new
  to the programme. Played character; the state model (§4) is hers.
- **The Rosekeeper** — the only other person in the cast. The prior
  keeper of Roseford, an adult of record, who performed the resurrection
  rite and set the five wards before vanishing below. Met in person only
  on the Rose Floor.
- **The ward-bosses** — the Bellwarden, the Veilwarden, the Throatwarden,
  the Mirrorwarden, and the Rosekeeper's ward-self on the Rose Floor.
  Excepting the last, these are **ward-constructs holding offices**, not
  persons: each is one seal given a voice, a courtesy title, and a tuning
  method. They speak, bargain, and tune; they are not people and are never
  written as people.
- **Lesser wardens** — hollow clergy: animated vestments that staff each
  floor. Constructs; combat obstacles and tuning sources, nothing more.

## 3. Shape of play

A short dungeon RPG. The **Chapel** (hub, above ground) holds the Chapel
Record, the fragment reading, and the descent stair. Below it, five
floors, each a compact sequence of chambers ending at a ward-boss and its
seal. Combat is turn-based (§5). Between floors she returns to the Chapel
only by the stair she has opened — descent is one-directional within a
run, which is what gives the price list in §4.4 its teeth.

A run is one descent. Endings (§7) resolve the run; the Chapel Record
(§4.6) persists across runs.

## 4. The state model — corruption as measured state

One integer carries the game. Everything else is derived.

### 4.1 Variables

| Variable | Range | Kind |
|---|---|---|
| **Corruption (C)** | 0–1000, integer | master state, per run |
| **Tuning Exposure (E)** | 0–100, integer | per boss fight |
| **Floor (F)** | 1–5 | position in the descent |
| **Fragments (M)** | 12 booleans | per run; titles persist (see §4.6) |
| **HP** | per-fight | combat resource, restored at shrines |

Derived, never stored: **Weather band** and **Face band** (§4.2), **pure
multiplier** and **invoke multiplier** (§4.5), **fragment visibility**
(§4.6). Purity is not a second meter: purity is `1000 − C` read from the
other end, and the design never lets the two drift apart.

### 4.2 Bands — the weather and the face ride the same state

Corruption bands are the estate's state-weather read on a person, and her
face state (F-code grammar) is locked to the same bands, so the state is
read on her and on the room at once — never on a number alone.

| C | Weather (the dungeon around her) | Face band (in tuning scenes) |
|---|---|---|
| 0–149 | **Clear** — dust, silence, cold stone | F-00 composed |
| 150–349 | **Humming** — the seals audibly hum; candle flames lean | F-03 edge |
| 350–549 | **Resonant** — her shadow answers a half-beat late | F-03 edge, deepening |
| 550–749 | **Drowned** — sound arrives muffled, as if underwater | F-05 peak |
| 750–1000 | **Rosedeep** — the stone sweats rose light; the hum is a voice | F-10 daze |

Band crossings are events, not thresholds passed in silence: each first
crossing in a run fires a short scene beat and is written to the Chapel
Record.

### 4.3 Monotonicity — the design's teeth

**C never decreases within a run.** No shop sells it back, no shrine
washes it, no prayer refunds it. A confession rite exists at the Chapel
and does exactly one thing: it ends the run (a recorded, honourable
retreat — not an ending, not a failure) so a new descent can begin at
C = 0. This is deliberate: corruption as a *price* only means something if
it cannot be un-spent.

### 4.4 Priced sources — what moves C

| Event | ΔC | Notes |
|---|---|---|
| Seal broken (ward-boss defeated) | **+60** | winning tunes her too — the seal's ward floods in as it breaks |
| Defeat by a ward-boss (a full Tuning taken) | **+120** | she wakes at the floor shrine; the boss's phrase advances (its dialogue and tuning pattern change); no floor progress is lost |
| Boss Tuning event (E fills, §5) | **+30** | per event, mid-fight |
| Defeat by a lesser warden | **+25** | she wakes at the floor shrine |
| The Listen rite (at a floor shrine) | **+40** | once per floor per visit; deliberately listening to the ward — the voluntary price |
| Fleeing a boss fight | **+10** | the boss resets; the dungeon notices |
| Band crossing | 0 | scenes and records only (§4.2) |

**The per-ward cap.** Each ward can contribute at most **200 C across a
whole run**, summed over every source above (its seal, its defeats, its
Tuning events, its floor's Listen rite, its flee price) — tracked per
ward in the Chapel Record. Five wards × 200 is exactly the 1000 ceiling:
the cap is what the ceiling is made of. The cap is also the anti-farming
law: no floor can be ground for more than its ward holds, so the deep
bands are unreachable early by construction — C ≥ 550 requires at least
three wards' worth of tuning, and C ≥ 750 at least four.

A floor's shrine is its checkpoint: rest restores HP and saves, and is
the only place the Listen rite may be taken.

### 4.5 The power curve — corruption pays, purity decays

- **Pure prayers** (her keeper's kit, 6 prayers): power multiplier
  `pure_mult = (1 − 0.12 × (F − 1)) × (1 − C/2500)`. On floor 5 at C = 0
  she prays at 0.52×; at C = 500, 0.42×. Purity stays *viable* — the
  numbers are a squeeze, never a wall — but it gets harder every floor,
  exactly as the wards intend.
- **Corrupted prayers (Invokes)** — one gifted by each ward, unlocking at
  C thresholds and scaling the other way, `invoke_mult = 0.6 + C/1000`:

| Invoke | Gift of | Unlocks at C | Effect sketch |
|---|---|---|---|
| The Answered Bell | Bellwarden | 150 | damage that rings again next turn |
| The Lowered Veil | Veilwarden | 300 | damage + blinds the target's tuning |
| The Borrowed Voice | Throatwarden | 450 | turns her next prayer into the boss's own phrase, at its strength |
| The Willing Mirror | Mirrorwarden | 600 | duplicates her last action at invoke strength |
| The Open Rose | Rosekeeper | 750 | the deep invoke; required for the Taking (§7) |

- **Listen (combat command)**: the next Invoke is ×1.5, at the price of
  +20 E. Listening is how she learns the phrases; it is also how the
  bosses learn her.

### 4.6 The memory ladder — truth is gated behind tuning

Twelve fragments of Isolde's memory. Revelation runs in three stages, in
the estate's ladder shape:

- **Hinted** — from C ≥ 150, unfound fragments show their titles in the
  Chapel Record ("*The Third Bell*", "*What the Voice Said*").
- **Glimpsed** — on acquisition, the fragment's partial text.
- **Known** — the assembled reading: with 12/12 fragments the Chapel
  Record can be *read whole*, and the truth of her death is stated in
  full, in her own recovered words.

Acquisition: F1 is given at the resurrection (the prologue). F2–F10 are
floor events — floors 1–4 hold two each, one on the seal-break path and
one on the defeat-or-tuned path, and floor 5 holds one (F10, its
seal-break), so a floor pays a fragment for either outcome but the
*second* fragment asks the other outcome of a later visit or a harder
fight. **F11** requires C ≥ 550: a memory her mind only releases once she
is Drowned — and by the per-ward cap (§4.4) that depth cannot be reached
before the third ward. **F12** requires C ≥ 750: it exists only in the
Rosedeep.

The arithmetic is the design: seals alone give 5 × 60 = 300, and every
Listen on the way down gives 200 more — 500, the most a never-tuned
descent can hold. Reaching 550 asks at least two Tuning events, or one
defeat, on top of a full voluntary descent; reaching 750 asks a run that
has taken real tuning from at least four wards. **A purity run cannot
read the whole truth** — it ends at 10 fragments, or 11 for a run that
was tuned once and stopped there. That is not a punishment; §7 makes the
not-knowing a complete ending, chosen with open eyes.

### 4.7 The Chapel Record

Cross-run bookkeeping in the programme's bookkeeping shape (cf. Withheld's
denial book): fragments found (with Glimpsed text), band crossings, every
Tuning taken and from whom, endings reached, runs confessed away. It
persists between runs; fragment *titles* persist into a new run once
Hinted, their texts do not. The Record is the game's memory even when
Isolde's is reset — the player is the second keeper of what she was.

## 5. Battle shape

Turn-based command battle against a ward-boss (lesser wardens use the
same loop minus the Exposure axis). Commands: **Pray** (pure kit),
**Invoke** (corrupted kit, if unlocked), **Listen**, **Guard** (halves
E gain this turn; restores a small, fixed amount of HP once per fight),
**Flee** (boss fights only, +10 C; lesser fights flee free to the chamber
door).

The boss fights on **two axes at once**: her HP, and her **Tuning
Exposure E** (0–100). E fills +8 per boss turn, +20 when she Listens, and
by each ward's signature pressure (below). When E fills, a **Tuning
event** fires instead of an attack: +30 C, a face-state beat at her
current band, a fragment check (§4.6), E resets to 0, and the boss's fill
rate rises +2 for the rest of the fight. If her HP empties first, she
takes the full Tuning (+120) and wakes at the shrine. **The boss is
trying to tune her; killing her is only its bluntest instrument** — and a
player who Guards and Listens carelessly can be tuned to the next band
without ever being in danger of dying, which the Chapel Record will
remember even if she wins.

Fixed-step, deterministic evaluation throughout (D-197): the same command
sequence from the same state always produces the same fight, byte for
byte where the medium allows.

## 6. Floors and wards

The Chapel above; five floors below. Each ward tunes by a different
sense, and each floor's pressure teaches the axis it prices.

| F | Floor | Ward-boss | Tuning method (signature pressure) |
|---|---|---|---|
| 1 | **The Bell Floor** | The Bellwarden | Rhythm: E fills on counted beats; its Tuning events land on the exhale. Listen is strongest here — and most expensive. |
| 2 | **The Veil Floor** | The Veilwarden | Gaze: E fills while she looks at it; Guard is *averting her eyes*, and Praying blind costs accuracy. |
| 3 | **The Throat Floor** | The Throatwarden | Voice: her own prayers echo back inverted; pure prayers feed E (+4 each) while Invokes starve it. The floor where the pure kit first turns against her. |
| 4 | **The Mirror Floor** | The Mirrorwarden | Self-image: it fields her uncorrupted self as its champion. Pure prayers strike at half strength *by rule, not by stat* — the mirror will not fight itself. |
| 5 | **The Rose Floor** | The Rosekeeper (ward-self) | The truth floor: no signature pressure. Every axis at once, at the plain rates — by now the player knows exactly what each point of C costs and buys. |

Lesser wardens per floor are one stat-block in five vestments (jam scope,
§8). Floor shrines sit before each boss chamber.

## 7. Endings — both complete, neither a fail state

- **The Purity Ending — "She Reseals the Door."** Defeat the Rosekeeper's
  ward-self with C < 750. Isolde reseals Roseford with the keeper's craft
  she still owns, walks up out of the dark, and keeps her post in the
  Chapel. She ends the game knowing 10–11 fragments' worth of truth —
  and the ending text says plainly that she *chose* the not-knowing, and
  what it cost the people the sealed thing would have told her about.
  A complete ending: credits, Record entry, fragment texts kept.
- **The Surrender Ending — "She Takes the Seat."** Enter the Rose door
  with C ≥ 750 and the Open Rose invoke: the final fight gains a second
  win condition, **the Taking** — endure five Tuning events without her
  HP emptying, and the ward-self yields the seat. F12 unlocks, the
  Record reads whole, and the full truth of her death is stated: who
  raised her, why, and what the wards were always for. She becomes the
  new Rosekeeper; the last scene is the next pilgrim finding *her*
  collapsed at the stair. A complete ending on identical footing —
  credits, Record entry, everything kept.
- **Mid-fight crossing:** if C crosses 750 during the final fight, the
  Taking becomes available the moment it does, announced in the fight
  text. The player chooses, in the fight, with the price list known.
- **Confession** (§4.3) is neither ending: a recorded retreat, available
  always, gated behind nothing (cf. R-403: safety and exit options are
  never progression-gated).

## 8. Scope fence — the jam cut

**IN (the jam build):** the Chapel; five floors as compact chamber
sequences; one lesser-warden stat-block per floor; five ward-boss fights
on the two-axis loop; 6 pure prayers; 5 Invokes; 12 fragment texts; the
Chapel Record with cross-run persistence; both endings; the Listen rite;
band-crossing beats as text-and-portrait scenes; face-state portraits in
the estate's F-code set; ≥6 screens (18+ gate / Title / How to Play /
Chapel / Descent-and-battle / Pause-Settings / Ending) in one
self-contained `index.html`.

**OUT (later rungs, named so nobody gold-plates the jam cut):** free-roam
floor maps; animated scene layers beyond the face-state portraits; voice;
a second lesser-warden type; New Game+ content beyond fragment titles; the
Torogao port itself (the port-back delivers the state model and its
tables, not a build); any Android build.

## 9. Programme gates

This entry passes the programme's GJ series (book chapter: Jam
Checklist), adapted where the design bites:

- **GJ-01** GAMEOTRON process documented for this entry, incl. language chain.
- **GJ-02** Single self-contained `index.html` assembles and runs offline.
- **GJ-03** ≥6 screens present.
- **GJ-04** Human ideation-approval gate recorded (the D-1123 ruling is
  this entry's record).
- **GJ-05** itch project created under NTRanch, slug `ntranch/roseford`
  (project creation is an Owner-gated step; the 20-project limit applies).
- **GJ-06** Week-15 toolchain preflight passed and recorded.
- **GJ-07** 18+ flag set, content warnings listed, itch ToS screen passed
  (verified live at entry).
- **GJ-08** Seahawk playtest pass done; breakage log filed to bloch.
- **GJ-09** Port-back note + language verdict filed; §9 transfer filing made.
- **State-model gate (this entry's own):** the §4 model is covered by the
  programme's half-validation / half-adversarial test split before the
  build is called done — validation: priced sources sum as tabled, band
  derivation, fragment acquisition paths, both endings reachable;
  adversarial: C clamped to [0, 1000] under every source, per-ward
  contribution clamped to 200 under every source mix, C monotonic
  under every command sequence, F11/F12 unreachable below their gates,
  ending exclusivity (no state satisfies both endings' conditions at
  once), E reset and escalation bounded.
- **Visual gate (D-221):** written SHOULD + final-artifact crops at
  viewing size + per-item PASS/FAIL against the Quality Bar chapter;
  the Owner's eye supersedes.
- **Determinism (D-197):** fixed-step evaluation; identical re-runs of a
  scripted fight produce identical state traces.
