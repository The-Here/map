# The Here™ — Atomic Actions Ledger

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

## Terminology
- Atomic unit = Action
- The word “event” is forbidden everywhere

## Atomic rule
1 action = 1 action label · 1 place · 1 time
If this cannot be satisfied, the action is skipped.

## Action title rule
`action` is the human-readable label.
- No sentences
- No dates
- No articles (“the”, “a”)
- No adjectives
- As short as possible, as specific as necessary

## time.source_text
- Verbatim date string exactly as shown in the source
- MUST NOT be normalized, parsed, reordered, localized, or rewritten
- Preserves original spelling, order, punctuation, and locale
- This field is the authoritative historical record

# time.display
- Human-readable display string for UI only
- Generated only when formatting does not increase precision
- Formatting only (e.g. 1914, Aug 3)
- MUST NOT add, assume, infer, or resolve any missing or ambiguous components
- MUST NOT exist for ambiguous numeric dates (e.g. 8/3/1914)
- If absent, clients MUST render time.source_text verbatim

# time.precision
- Machine-usable precision marker
- One of: day | month | year | century | era
- Derived strictly from time.source_text
- This is the only time field allowed for logic, sorting, or filtering

# Precision rules
- Time is stored exactly as stated in the source
- Precision is explicit and minimal
- Missing precision is NEVER inferred
- Precision may decay into the past
- Precision may never increase
- Formatting MUST NOT affect precision

# Ambiguous dates
- Numeric-only dates (8/3/1914, 3/8/1914) are treated as ambiguous
- Ambiguity is never resolved by the system
- time.display MUST NOT be generated for ambiguous dates
- Only textual month names (August 3, 1914, 3 August 1914) are considered unambiguous

# Display format
- Canonical display format (when allowed):
YYYY, Mon D → 1914, Aug 3
- Month abbreviation uses Title Case (Aug, not AUG)

# UI invariant
If time.display is missing, the interface must render time.source_text exactly as stored.

# Core principle
Precision encodes truth. Formatting encodes convenience. Ambiguity is preserved, never resolved.

## References (required)
Each action MUST include:
- exactly 1 primary reference
- 0–2 secondary references
Each reference MUST include:
- revision-pinned URL (if supported)
- SHA-256 hash of referenced content

## Hashing & anchoring
Two required fingerprints:
1. reference content hash (freezes source state)
2. action payload hash (freezes the assertion)

Actions hashes are Merkle-batched and anchored on a public chain.
Anchoring proves: **this exact action record existed no later than the anchored block time**.

## Source of truth
- Action JSON files are canonical
- `manifest.geojson` is a derived rendering artifact only

## Authority
- `schema/action.schema.json` is enforcement
- `prompts/atomic_action.md` is generator law
- README rules override any tool behavior

## Repository invariants
- Files under `actions/golden/` are the only canonical action definitions; all other files are derived, illustrative, or tooling artifacts.
- Canonical status is determined exclusively by filesystem path, never by JSON fields or metadata.
- `index.json` and `manifest.geojson` are always rebuildable and must never be cited as sources of truth.

