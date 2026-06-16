# Decisions — Key Friends

One line per key decision: decision — why — which GOAL line it serves.

---

## Epic 1 (2026-06-15)

- HAT kept over HEN — HAT covers H, A, T; SUN set precedent for inanimate objects with a face; parent confirmed — serves "every addition helps a toddler encounter every letter"
- OWL assigned m:"air" (flying) not m:"ground" (perched) — spec was explicit; caught by independent review cycle and fixed before merge — serves "single HTML file with zero dependencies" (correct motion class matters for rendering)
- BEE and OWL split into a separate PR (1-B) from ground creatures (1-A) — keeps diffs reviewable; air vs ground is a natural boundary — serves build-cycle guardrail "one PR per story"
- Stacked PR approach: 1-B targeted 1-A branch — resulted in 1-B not reaching main automatically on merge; future runs should target main directly or merge stacking branch explicitly after close

## Pacing (2026-06-16)

- Crossing animation slowed: `--drive-ms` 5000ms → 9000ms, `--parade-ms` 5500ms → 10000ms — parent found the default speed too fast for the toddler to track the creature; serves "calm, not overstimulating"
