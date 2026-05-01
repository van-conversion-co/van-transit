---
last_updated: {YYYY-MM-DD}
last_updated_by: Shopper
phase: {current-phase-slug}
---

# Shopping List

> Only include items with confirmed Decisions.md entries. No speculative items.
> All specifications must reference a DEC-NNN entry.

## Budget Summary

| Category | Estimated | Actual | Remaining budget |
|----------|-----------|--------|-----------------|
| Electrical | — | — | — |
| Insulation | — | — | — |
| Carpentry & furniture | — | — | — |
| Plumbing | — | — | — |
| Heating & ventilation | — | — | — |
| Vehicle prep | — | — | — |
| Miscellaneous | — | — | — |
| **Total** | **—** | **—** | **—** |

---

## Phase 0 — Setup

{No purchased items in Phase 0}

---

## Phase {N} — {Name}

### {Category}

| Item | Specification | Qty | Unit | Est. price | Actual price | Source | Decision ref | Lead time | Status | Notes |
|------|--------------|-----|------|-----------|-------------|--------|-------------|-----------|--------|-------|
| {item} | {spec} | {n} | {each/m/kg} | £{est} | £{actual or —} | {supplier} | DEC-{NNN} | {days or —} | Not ordered / Ordered / Received | {flags} |

---

## Item Status Key

- **Not ordered** — confirmed in Decisions.md, not yet purchased
- **Ordered** — purchase placed, awaiting delivery
- **Received** — in hand, ready to use
- **Substituted** — different item received; see Notes

## Shopping List Rules

- Every item must have a Decision reference.
- Flag items with lead times >7 days — they may affect phase start dates.
- Flag safety-critical items (cable, fuses, battery terminals, gas fittings) sourced from marketplace — specialist or trade supplier recommended.
- After every significant order, update Conversion.md budget with actual spend.
