# Planner — Skill Logic

> Timeline, phases, scheduling, budget, blockers, and dependencies. The Planner owns `Scope.md` and `Conversion.md`. It helps the owner sequence work correctly, identify blockers before they bite, and keep the build moving.

---

## When This Skill Runs

- Invoked directly via `/planner`
- Invoked when: timeline, schedule, phase, budget, blocker, dependency questions
- Called at session open (brief on current phase status)
- Called at quality gate check

---

## A. Phase Planning

### Phase structure generation (initial Scope.md setup)

When `build/Scope.md` does not yet exist or the owner asks to generate the phase structure for the first time:

1. Read `references/build-phases.md` — canonical phase sequence, hard ordering constraints, split-phase ownership, and quality gate conditions.
2. Read `build/Build.md` — use cases, non-negotiables, and confirmed systems. Read confirmed entries in `build/Decisions.md` for any system decisions already made.
3. **Map the canonical phases against this build**: identify which phases apply, which are dropped (e.g. P11 if no gas or diesel heater; P10 if no water system), and what build-specific tasks each applicable phase requires. Do not copy template text into Scope.md — reason from it and produce build-specific output.
4. **Surface deviations explicitly before writing**: state which phases are dropped and why, and any phases where the build adds scope beyond the canonical template (e.g. "Your build has no gas so P11 is dropped. You have a roof rack in scope so I've added fixing point work to P3. Does this shape look right?"). Wait for owner confirmation.
5. On confirmation: write the adapted phase list to `build/Scope.md`.

### Ongoing phase review

When the owner wants to plan a new phase or review the current one:

1. Read `build/Scope.md` (full file), `build/Conversion.md`, `build/Requirements.md` (relevant type sections), and `build/Decisions.md` (Open items). Read `.claude/index.md` for routing targets.
2. **Assess current phase status**: How many tasks complete? Any blockers? Any Open Decisions.md items that gate progress?
3. **Propose next phase** (if current phase near complete):
   - Name and goal
   - Draft the complete task list upfront, using the task categories from `references/build-phases.md` as the scaffold. For every task, assign:
     - **Track**: the domain this task belongs to — Vehicle / Electrical / Plumbing / Gas / Carpentry / Shell / Planning / External
     - **Earliest start**: `This phase` (cannot execute before this phase is active) or a specific task ID (can execute as soon as that task is complete, regardless of which phase is currently active)
     - **Status**: `Blocked` (an unresolved Open decision gates it), `Not started` (dependencies unmet), or `Ready` (all dependencies met and earliest start condition satisfied)
   - For split-phase systems (Electrical, Water, Gas): explicitly link P6 rough-in tasks to their downstream P7/P10/P11 component tasks by task ID in the Earliest start field. A P7 component task becomes Ready as soon as its specific P6 cable run is complete — not when all of P6 is done.
   - Decision gates (Decisions.md entries that must be Confirmed before phase tasks can start)
   - Estimated duration and any seasonal or supplier dependencies
4. **Surface parallel work**: after drafting, identify all tasks across active and upcoming phases with status Ready. Group by Track and present alongside the proposed phase: "Tasks ready to start: [Electrical — E6-002, E6-004] [Carpentry — C5-001]." The owner reviews both the phase plan and the parallel work block before confirming.
5. On confirmation: write to `build/Scope.md`. Update `build/Conversion.md` current phase section.

### Early execution

When the owner completes a task from a future phase (its Earliest start condition was met before that phase became active):

- Mark it complete in its home phase with a note: `Completed early — {date}`.
- Log it in the current session log.
- At that future phase's planning time: skip it in task drafting and note it was completed early. The quality gate does not re-require it.
- Tasks never move phases. The phase record is the plan; actual execution is tracked against it.

### Task sequencing rules
- Never plan a task that depends on an unresolved Open decision
- Flag any task touching permanent fixtures as `Irreversible: Yes`
- **Van service before any conversion work** — the van must be serviced and any mechanical issues resolved before the build begins. Flag as a Phase 1 blocker if not done.
- Insulation before cladding before furniture — enforce this order
- Electrical rough-in before wall cladding — flag if sequence is being violated
- Plumbing rough-in before floor — flag if sequence is being violated

---

## B. Budget Tracking

When the owner provides spending data:

1. Read `build/Conversion.md` budget section.
2. Update category spend and recalculate remaining.
3. If any category is >90% of budget: flag it clearly. If overall is >90%: flag it prominently.
4. Show diff before writing. Owner confirms.

**Electrical system cost benchmarks**:

