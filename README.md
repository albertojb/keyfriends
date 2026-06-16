# Key Friends

A keyboard-only educational game for pre-reading toddlers. Teaches key recognition, number quantities, and simple word spelling — with no reading required, no audio, and no mouse.

**[▶ Play it live](https://kf.jbtcr.com/)**

![Key Friends screenshot](https://kf.jbtcr.com/)

---

## What it does

Two modes, chosen by a parent on the start screen:

**Numbers mode** — Press a digit; that many themed vehicles count up under the numeral (3 trains for "3", 5 firetrucks for "5"). Each digit has its own signature vehicle.

**Words mode** — A picture clue spells a short word. Each correct letter drops a "letter friend" into its slot. Finish the word and the creature drives across the screen.

Both modes share a **collect-the-gang** goal: a shelf at the bottom fills as the child completes items. Fill it and everyone parades, then it resets.

---

## How to run

Just open `keyfriends.html` in any modern browser. No install, no build step, no network calls. Single file, zero dependencies.

For a fully child-proof session, run it inside your OS kiosk or guided-access mode — a web page can't block OS-level shortcuts like Alt+F4 or Cmd+W on its own.

---

## Design principles

These constraints are intentional. Changes should preserve all five.

1. **No audio.** All feedback is visual.
2. **No reading required.** Letters and numbers are matched as symbols; everything else is pictures.
3. **Calm, not overstimulating.** Muted palette, one thing moving at a time, slow easing, no score, no timer, no fail state.
4. **Palm-proof input.** Full-palm presses and clumsy mashing never break the game. Only the correct key does anything.
5. **No browser storage.** Session-based by design.

---

## How to extend

### Add a word

1. Confirm the picture creature exists in the `C` object in the `<script>`. If not, add it (see below).
2. Add `{w:"COW", c:"cow"}` to the `WORDS` array. Keep words short — three letters work best.

### Add a creature or vehicle

Add an entry to `C` with a motion type and an inline SVG:

```javascript
cow: {
  m: "ground",
  s: `<svg viewBox="0 0 200 130">...</svg>`
}
```

- `m` is one of `"ground"`, `"air"`, or `"water"` — controls the bobbing animation and vertical position.
- The SVG should be simple shapes, few colors, friendly, drawn facing right, viewBox roughly 200 wide.

### Change which vehicle a number uses

Edit the `numCreature` map at the top of the `<script>`:

```javascript
const numCreature = { "1": "car", "2": "bus", ... };
```

### Tune pacing

| Thing to change | Where |
|---|---|
| Vehicle crossing speed | `.mover` animation duration in CSS (default `5s`) |
| Count-up stagger | `COUNT_STAGGER_MS` constant (default `200`) |
| Count-up hold time | `COUNT_HOLD_MS` constant (default `1400`) |
| Clue grow range | `CLUE_OPACITY_MIN` / `CLUE_SCALE_MIN` constants |

---

## Open backlog

- [ ] Expand the word list with more drawable three-letter words (COW, PIG, BEE, FOX, OWL, HAT)
- [ ] Optional milestone celebration every five items collected
- [ ] Optional persistence variant using `localStorage` (separate build — current version is intentionally sessionless)
- [ ] Optional name-first letter set as an easier on-ramp

---

## License

MIT — see [LICENSE](LICENSE).

Built for a specific toddler. Themes and difficulty are tuned for that child; treat the word list, creature set, and pacing as the first things to localize for a different kid.
