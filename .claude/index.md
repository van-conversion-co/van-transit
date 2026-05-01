# Component Index

State and structure authority for the Van Build Assistant. Defines what exists, who owns it, what state it is in, and what conditions must be true at each phase gate. Behavioural rules live in `CLAUDE.md`. The Active Cross-Worker Constraints registry lives in `.claude/workers/assistant/SKILL.md` Section E.

---

## Build Components

### `build/Conversion.md`
- **Path**: `build/Conversion.md`
- **Purpose**: Master project status — current phase, timeline, budget overview, current tasks, open decisions count
- **Owner worker**: All workers on phase change; session open/close
- **Write when**: Phase advances, budget changes, new tasks identified, open decisions resolved
- **Read for context when**: Every session startup; every worker session; weekly review
- **Confirms before write**: Owner confirms phase advances and budget changes; workers update tasks autonomously
- **Stale when**: Phase unchanged for >30 days with no session log activity

### `build/Van.md`
- **Path**: `build/Van.md`
- **Purpose**: The specific vehicle — make, model, year, all measured dimensions, payload capacity, condition, quirks, modification history, ongoing observations
- **Owner worker**: Mechanic (vehicle facts); Architect (spatial measurements)
- **Write when**: New measurement taken, new quirk discovered, modification made, condition observation added
- **Read for context when**: Any spatial planning (Architect), any weight calculation (Architect, Electrician), any vehicle work (Mechanic)
- **Confirms before write**: Owner confirms all measurements (must be physically measured, not estimated or recalled); observations logged autonomously
- **Stale when**: Any field marked `-tbd-` or `~{value} (unverified)` is referenced by an active phase task or layout decision
- **Quality gate**: All dimensions referenced in the current phase are physically measured — no estimates, no `~` values. No dimension contradicts a confirmed layout decision in Decisions.md (Architect verifies before gate passes)

### `build/Build.md`
- **Path**: `build/Build.md`
- **Purpose**: Vision — what this van is for, use cases in priority order, non-negotiables, trade-offs the owner has consciously accepted, use hierarchy
- **Owner worker**: Populated via facilitated conversation in `/add-van`; owner owns the content; Architect reads it for every spatial decision
- **Write when**: Use case added or re-prioritised, trade-off accepted, non-negotiable established
- **Read for context when**: Any layout decision (Architect), any system sizing decision (Electrician, Plumber), any trade-off question
- **Confirms before write**: Owner confirms every entry — this document cannot be autonomously updated

### `build/Requirements.md`
- **Path**: `build/Requirements.md`
- **Purpose**: Testable statements the build must satisfy. Five types: Functional, Spatial, Systems, Comfort & UX, Constraint. Each has a statement, MoSCoW priority, source (use case or decision), and test method
- **Owner worker**: Each domain worker proposes requirements for their domain; owner confirms
- **Write when**: New requirement identified from Build.md, from a decision, or from a measurement; requirement status updated
- **Read for context when**: Any design decision in any worker session; quality gate check; phase planning
- **Confirms before write**: Owner confirms all new requirements and priority changes
- **Stale when**: Any requirement has no defined test method and is in scope for the current phase
- **Quality gate**: Every system in scope for the current phase has a commissioning test defined in Requirements.md

### `build/Scope.md`
- **Path**: `build/Scope.md`
- **Purpose**: Phases, goals, tasks, dependencies, decision gates, irreversibility flags. One section per phase. Each task has: ID, description, worker domain, dependencies, irreversibility flag, status
- **Owner worker**: Planner
- **Write when**: Phase advances, task status changes, new task added, dependency resolved
- **Read for context when**: Session startup (current tasks), quality gate, weekly review, any worker checking what's next
- **Confirms before write**: Owner confirms phase advances and new irreversibility flags; task status updated autonomously by workers
- **Stale when**: Active phase with no task status update in >14 days
- **Quality gate**: All tasks in the current phase have status Complete or explicitly deferred with owner confirmation. No `-tbd-` fields in critical tasks.

