# NORTH STAR
Every addition to Key Friends must help a pre-reading toddler encounter every letter without getting bored, while staying inside a single HTML file with zero dependencies and zero audio.

---

## Goal
Build a calm, keyboard-only game a parent can hand to any toddler on any device — no setup, no reading, no breakage — until every letter has been seen and the child stays engaged through a full round.

## Core Decision
Every addition is evaluated against one question: does it help a pre-reading toddler encounter every letter without getting bored, inside the existing single-file, zero-dep model?

## Definition of Done
- Every letter (A–Z, Q and Z handled explicitly) appears at least once across the word set.
- A child can play a complete session — numbers 0–9, all words — without disengaging.

## Out of Scope
- Touch / tap input
- Per-child profiles or custom word lists
- Audio of any kind
- Persistence or saved progress
- Multi-file architecture, build tooling, or external dependencies
- Mouse interaction

## Fixed Constraints
1. Single HTML file — no build step, no framework, no external assets, no network calls.
2. No audio. All feedback is visual.
3. No reading required. Letters and numbers are the content; everything else is pictures.
4. Calm, not overstimulating. Muted palette, one thing moving at a time, no score, no timer, no fail state.
5. Palm-proof input. Only the correct key does anything; everything else is ignored.
6. No browser storage. Session-based by design.
