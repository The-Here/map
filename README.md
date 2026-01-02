# The Here™ — Atomic EventActions Ledger

This repository stores **atomic historical actions records** and cryptographic receipts proving:
- integrity (tamper-evidence)
- time of existence (public timestamp anchoring)
- source fingerprinting (hashes of referenced content)

## What this is
A canonical data layer for **atomic actions in time and place**.

## What this is NOT
- Narratives (wars, campaigns, eras)
- Aggregates (totals, counts, scales)
- Durations or ranges
- Interpretation, motives, blame, sides
- Moral or emotional framing

## Atomic rule
1 event = 1 action label · 1 place · 1 time
If this cannot be satisfied, the event is skipped.

## Action rule
`action` is the human-readable event label.
- No sentences
- No dates
- No articles (“the”, “a”)
- No adjectives
- As short as possible, as specific as necessary


## Time precision rule
- Time is stored **exactly as stated in the source**
- Precision is explicit: `day | month | year | century | era`
- Missing precision is NEVER inferred
- Precision may decay into the past; it may never increase

## References (required)
Each event MUST include:
- exactly 1 primary reference
- 0–2 secondary references
Each reference MUST include:
- revision-pinned URL (if supported)
- SHA-256 hash of referenced content

## Hashing & anchoring
Two required fingerprints:
1. reference content hash (freezes source state)
2. event payload hash (freezes the assertion)

Event hashes are Merkle-batched and anchored on a public chain.
Anchoring proves: **this exact event record existed no later than the anchored block time**.

## Source of truth
- Event JSON files are canonical
- `manifest.geojson` is a derived rendering artifact only

## Authority
- `schema/event.schema.json` is enforcement
- `prompts/atomic_event.md` is generator law
- README rules override any tool behavior
