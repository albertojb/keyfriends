# Spec: Epic 1 — Backlog Words

## Goal
Add 6 words (COW, PIG, BEE, FOX, OWL, HAT) to the words mode. Each requires a new creature entry in the `C` library. After this epic, 19 of 26 letters are covered.

## New letters introduced
| Word | New letters |
|---|---|
| COW | W |
| PIG | P I |
| BEE | E |
| FOX | F X |
| OWL | L |
| HAT | H |

## Acceptance criteria

### AC-1: Creature SVGs
Each of the 6 new creatures (cow, pig, bee, fox, owl, hat) has an entry in the `C` object with:
- `m`: motion type — `"ground"` for cow, pig, fox, hat; `"air"` for bee, owl
- `s`: inline SVG meeting all of:
  - Simple shapes, few colors, friendly look
  - Drawn facing right (or symmetrical)
  - ViewBox roughly 200 wide
  - Instantly recognizable at `min(17vh, 135px)` — no label needed
  - Color palette consistent with existing creatures (soft, muted, `--ink` for outlines)

### AC-2: WORDS array
All 6 words appear in the `WORDS` array as `{w:"COW", c:"cow"}` etc.

### AC-3: Word slots fit
With 11 words total (5 existing + 6 new), the word shelf renders without overflow on a 1280×800 landscape screen. The longest words (3 letters each) still fit their slot sizing.

### AC-4: Shelf slots fit
The gang shelf renders 11 filled slots without wrapping past `max-height: 22vh` on a 1280×800 landscape screen.

### AC-5: Five constraints unbroken
After the change:
- [ ] No audio added
- [ ] No reading required to play (all new pictures are unambiguous without text)
- [ ] No new browser storage used
- [ ] Palm-proof: mashing random keys during a new word round does not advance state
- [ ] Calm: no score, no timer, no fail animation added

### AC-6: No regressions
Numbers mode (0–9) and the existing 5 words (CAR, BUS, DOG, CAT, SUN) play identically to before.

### AC-7: Single file
`keyfriends.html` remains a single self-contained file. No new external assets, imports, or script tags added.

## Out of scope for this epic
- Words covering J, K, M, Q, V, Y, Z (Epic 2)
- Mid-round celebration (Epic 3)
- Pacing tuning (Epic 4)
- Touch input, profiles, audio — permanently out of scope per GOAL.md
