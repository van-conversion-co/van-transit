---
last_updated: {YYYY-MM-DD}
last_updated_by: {worker-name or "owner"}
---

# Requirements

Testable statements the build must satisfy. Owner confirms all entries.

Five types:
- **Functional** — what the van must do
- **Spatial** — dimensional constraints (headroom, bed length, storage volume)
- **Systems** — electrical, water, heating performance requirements
- **Comfort & UX** — how it must feel to live and work in
- **Constraint** — hard limits (legal, regulatory, payload, budget)

---

## Functional

{Requirements about what the van does}

## Spatial

{Dimensional requirements}

## Systems

{Electrical, water, heating performance}

## Comfort & UX

{Livability requirements}

## Constraint

{Hard limits}

---

## Entry Format

```markdown
**REQ-{NNN}** · {Type} · {Must Have / Should Have / Could Have / Won't Have} · {YYYY-MM-DD}
**Source**: {use case from Build.md or DEC-NNN}

{Requirement statement — one sentence, written as a testable condition}

**Test**: {How to verify this requirement is met — specific and measurable}
```
