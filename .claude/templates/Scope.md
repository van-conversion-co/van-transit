---
last_updated: {YYYY-MM-DD}
last_updated_by: {worker-name or "owner"}
---

# Scope

Phases, goals, tasks, dependencies, decision gates, and irreversibility flags.

**Active phase**: -tbd-

---

## Phase 0 — Setup

**Goal**: Van acquired, vision documented, all dimensions measured, build plan in place.
**Status**: Active
**Quality gate**: All dimensions in Van.md measured. Build.md confirmed by owner. Scope.md Phase 1 tasks defined. Use case hierarchy in Build.md constrains phase order.

### Tasks

| ID | Task | Worker | Track | Depends on | Earliest start | Irreversible | Est. duration | Acceptance criteria | External blockers | Status |
|----|------|--------|-------|-----------|----------------|--------------|---------------|--------------------|--------------------|--------|
| P0-001 | Service the van | Mechanic | Vehicle | — | This phase | No | 1d | Full service completed; any mechanical issues resolved or logged as blockers in Van.md | Garage availability | -tbd- |
| P0-002 | Measure all cargo area dimensions | Architect | Planning | — | This phase | No | 2h | All fields in Van.md Cargo Area populated, no -tbd- remaining | — | -tbd- |
| P0-003 | Document van condition (rust, panel, mechanicals) | Mechanic | Vehicle | P0-001 | This phase | No | 1h | Van.md Rust, Panel & Shell, and Mechanicals sections complete | — | -tbd- |
| P0-004 | Confirm use case hierarchy in Build.md | Planner | Planning | — | This phase | No | 1h | Build.md confirmed by owner; Non-Negotiables list populated | — | -tbd- |
| P0-005 | Define Phase 1 scope | Planner | Planning | P0-002, P0-004 | This phase | No | 2h | Scope.md Phase 1 section written and confirmed by owner | — | -tbd- |
| P0-006 | Identify all regulatory requirements (insulation, electrics, gas) | Assistant | Planning | — | This phase | No | 2h | Requirements.md populated with Constraint entries for relevant regulations | — | -tbd- |

---

## Phase Template

```markdown
## Phase {N} — {Name}

**Goal**: {What this phase delivers — one sentence}
**Status**: {Not started / Active / Complete / Paused}
**Use case alignment**: {Which use cases from Build.md this phase primarily serves — phases should be ordered so higher-ranked use cases are enabled earlier}
**Quality gate**: {Specific conditions that must be true before this phase is considered complete}

### Tasks

| ID | Task | Worker | Track | Depends on | Earliest start | Irreversible | Est. duration | Acceptance criteria | External blockers | Status |
|----|------|--------|-------|-----------|----------------|--------------|---------------|--------------------|--------------------|--------|
| P{N}-001 | {task description} | {Worker} | {Track} | {ID or —} | {This phase / task ID} | {Yes/No} | {Nh or Nd} | {How to verify done} | {Supplier lead time / specialist availability / weather / —} | Not started |

### Decision gates

{Decisions that must be in Decisions.md as Confirmed before tasks in this phase can proceed}

### Commissioning tests

{For any phase installing a system: the specific test that must pass before phase advance. For phases involving heavy fixed components: include Weight.md update and payload headroom verification.}

### Phase notes

{Anything specific to this phase — seasonal constraints, supplier lead times, known risks}
```

---

## Deferred Items

{Items removed from active phases but not abandoned — with rationale and suggested future phase}

## Future Phases

{Ideas for phases not yet planned}
