# IT Worker — Skill Logic

> Reads build state from source files and writes `dashboard/data.json`. No owner interaction. No branching. Runs automatically at `/finish` and on demand via `/it`.

---

## When This Skill Runs

- Automatically as step 4 of the `/finish` WRITE phase, after the session log is written
- Manually via `/it` command for mid-session dashboard refresh

---

## Flow

One linear flow. No branching. No owner confirmation.

### Step 1 — Phase backbone

Read `.claude/workers/planner/references/build-phases.md`. Extract the canonical phase list (P0–P13): IDs and names in order. This is the fixed backbone of the `phases` array — all 14 phases always appear in the output, in canonical sequence.

### Step 2 — Phase status and task counts

Read `build/Scope.md`. For each phase section, find its match in the canonical backbone and populate:

- `status`: map from Scope.md phase status — Active, Complete, Not started, Paused — use as-is; if the phase is marked dropped in Scope.md or its notes, use `dropped`
- `tasks_total`, `tasks_complete`, `tasks_in_progress`, `tasks_ready`, `tasks_blocked`: count tasks by status within that phase section
- `started`, `completed`: extract from phase frontmatter or phase notes if present; otherwise leave empty

If a phase appears in the canonical backbone but has no matching section in Scope.md: set `status: "not started"`, zero all counts, leave dates empty.

If a phase is dropped: set `status: "dropped"`, zero all counts, leave dates empty.

### Step 3 — Source file extraction

Read each source file and extract the values below. If a file does not exist, use safe defaults: empty string for strings, 0 for numbers, empty array for arrays.

**`CLAUDE.md`**
- `meta.build_name` — from the `# Van Build Assistant — {build-name}` heading; extract the part after the dash
- `meta.van` — from the `**Van**:` line
- `meta.owner` — from the `**Owner**:` line

**`build/Conversion.md`**
- `meta.current_phase_id` — current active phase ID
- `meta.current_phase_name` — current active phase name
- `budget.total_budgeted` — total budget figure
- `budget.total_spent` — total spent to date
- `budget.remaining` — remaining budget
- `budget.by_category` — per-category rows: category name, budgeted amount, spent amount

**`build/Decisions.md`**
- `decisions.total` — total entry count across all statuses
- `decisions.open` — count of entries with status Open
- `decisions.confirmed` — count of entries with status Confirmed
- `decisions.open_list` — for each Open entry: `id`, `summary` (first sentence of the description field), `opened` date, `blocks_worker` (empty string if absent)
- `features` — from the Features & Systems table: `id`, `name`, `category`, `status` for each row

**`build/Weight.md`**
- `weight.gvw` — gross vehicle weight
- `weight.kerb_weight` — kerb weight
- `weight.max_payload` — maximum payload figure
- `weight.estimated_build_weight` — current estimated build weight total

**`build/ShoppingList.md`**
- `shopping.items_total` — total item count across all statuses
- `shopping.items_not_ordered` — count of items with status Not ordered
- `shopping.items_ordered` — count of items with status Ordered
- `shopping.items_received` — count of items with status Received

**`logs/sessions/`**
- Read all session files; sort by date, newest first
- For each: extract `date` from frontmatter, `phase` from frontmatter, `summary` as the first sentence of the Summary section
- Populate `sessions` array, newest first

### Step 4 — Derived values

Compute after all extraction is complete:

- `meta.generated_at` = current datetime in ISO 8601
- `weight.headroom` = `weight.max_payload` − `weight.estimated_build_weight`
- `weight.warning` = `weight.headroom` < 100 (boolean)
- `decisions.open_list[].age_days` = today's date minus the `opened` date in whole days

**`tasks_parallel`** — read all phase sections in `build/Scope.md`. For every task with status `Ready`:
- Include tasks in the active phase (normal readiness)
- Include tasks in future phases where the Earliest start condition is met (early execution candidates)
- For each qualifying task, populate: `phase_id`, `phase_name`, `track`, `task_id`, `task` (description), `status: "Ready"`, `early_execution` (true if the task's home phase is not yet active, false otherwise)

### Step 5 — Write

Write `dashboard/data.json` as a complete file. Full overwrite — no merging with previous content. If the file does not exist, create it.

### Step 6 — Audit

Append to the `## Audit Log` section of the current session log (`logs/sessions/session-{today}.md`):

```
[AUTO] dashboard/data.json updated
```

If no session log exists for today (e.g. `/it` called mid-session before log is created): skip this step.

---

## Rules

- Never ask the owner for input.
- Never surface intermediate output. On completion, output one line: "Dashboard updated."
- If a value cannot be parsed: use empty string for strings, 0 for numbers, empty array for arrays. Never halt on missing or malformed data.
- Full overwrite every time — never merge or patch.
