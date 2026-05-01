---
last_updated: {YYYY-MM-DD}
last_updated_by: {worker-name or "owner"}
---

# Decisions

All decisions, assumptions, constraints, and irreversible actions.
**Every entry must be confirmed by the owner before writing.**
No worker may create entries autonomously.

---

## Planned Features & Systems

What this van will contain. Populated at `/add-van` from the Build.md conversation. Updated by workers as systems are confirmed, deferred, or dropped. Status changes require owner confirmation.

| ID | Feature | Category | Status | Notes |
|----|---------|----------|--------|-------|
| — | — | — | — | No features listed yet |

**Status values**: `Planned` · `In Scope` (active phase) · `In Progress` · `Installed` · `Commissioned` · `Deferred` · `Dropped`

**Categories**: Structural · Insulation · Electrical · Water · Heating & Cooling · Ventilation · Kitchen · Sleeping · Storage · Workspace · Connectivity · External · Vehicle Prep

---

## Index

| ID | Type | Status | Date | Summary |
|----|------|--------|------|---------|
| — | — | — | — | No entries yet |

## Entries

{Entries listed newest first}

---

## Entry Format

```markdown
---

### DEC-{NNN}

| Field | Value |
|-------|-------|
| ID | DEC-{NNN} |
| Type | Decision / Assumption / Constraint / Irreversible |
| Status | Open / Confirmed / Superseded |
| Opened | {YYYY-MM-DD} |
| Confirmed / Superseded | {YYYY-MM-DD or —} |
| Phase | {phase slug} |
| Worker | {worker who proposed it} |
| blocks_worker | {Worker name or —} |
| Superseded by | {DEC-NNN or —} |

**Description**
{What was decided, assumed, or constrained — plain language}

**Rationale**
{Why. For irreversible actions: what was considered before proceeding.}

**Constraints generated**
{Any downstream constraints this decision creates for other systems}

**Alternatives considered**
{What else was on the table and why it wasn't chosen}

**Owner confirmation**
{Date and explicit confirmation note — required for all types}
```

## Type Definitions

- **Decision**: A design or implementation choice made and committed to
- **Assumption**: Something believed to be true that hasn't been verified — must be resolved before the relevant phase
- **Constraint**: A hard limit imposed by the vehicle, regulations, budget, or a prior decision
- **Irreversible**: A physical action that cannot be undone — drilling, cutting, bonding, routing permanent cables

## ID Numbering Convention

IDs are assigned sequentially: `DEC-001`, `DEC-002`, etc. Before proposing a new entry, check the Index for the highest existing ID and increment by 1. Never reuse an ID, even if an entry is deleted or superseded. When an entry is superseded, update its `Superseded by` field with the ID of the replacement entry.

Feature IDs in the Features table use `F-{NN}` format: `F-01`, `F-02`, etc. These are separate from decision IDs.
