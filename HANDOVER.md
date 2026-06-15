# Key Friends: developer handover

A keyboard-only educational game for a pre-reading toddler. It teaches him to find keys, builds numbers as quantities, and spells simple words. No audio, no mouse, no reading required. The whole thing is one file: `keyfriends.html`.

This doc gets a new developer productive without reading every line first.

## What it is

- One self-contained HTML file. No build step, no framework, no external assets, no network calls.
- Two modes, picked by a parent on the start screen: numbers and words.
- Numbers mode: press a digit, that many themed vehicles count up under the numeral (3 trains for "3", 5 firetrucks for "5"). Each digit has a fixed vehicle.
- Words mode: a picture clue spells a short word. Each correct letter drops a "letter friend" into its slot; finishing the word sends the creature driving across.
- Both modes share a "collect the gang" goal: a shelf at the bottom fills as the child completes items. Fill the shelf and everyone parades, then it resets.

## How to run

Open `keyfriends.html` in any modern browser. That is the entire setup.

The first parent keypress or button tap requests fullscreen (browsers require a user gesture for that, so it cannot fire on load). For a truly child-proof session, run it inside the OS kiosk or guided-access mode; a web page cannot block OS-level shortcuts like Alt+F4 or Cmd+W on its own.

## Design constraints (do not break these)

These are the reasons the code looks the way it does. Changes should preserve all five.

1. No audio. All feedback is visual.
2. No reading required. Letters and numbers are the content, matched as symbols; everything else is pictures.
3. Calm, not overstimulating. Muted palette, one thing moving at a time, slow easing, no score, no timer, no fail state.
4. Palm-proof input. Full-palm presses and clumsy mashing never break the game or skip ahead. Only the correct key does anything; everything else is ignored.
5. No browser storage. `localStorage` and `sessionStorage` are not used. They break the in-app artifact preview, and the game is session-based by design.

## File structure

Single file, three parts:

1. `<style>`: all CSS, including the calm palette in `:root`, the keycap and slot styling, the creature animations, and the keyboard helper.
2. HTML body: `#menu` (parent start screen), `#game` containing `#scene-num` and `#scene-word`, the shared `#gang` shelf, `#hint` keyboard, and `#exit` ring.
3. `<script>`: all logic.

## Core data structures

- `C`: the creature library. Keys are creature names; each value is `{m, s}` where `m` is motion type (`ground`, `air`, `water`) and `s` is an inline SVG string. Adding art means adding entries here.
- `WORDS`: array of `{w, c}` where `w` is the uppercase word and `c` is the creature key drawn as its picture. Every word's letters must exist on the keyboard and its picture must exist in `C`.
- `numCreature`: maps digits 1 through 9 to the vehicle that counts up for that number. Zero has no vehicle on purpose (it teaches "none").
- `numColors`: per-digit signature color, used by the number friend and its gang tile.
- `letterPal`: rotating soft colors for letter friends by position.

## State

A small set of module-level variables drives everything:

- `mode`: `'numbers'` or `'words'`.
- `current`: the key the child must press right now. In words mode this is the active letter.
- `locked`: true while a reward animation plays. The input handler ignores all keys when locked. This is the main palm-proofing mechanism.
- `collected`: a `Set` of items already finished this round (digits, or words).
- `curWord`, `curCreature`, `wi`: the active word, its picture, and the index of the next letter to press.

## Control flow

Both modes follow the same shape: pick a target the child has not finished, wait for the correct key, play a reward, record it, repeat. When nothing is left, run the finale and reset.

Numbers:
1. `nextNumber()` picks a random uncollected digit, shows the numeral, unlocks input.
2. On the correct key, the handler sets `locked = true` and calls `rewardNumber()`.
3. `rewardNumber()` builds `count` vehicle units in `#countrow`, each delayed by 0.2s, then after the count finishes adds the digit to `collected`, fills its gang tile, and calls `nextNumber()`.

Words:
1. `nextWord()` picks a random uncollected word and calls `renderWord()`.
2. `renderWord()` draws the clue, scales and brightens it by progress (`wi / length`), and lays out the letter slots: filled letters show friends, the active letter is a keycap, pending letters are greyed.
3. On the correct letter, `letterCorrect()` advances `wi` and re-renders. If the word is done it drives the creature across, records the word, and moves on; otherwise it unlocks after a short delay.

Finale:
- `finale()` builds a parade and animates it across, then clears `collected`, rebuilds the shelf, and starts the next round. The numbers parade leads with a train pulling the number friends as carriages.

## Input handling

One `keydown` listener in capture mode handles all input.

- It calls `preventDefault()` on everything except F11 and F12, so browser shortcuts and scrolling stay out of the way.
- It ignores key-repeat events (`e.repeat`), so a held key does not spam.
- It ignores all input while `locked` is true.
- Numbers accept the top row and the numpad (`e.code` is checked for both `Digit` and `Numpad`).
- Letters compare the uppercased `e.key` to `current`.
- Escape is the parent exit: hold it 1.5s and a ring fills, then the game returns to the menu. A single tap does nothing, so the child cannot quit by accident.

## How to extend

Add a word:
1. Confirm the picture creature exists in `C`. If not, add it first.
2. Add `{w:"COW", c:"cow"}` to `WORDS`. Keep words short (three letters work best for this age).

Add a creature or vehicle:
1. Add an entry to `C` with a motion type and an inline SVG. Match the existing style: simple shapes, few colors, friendly, drawn facing right, viewBox roughly 200 wide.
2. To use it as a number's count-up vehicle, point a digit at it in `numCreature`.

Change which vehicle a number uses: edit `numCreature`.

Tune difficulty:
- Hide the upcoming letters: in `renderWord()`, stop setting `textContent` on the pending slots (leave them blank).
- Drop the keyboard helper by default: uncheck it on the menu, or default `hintToggle` off.
- Start letters with a smaller set (for example, the letters in the child's name) by replacing `WORDS` with a shorter list or adding a name word.

Tune pacing:
- Vehicle crossing speed: the `drive` keyframe duration on `.mover` (currently 5s).
- Number count-up speed: the `0.2` stagger and the `count*200+1400` hold in `rewardNumber()`.
- Clue grow range: the `0.35 + 0.65*prog` opacity and `0.65 + 0.35*prog` scale in `renderWord()`.

## Known limits

- A web page cannot block OS-level shortcuts. Use kiosk or guided-access mode for full lockdown.
- The on-screen keyboard helper assumes a standard QWERTY layout. Other physical layouts will mislead the position hint.
- The number count-up caps visually at 9 units in a row, which fits a typical landscape screen. Smaller or portrait screens may crowd.
- Word slots and the shelf assume landscape. Very short viewports will feel tight.

## Open backlog

- Expand the word list with more drawable three-letter words (COW, PIG, BEE, FOX, OWL, HAT).
- Optional smaller milestone in long sets (a small celebration every five collected) so wins come faster.
- Optional persistence for a locally hosted copy, using `localStorage`. Note this version intentionally avoids it; a persistent build is a separate variant.
- Optional name-first letter set as an easier on-ramp.

## Provenance

Built and iterated for a specific toddler. Themes and difficulty are tuned for that child; treat the word list, creature set, and pacing as the first things to localize for a different kid.
