---
last_updated: {YYYY-MM-DD}
last_updated_by: Architect
phase: {current-phase-slug}
---

# Weight Manifest

> Tracks cumulative build weight. Every worker that specifies a heavy component adds an entry.
> Architect owns the totals and payload headroom calculation.
> Update this file whenever a heavy component is confirmed in Decisions.md.

## Payload Summary

| Field | Value |
|-------|-------|
| GVW (from Van.md) | -tbd- |
| Kerb weight (from Van.md — verified) | -tbd- |
| Maximum payload | -tbd- |
| Estimated build weight (sum below) | -tbd- |
| Actual build weight (weighbridge) | -tbd- |
| Remaining headroom (payload − build weight) | -tbd- |

> **Warning threshold**: Flag when remaining headroom drops below 100kg. Hard stop if headroom goes negative.
> **Weighbridge requirement**: A weighbridge ticket is required before any phase involving heavy fixed systems is marked complete.

---

## Component Weights

| ID | Component | System | Worker | Est. weight (kg) | Actual weight (kg) | Decision ref | Phase | Notes |
|----|-----------|--------|--------|-----------------|-------------------|-------------|-------|-------|
| W-001 | Base vehicle (kerb weight) | Vehicle | Mechanic | -tbd- | -tbd- | — | P0 | From V5C or manufacturer spec — verify on weighbridge |

---

## Weight Entry Format

Workers add a row to the table above when a heavy component is confirmed in Decisions.md. Use this format:

```
| W-{NNN} | {component name} | {Electrical / Plumbing / Insulation / Carpentry / Vehicle / Heating} | {Worker} | {kg or -tbd-} | {kg or —} | DEC-{NNN} | P{N} | {notes} |
```

- **Est. weight**: Use manufacturer spec or typical value. Mark as `~{value} (unverified)` if approximate.
- **Actual weight**: Fill in when item is received and weighed.
- **ID**: W-001, W-002, etc. — sequential, never reused.

---

## Weight Log

{Dated notes when significant changes to the manifest are made — e.g., "2024-03-15: Battery bank confirmed at 28kg (LiFePO4 100Ah). Headroom updated."}
