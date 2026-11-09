# Bloch candidate — A late programme entry mirrors the founding scaffold, not its siblings' finished state

- origin_lane: ntranch
- content_label: sfw
- evidence: ~/workspace/ntranch-jam-repos-20261030/withheld/ git history (scaffold commit cbad74b, 33 files, vs the v1.0.0 tree, ~120 files incl. built book HTML, previews, web build); ~/workspace/ntranch-jam-repos-20261030/roseford/ (stood up 2026-11-08 under D-1123 against that scaffold commit)

## Lesson

When the Torogao Jam Program gained a fifteenth entry by Owner ruling after the original fourteen had all shipped v1.0.0, the obvious reference — a sibling's working tree — was the wrong specification for the new repo's baseline. The finished tree carries a whole programme's worth of build state (compiled book HTML, preview videos, release SHA256SUMS, a v1.0.0 version line) that a day-one repo must not be born with. The true baseline specification was the sibling's **scaffold commit** in git history: 33 named files, an all-unchecked roadmap, an empty attempts log, version 0.1.0, and no SHA256SUMS (that file is a release artefact, born at R-603, not a scaffold artefact).

## Standing rule proposed

For any repo stood up to join an existing family late: derive the baseline file set from a sibling's scaffold commit (`git show <first-commit> --stat`), never from its current tree. Current tree state answers "what does a finished one look like"; only the scaffold commit answers "what is one born with". The same check settles convention questions (checksums, version lines, placeholder files) that the finished tree answers wrongly for a baseline.
