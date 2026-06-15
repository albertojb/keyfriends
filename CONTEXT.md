# Context — Key Friends

Durable notes for future runs. Read this alongside GOAL.md and ROADMAP.md.

## Architecture

Single HTML file, no build, no deps. All creatures are inline SVGs in the `C` object at the top of `<script>`. All playable words are in the `WORDS` array. Adding a word = add one `C` entry + one `WORDS` entry.

## Creature conventions

- `m:"ground"` — drives at road level (CSS top:46%), bobs 7px
- `m:"air"` — flies at sky level (CSS top:18%), bobs 22px
- `m:"water"` — floats at water level (CSS top:50%), bobs 10px
- ViewBox should be roughly 200px wide (SVG scaled by `.bobber{width:min(24vh,180px)}`)
- Clue picture (word scene): `min(17vh,135px)` — must be instantly recognizable at this size
- Colors: soft/muted palette, `#2e3a44` for outlines/pupils, no bright saturated fills

## Word constraints

- All 3-letter words (word slot sizing is tuned for 3 letters; 4+ requires `wsz` logic check)
- No reading required — creature picture must make the word clear without text
- Q is permanently excluded — no usable 3-letter toddler word

## Epic 1 review finding

The independent reviewer caught OWL being set to `m:"ground"` (perched) when the spec required `m:"air"` (flying). Fixed in the review cycle. Spec is authoritative on motion type — check it before assigning `m:`.

## Stacked PR note

Epic 1-B was stacked on the 1-A branch. When 1-A merged to main and 1-B merged to its base (1-A branch), 1-B's commits didn't land on main automatically. Future runs: either target all PRs at main (no stacking), or remember to bring the stacking branch to main after merge.

## Shelf layout (gang)

Word slots: `min(11vw, 92px)`. At 11 words (current): fits single row at 1280px, 2-row wrap at 360px within `max-height:22vh`. Next check point: Epic 2 brings it to ~18 words — verify shelf still fits before merging.