### `build/Decisions.md`
- **Path**: `build/Decisions.md`
- **Purpose**: All decisions, assumptions, constraints, and irreversible actions. Each entry has: ID (`DEC-NNN`), type (Decision / Assumption / Constraint / Irreversible), status (Open / Confirmed / Superseded), description, rationale, constraints generated, alternatives considered, `blocks_worker` (names the downstream worker this entry constrains — used at session startup to surface cross-domain dependencies), and owner confirmation. Also contains the Planned Features & Systems table — the living inventory of everything the van will contain, updated as systems are confirmed, deferred, or dropped
- **Owner worker**: Assistant is the sole writer. All other workers propose entries; Assistant formats, assigns IDs, presents for owner confirmation, and writes. No worker writes to this file directly
- **Write when**: Decision made, assumption established, constraint identified, irreversible action taken, feature status changes
- **Read for context when**: Any decision session (check for conflicts), quality gate, session close audit, session startup (surface any `blocks_worker` entries relevant to the day's domain)
- **Confirms before write**: Owner confirms every entry individually — no bulk confirmation
- **Stale when**: Any `Open` entry is older than 14 days
- **Quality gate**: No Open entries blocking the current phase. Any irreversible action taken this phase has a confirmed entry with owner confirmation recorded. Any `blocks_worker` entry created this phase has been acknowledged by the named worker.

### `build/Knowledge.md`
- **Path**: `build/Knowledge.md`
- **Purpose**: Domain encyclopedia — terms, techniques, materials, product names, standards, concepts. Includes Contacts & Suppliers section (Administrator-owned). Auto-populated by workers. No confirmation required for new entries; owner can correct or flag
- **Owner worker**: Auto-populated by all workers; Contacts section owned by Administrator
- **Write when**: New term, technique, product, or contact encountered; existing entry needs correction
- **Read for context when**: Any worker session involving unfamiliar domain; document ingestion; Administrator needs supplier history
- **Confirms before write**: No confirmation required for new entries; corrections require owner confirmation

### `build/Lessons.md`
- **Path**: `build/Lessons.md`
- **Purpose**: Generalizable insights from this build. Each lesson: ID, category, the lesson (general), context (what happened), and the test — would this help someone doing the same build who hadn't made the mistake yet?
- **Owner worker**: Auto-populated at session close; owner can add manually
- **Write when**: Autonomously at `/finish` close; manually via owner input
- **Read for context when**: Any decision involving a technique or approach that has a past lesson
- **Confirms before write**: Owner confirms at session close before writing; manual additions confirmed by owner

### `build/Weight.md`
- **Path**: `build/Weight.md`
- **Purpose**: Cumulative build weight tracker. Every worker that specifies a heavy component adds its estimated and actual weight. Totals build weight and shows remaining payload headroom against Van.md figures
- **Owner worker**: Architect (owns totals and payload calculation); all domain workers add their components
- **Write when**: Any component with significant mass is confirmed in Decisions.md (battery bank, water tank, diesel heater, furniture framing, floor, cladding); actual weight confirmed on delivery
- **Read for context when**: Any sizing decision that has weight implications; quality gate for any phase with heavy fixed systems
- **Confirms before write**: Workers add their components autonomously; Architect confirms the total and headroom calculation
- **Stale when**: Phase involves heavy fixed systems and Weight.md has not been updated since phase start
- **Quality gate**: For phases involving heavy fixed systems (battery bank, water tank, diesel heater, furniture framing): payload headroom has been calculated and confirmed by Architect since phase start

### `build/ShoppingList.md`
- **Path**: `build/ShoppingList.md`
- **Purpose**: All parts confirmed via Decisions.md, grouped by phase and category, with quantities, specifications, estimated and actual costs, sources, and order status
- **Owner worker**: Shopper
- **Write when**: New component confirmed in Decisions.md; order placed or received; price updated
- **Read for context when**: Shopper generating shopping list; Planner assessing budget; any worker checking component specifications
- **Confirms before write**: Owner confirms new Shopping List entries; order status updates are autonomous
- **Stale when**: A component confirmed in Decisions.md is not yet present in ShoppingList.md

---

## Log Components

### `logs/sessions/session-YYYY-MM-DD.md`
- **Path**: `logs/sessions/session-YYYY-MM-DD.md`
- **Purpose**: Dated log per session — phase status, session summary, open questions, blockers, action items, audit trail of all changes made
- **Owner worker**: You (session open/close); workers append during session
- **Write when**: Session opens (create), session closes (`/finish` command), significant event mid-session
- **Read for context when**: Session startup (most recent), weekly review (all since last review)
- **Confirms before write**: Session summary confirmed by owner at close; audit entries appended autonomously
- **Stale when**: Active build phase with no session log in >7 days

### `logs/weekly/week-YYYY-WNN.md`
- **Path**: `logs/weekly/week-YYYY-WNN.md`
- **Purpose**: Between-sessions summary — phase status, open items, time-sensitive flags (weather, deliveries, bookings). Lighter than session close
- **Owner worker**: You (`/review` command)
- **Write when**: `/review` invoked, or owner requests a catch-up
- **Read for context when**: Session startup after a gap of >3 days
- **Confirms before write**: Owner confirms before writing

---

## Conversation & Document Components

### `conversations/YYYY-MM-DD-{slug}.md`
- **Path**: `conversations/`
- **Purpose**: Logged interactions — tradespeople, suppliers, forums, video debriefs. Summary, key findings, routing of what was learned
- **Owner worker**: Assistant (`/new-conversation`)
- **Write when**: `/new-conversation` invoked
- **Read for context when**: Related topic comes up; Administrator needs supplier history; Shopper needs quote history
- **Confirms before write**: Owner confirms routing of extracted knowledge; log itself is autonomous

### `documents/index.md`
- **Path**: `documents/index.md`
- **Purpose**: Index of all ingested documents — manuals, quotes, specs, guides. Date, title, source, summary excerpt, file reference
- **Owner worker**: Assistant (`/new-doc`)
- **Write when**: New document ingested
- **Read for context when**: Any worker session involving a system covered by an ingested document
- **Confirms before write**: Autonomous index entry; routing of extracted knowledge confirmed by owner

---

## Dashboard Components

### `dashboard/data.json`
- **Path**: `dashboard/data.json`
- **Purpose**: Structured build state for dashboard consumption — phases, decisions, budget, weight, shopping, sessions, features, and parallel-ready tasks. Full overwrite on every `/finish`.
- **Owner worker**: IT
- **Write when**: Every `/finish` (automatic, step 4 of WRITE); `/it` command (manual mid-session refresh)
- **Confirms before write**: No — fully autonomous
- **Stale when**: Last modified date is older than the most recent session log

---

## Templates

All templates live in `.claude/templates/`. To add a new component, register it here first, then create the template.

| Template | Creates | Instantiated by |
|---|---|---|
| `templates/Build.md` | `build/Build.md` | `/add-van` section G — via facilitated conversation, not direct copy |
| `templates/Conversation.md` | `conversations/YYYY-MM-DD-{slug}.md` | `/new-conversation` |
| `templates/Conversion.md` | `build/Conversion.md` | `/add-van` section H — assembled from other components, not direct copy |
| `templates/Decisions.md` | `build/Decisions.md` | `/add-van` section F |
| `templates/Knowledge.md` | `build/Knowledge.md` | `/add-van` section F |
| `templates/Lessons.md` | `build/Lessons.md` | `/add-van` section F |
| `templates/Requirements.md` | `build/Requirements.md` | `/add-van` section F |
| `templates/Scope.md` | `build/Scope.md` | `/add-van` section F |
| `templates/ShoppingList.md` | `build/ShoppingList.md` | `/add-van` section F |
| `templates/Van.md` | `build/Van.md` | `/add-van` section E |
| `templates/WeeklyReview.md` | `logs/weekly/week-{YYYY-WNN}.md` | `/review` |
| `templates/Weight.md` | `build/Weight.md` | `/add-van` section F |
