# ROADMAP — Key Friends
_draft_

Letters currently covered: A B C D E F G H I L N O P R S T U W X — **19 of 26**

---

## ✅ Done

### Release 0 — Foundation
- Single-file game engine: numbers mode (0–9) and words mode (3-letter words)
- 11 creatures / vehicles with inline SVGs
- Collect-the-gang shelf + parade finale
- Palm-proof keyboard input, escape-hold exit
- Named constants for all timing values (code-degunker pass)
- Open-source release: GitHub + live at sail.zo.space/keyfriends

### ✅ Epic 1 — Backlog words (shipped 2026-06-15)
Added: COW, PIG, BEE, FOX, OWL, HAT — 6 new creature SVGs.
New letters: E F H I L P W X — coverage 11 → **19 of 26**

Still missing: J K M Q V Y Z (Q excluded per GOAL.md)

---

## Epic 2 — Full alphabet (7 words, 6–7 new letters)
_Unspecced. Will spec when Epic 1 ships._

Target words (candidates — confirm before speccing):
| Letter(s) | Word | Creature |
|---|---|---|
| J + M | JAM | jar with a face |
| K + Y | KEY | key with a face (or baby goat KID for K, YAK for Y) |
| V | VAN | van (ground vehicle) |
| Y | YAK | yak (ground animal) — if KEY doesn't cover Y |
| Z | ZIP | zipper creature, or ZAP (lightning bolt) |
| Q | — | **explicitly excluded** — no drawable 3-letter toddler word; note in game comment |

Goal: every letter A–Z appears in at least one word (Q excepted with a code comment explaining why).

---

## Epic 3 — Engagement layer
_Unspecced. Will spec when Epic 2 ships._

A small mid-round celebration every 5 items collected — prevents boredom as the word set grows longer. Must stay calm (no audio, no score, no timer). One option: a quick mini-parade of the last 5 collected, then resumes. Must not add fail state or pressure.

---

## Epic 4 — Content polish
_Unspecced. Will spec when Epic 3 ships._

- Pacing review with the full word set: verify COUNT_HOLD_MS / WORD_DONE_MS still feel right
- SVG legibility pass: every creature picture must be instantly recognizable at min(17vh, 135px)
- Verify shelf layout holds on landscape screens with 20+ word slots