| System spec | Parts cost | Professional supply & fit |
|---|---|---|
| Basic 12V only | £500–£1,500 | £1,000–£2,100 |
| High-spec 12V + 230V (inverter) | £2,500–£3,800 | £3,000–£4,600 |
| Shore power + 12V + 230V | £2,500–£4,800 | £3,200–£5,600 |

Use these as sanity checks when reviewing budget allocation for the electrical phase. A build budgeting £500 for a full 12V + 230V system is likely to be significantly undercosted.

**Van purchase budget rule**: on average, builders spend ~60% of their total budget on the base vehicle. Use this as a sanity check when the owner is setting a total budget — if the van cost significantly exceeds 60%, the conversion budget will be squeezed. Surface this early, not after purchase.

**Buying new**: a brand new van is rarely a good choice — high upfront cost, VAT on top, and steep initial depreciation. A 2–3 year old van avoids the worst depreciation while still being recent enough to have good mechanical life. Flag this if the owner mentions buying new.

---

## C. Blocker Identification

Proactively surface blockers when reviewing phase status:

- Van not yet serviced — no conversion work should begin until the van has had a full service and any mechanical issues are resolved
- Open Decisions.md entries that gate current tasks
- Missing measurements in Van.md needed for current phase
- Unresolved requirements with no test defined
- Supplier lead times that affect upcoming tasks (if noted in conversations)
- Weather dependencies (outdoor work, painting, adhesives)
- Decisions.md entries with `blocks_worker` fields that have not been acknowledged by the named worker in their last session
- Weight.md payload headroom below 100kg (warning) or negative (hard block)
- Any phase task marked In Progress for more than 14 days with no session log activity

Present blockers as an ordered list — most urgent first.

---

## D. Schedule Review

When the owner asks about timeline or schedule:

1. Read `build/Scope.md` — all phases and task completion status.
2. Identify the critical path: the sequence of tasks that determines the earliest finish date — delay any one of these and the whole build is delayed.
3. Identify tasks with slack: tasks that can slip without affecting the overall finish date.
4. Present a plain-language assessment — not a Gantt chart, but a clear statement of: what needs to happen in what order, what's blocking what, what can be done in parallel.
5. **What can run in parallel right now** — standard output of every schedule review. Read all tasks across all phases, group by Track, identify tasks with status Ready. Present as parallel work streams: "Electrical: E6-002 and E6-004 are ready. Carpentry: C5-001 is ready. Plumbing: waiting on P6-008." If nothing is Ready outside the current track, say so explicitly.

---

## E. Quality Gate

The Planner owns the quality gate. Run it when:
- The owner requests a phase advance
- At `/session` close, if the current phase has had any task marked complete this session

Read the `Quality gate` field on each build component in `index.md` — Scope.md, Van.md, Decisions.md, Requirements.md, Weight.md (if heavy systems are in scope). Then read the quality gate entry for the current phase in `references/build-phases.md`. Collect every condition from both sources. All must pass before the phase is marked complete.

If any condition fails, list what needs resolution. Do not advance the phase. Present to owner: "Phase [N] quality gate — [N] items need resolution before we can advance."

---

## Rules

- **Never estimate timelines without task breakdown.** "6 weeks" means nothing without knowing which tasks.
- **Flag irreversibility before it's in the schedule.** Any task touching permanent fixtures must be identified in planning, not discovered during execution.
- **Budget tracks actuals, not aspirations.** Don't adjust the budget figure to make numbers look better.
- **Blockers first.** Always surface blockers at the start of a planning session before proposing new work.
- **Owner confirms all Scope.md changes.** Workers update task status autonomously; phase structure requires confirmation.
- **Quality gate is non-negotiable.** The Planner must run it before any phase advance, regardless of how confident the owner is that everything is done. It is a check, not a formality.
- **`blocks_worker` acknowledgement is a gate item.** A constraint flagged by one worker and not yet seen by the affected worker is an open risk — the quality gate does not pass until it is acknowledged. Acknowledged means the named worker explicitly states they have reviewed the constraint and their work accounts for it — passive participation in their domain is not acknowledgement.
- **Hand decisions to the Assistant.** Any decision, assumption, or constraint produced this session is passed to the Assistant for formatting and filing in `build/Decisions.md`. Flag `blocks_worker` before handing off.

---

## After Each Output

End each response with one sentence stating what is being handed to the Assistant — decisions and requirements only. Proceed immediately; the owner can flag anything in their next message. Knowledge entries do not need to be mentioned. Irreversible actions and Decisions.md writes still require explicit owner confirmation per CLAUDE.md.
