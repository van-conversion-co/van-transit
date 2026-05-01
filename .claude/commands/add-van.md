---
description: Start a new van build
---
> The entry point for every new build. Runs a structured Q&A with the owner, branches on ownership status, then creates all foundational components across four checkpointed stages. Only run once per build.
---

## When This Skill Runs

Once, when the owner invokes `/add-van`. Detected by the absence of any components in `build/`.

---

## Voice

Infrastructure is invisible. Never announce gate results, stage names, or what you're about to check internally. Intake is a conversation — ask questions naturally, one at a time. After each checkpoint confirmation, act without announcing it, then say what was done. "Your files are ready." Not "Starting Stage 2 now."

---

## 0. Gate

Check whether `build/Conversion.md` exists. If it does: say "Looks like this build is already set up — run `/start` to continue." and stop.

Do not announce the check or its result. If no build exists, go straight to Q1 with no preamble.

---

## Intake

Ask questions one at a time, in order. Wait for each answer before asking the next. Never combine questions.

Sub-state (Path A, B1, B2, B3) is internal — never use these labels with the owner. Resolve sub-state silently from the answers and let it shape what gets created.

Skip any question whose answer is already clear from a prior answer.

Respond to what the owner tells you as a person would. If they describe something interesting or unusual about their plans, acknowledge it briefly before moving to the next question. Don't treat this as a form.

A light progress signal is appropriate after Q4 or Q5: "Just a couple more questions." No stage announcements.

---

### Q1 — The van

> "What van are you building in — make, model, year?"

**Silent evaluation after Q1:**

| Answer | Internal path |
|---|---|
| Make, model, year stated; owner says they own it or implies physical access | Path A |
| Make, model, size (wheelbase + roof height) all stated; no specific unit yet | B1 — no unit |
| Specific unit identified (listing found, viewing done, or purchase imminent) | B1 — unit found |
| Make and model stated; size not decided | B2 |
| Van not yet chosen | B3 |

Ownership and sub-state are resolved from Q1 context clues (tense, phrasing, specific vs. general). If unclear after Q1, Q2 resolves it.

---

### Q2 — Ownership or specificity (ask only if Q1 left this unclear)

**Path A branch** (van sounds owned but condition unknown):
> "What condition is it in — anything to note from the history or a first look?"

**B1 branch** (specific unit identified):
> "Tell me anything you know about this particular van — mileage, condition notes from a viewing, anything from the listing."

**B2 branch** (make/model known, size unclear):
> "Have you decided on the body size — wheelbase and roof height — or is that still open?"

**B3 branch** (van not yet chosen):
> "How far along are you on choosing one — do you have a make and model in mind, or are you still narrowing that down?"

Re-evaluate sub-state after Q2 if B3 answer reveals make/model or size.

---

### Q3 — Purpose

> "What do you want this van to do — what kind of trips, how long, who's coming?"

---

### Q4 — Budget

> "What's your rough budget? Does that include buying the van?"

---

### Q5 — Timeline

> "When does it need to be ready? Any hard deadlines?"

---

### Q6 — Technical resources

> "Are you working from any technical resources — manuals, wiring diagrams, build specifications?"

---

### Q7 — Name

> "What do you want to call it — a nickname, a project name, whatever you'll actually use."

---

## Checkpoint 1 — Ready to build?

Ask simply: "Got everything I need — want me to set this up now?"

Wait for confirmation. If the owner corrects anything, update it silently and proceed.

**On confirmation**: create all files from Stage 2 through Stage 3 without narrating the process. No "Starting Stage 2", no "checking templates", no status updates during creation. When all files are created, output the completion summary from Section J. The summary is the only output from the creation process.

---

## Stage 2 — Phase 0 Infrastructure

### D. Phase 0 — Infrastructure (All Paths)

> The repo ships with only `.claude/`, `CLAUDE.md`, `README.md`, and `.gitignore`. Everything below is created fresh by this skill. If any file already exists (re-run scenario), ask the owner: overwrite, skip, or merge?

#### D1. Create all directories
```
build/
logs/sessions/
logs/weekly/
conversations/
documents/
```

#### D2. Personalise CLAUDE.md
Replace `{build-name}`, `{van-make-model-year}`, `{owner-name}`, `{start-date}` with actual values from the owner's input. If any value is still unknown after Beat 2, leave the placeholder — do not guess.

For B2: use make/model only, e.g. `{Ford Transit — size tbd}`. For B3: use `-tbd-`.

#### D3. Create `.claude/settings.json`

```json
{
  "permissions": {
    "allow": [
      "Read(**)",
      "Bash(git add:*)",
      "Bash(git commit:*)",
      "Bash(git push:*)"
    ],
    "deny": []
  }
}
```

Starts with `Read` only. Permissions are added progressively as the owner approves them.

#### D4. Create index files

**`documents/index.md`**:
```markdown
# Document Index

| Date | Title | Type | Summary | File |
|------|-------|------|---------|------|
```

**`conversations/index.md`**:
```markdown
# Conversation Index

| Date | With | Topic | Summary | File |
|------|------|-------|---------|------|
```

---

State what was just created: directories, personalised `CLAUDE.md`, `settings.json`, `documents/index.md`, `conversations/index.md`. Then proceed immediately to Stage 3.

---

## Stage 3 — Van.md and Skeleton Components

### E. Van.md (All Paths)

Create `build/Van.md` using `.claude/templates/Van.md`. Population method depends on sub-state:

#### Path A

Pre-fill from published specs for the confirmed make/model/year/wheelbase/roof — same as B1. Mark all pre-filled dimension values as `~{value} (source: published specs — verify before irreversible cuts)`.

Fields that cannot be estimated from published specs (registration, mileage, rust condition, existing fixings, MOT expiry): mark `-tbd-`.

Any details the owner mentioned about the van's condition or quirks: add to the Quirks & Observations section.

#### B1 — Size known

Pre-fill from published manufacturer specifications for the confirmed make/model/year/wheelbase/roof type. Mark every pre-filled value as `~{value} (unverified — verify on purchase)`.

Fields that cannot be estimated from published specs — registration, mileage, rust condition, existing fixings, MOT expiry — mark `-tbd-`.

If a specific unit has been identified, add any known details to the Quirks & Observations section — mileage from the listing, condition notes from a viewing — marked `~{value} (unverified — pre-purchase inspection pending)`.

Add this note at the top of Van.md:

> "Dimensions and specifications are sourced from published manufacturer data for this size. All values must be physically verified on purchase. Do not treat any value here as measured until confirmed."

If a specific unit is identified, also add:

> "Specific unit identified — pre-purchase inspection required before any irreversible action. See Scope.md task P0-016."

#### B2 — Size unknown

Pre-fill make, model, and year. Leave all cargo dimension fields (cargo length, width, height, wheelbase, roof height) as `-tbd-`. Engine options and approximate payload ranges may be noted where model-level data is available, marked `~{value} (unverified — model-level estimate)`.

Add this note at the top of Van.md:

> "Van model confirmed. Size (wheelbase and roof height) not yet selected — cargo dimensions are -tbd- until size is chosen. Invoke the Architect to select the size that best fits your use cases."

#### B3 — Model unknown

Create Van.md with section headers only. Mark all fields `-tbd-`.

Add this note at the top of Van.md:

> "Van model not yet chosen. Once model and size are confirmed, invoke the Architect worker to pre-fill from published specs."

Set frontmatter: `last_updated: {today}`, `last_updated_by: auto — add-van`.

---

### F. Skeleton Components (All Paths)

Create files using templates. Sub-state determines Phase 0 tasks and active vs. skeleton status for dimension-dependent components.

- `build/Decisions.md` — from `.claude/templates/Decisions.md`. All paths active.
- `build/Requirements.md` — from `.claude/templates/Requirements.md`. B2: dimension-dependent requirements flagged pending size. B3: use-case requirements only — system-specific requirements deferred until model chosen.
- `build/Scope.md` — from `.claude/templates/Scope.md`. Phase 0 tasks differ per sub-state — see below.
- `build/Weight.md` — from `.claude/templates/Weight.md`. Path A / B1: pre-fill kerb weight from published specs, mark `~{value} (source: published specs)`. B2: approximate model-level payload range if available. B2: approximate model-level payload range if available, dimensions `-tbd-`. B3: skeleton only.
- `build/ShoppingList.md` — from `.claude/templates/ShoppingList.md`. Path A / B1: active, empty. B2: active for dimension-independent items only, note that dimension-dependent quantities are held. B3: skeleton only.
- `build/Knowledge.md` — from `.claude/templates/Knowledge.md`. Pre-populate with any domain terms mentioned in owner's input. Mark status `Needs confirmation` on anything inferred. All paths.
- `build/Lessons.md` — from `.claude/templates/Lessons.md`. Empty. All paths.

Set frontmatter on each: `last_updated: {today}`, `last_updated_by: auto — add-van`.

#### Phase 0 Task Lists

##### Path A

Van.md is pre-filled from published specs at setup — layout planning can start immediately. Physical measurement is only required before irreversible cuts (floor, framing, roof apertures) — not as a gate for planning.

Starting state assessment — before writing Scope.md Phase 0 tasks, evaluate what the owner has already done:
- If existing build resources were mentioned: add an action item to ingest them via `/new-doc` or `/new-conversation`
- If van condition is already documented: mark the condition documentation task complete

Do not generate the same boilerplate task list every time — generate tasks that reflect actual starting state.

##### B1 — Size known

All planning tasks proceed immediately. Execution tasks are blocked until the van is physically in hand. If a specific unit has already been identified, replace P0-014 with `P0-014 | Complete purchase of identified unit | Owner | — | —` and add `P0-014a | Log unit details to Van.md Quirks | Administrator | — | —`. The pre-purchase inspection (P0-016) should run before purchase if possible.

| ID | Task | Worker | Track | Depends on | Earliest start | Blocked until |
|---|---|---|---|---|---|---|
| P0-001 | Ingest existing research — manuals, forums, build guides | Assistant | Planning | — | This phase | — |
| P0-002 | Confirm use case hierarchy in Build.md | Planner | Planning | — | This phase | — |
| P0-003 | Populate Features & Systems table from Build.md conversation | Assistant | Planning | P0-002 | This phase | — |
| P0-004 | Pre-fill Van.md from published specs | Architect | Planning | — | This phase | — |
| P0-005 | Define all requirements | All workers | Planning | P0-002 | This phase | — |
| P0-006 | Identify regulatory requirements | Assistant | Planning | — | This phase | — |
| P0-007 | Full layout design and zone planning | Architect | Planning | P0-004 | This phase | — |
| P0-008 | Electrical system design — sizing, cable, fuse layout | Electrician | Planning | P0-004 | This phase | — |
| P0-009 | Insulation approach — material, sequence, quantities | Builder | Planning | P0-004 | This phase | — |
| P0-010 | Framing design and cut lists | Carpenter | Planning | P0-007 | This phase | — |
| P0-011 | Water system design, tank sizing, pipe routing | Plumber | Planning | P0-007 | This phase | — |
| P0-012 | Heating system design — heater choice, placement, fuel route | Mechanic | Planning | P0-004 | This phase | — |
| P0-013 | Product research and shopping list | Shopper | Planning | P0-008, P0-010 | This phase | — |
| P0-014 | Find and shortlist specific units | Owner | Planning | P0-002 | This phase | — |
| P0-015 | Purchase van | Owner | Planning | P0-014 | This phase | — |
| P0-016 | Pre-purchase inspection | Mechanic | Vehicle | P0-015 | This phase | Van in hand |
| P0-017 | Sense-check critical dimensions against published specs | Architect | Planning | P0-016 | This phase | Van in hand |
| P0-018 | Verify all unverified Van.md fields | Mechanic + Architect | Vehicle | P0-016 | This phase | Van in hand |
| P0-019 | Define Phase 1 scope | Planner | Planning | P0-017, P0-018 | This phase | Van in hand |

##### B2 — Size unknown

P0-006 (size choice) is the gate for all dimension-dependent work. Use-case and vision work proceeds immediately.

| ID | Task | Worker | Track | Depends on | Earliest start | Blocked until |
|---|---|---|---|---|---|---|
| P0-001 | Ingest existing research — manuals, forums, build guides | Assistant | Planning | — | This phase | — |
| P0-002 | Confirm use case hierarchy in Build.md | Planner | Planning | — | This phase | — |
| P0-003 | Populate Features & Systems table from Build.md conversation | Assistant | Planning | P0-002 | This phase | — |
| P0-004 | Identify regulatory requirements | Assistant | Planning | — | This phase | — |
| P0-005 | Define size requirements from use cases — size, height, wheelbase trade-offs | Architect | Planning | P0-002 | This phase | — |
| P0-006 | Choose van size (wheelbase and roof height) | Owner | Planning | P0-005 | This phase | — |
| P0-007 | Pre-fill Van.md cargo dimensions from published specs | Architect | Planning | P0-006 | This phase | Size chosen |
| P0-008 | Define all requirements | All workers | Planning | P0-006 | This phase | Size chosen |
| P0-009 | Full layout design and zone planning | Architect | Planning | P0-007 | This phase | Size chosen |
| P0-010 | Electrical system design — sizing, cable, fuse layout | Electrician | Planning | P0-007 | This phase | Size chosen |
| P0-011 | Insulation approach — material, sequence, quantities | Builder | Planning | P0-007 | This phase | Size chosen |
| P0-012 | Framing design and cut lists | Carpenter | Planning | P0-009 | This phase | Size chosen |
| P0-013 | Water system design, tank sizing, pipe routing | Plumber | Planning | P0-009 | This phase | Size chosen |
| P0-014 | Heating system design — heater choice, placement, fuel route | Mechanic | Planning | P0-007 | This phase | Size chosen |
| P0-015 | Product research and shopping list | Shopper | Planning | P0-010, P0-012 | This phase | Size chosen |
| P0-016 | Find and shortlist specific units | Owner | Planning | P0-006 | This phase | Size chosen |
| P0-017 | Purchase van | Owner | Planning | P0-016 | This phase | — |
| P0-018 | Pre-purchase inspection | Mechanic | Vehicle | P0-017 | This phase | Van in hand |
| P0-019 | Sense-check critical dimensions against published specs | Architect | Planning | P0-018 | This phase | Van in hand |
| P0-020 | Verify all unverified Van.md fields | Mechanic + Architect | Vehicle | P0-018 | This phase | Van in hand |
| P0-021 | Define Phase 1 scope | Planner | Planning | P0-019, P0-020 | This phase | Van in hand |

##### B3 — Model unknown

P0-006 (model and size choice) is the critical gate. P0-005 invokes the Architect's van selection flow — that flow needs to exist in the Architect's SKILL.md.

| ID | Task | Worker | Track | Depends on | Earliest start | Blocked until |
|---|---|---|---|---|---|---|
| P0-001 | Ingest existing research | Assistant | Planning | — | This phase | — |
| P0-002 | Confirm use case hierarchy in Build.md | Planner | Planning | — | This phase | — |
| P0-003 | Populate Features & Systems table from Build.md conversation | Assistant | Planning | P0-002 | This phase | — |
| P0-004 | Identify regulatory requirements | Assistant | Planning | — | This phase | — |
| P0-005 | Van selection — invoke Architect to define make/model/size from use cases | Architect | Planning | P0-002 | This phase | — |
| P0-006 | Choose van make, model, and size | Owner | Planning | P0-005 | This phase | — |
| P0-007 | Pre-fill Van.md from published specs | Architect | Planning | P0-006 | This phase | Model + size chosen |
| P0-008 | Find specific unit | Owner | Planning | P0-006 | This phase | Model chosen |
| P0-009 | Purchase van | Owner | Planning | P0-008 | This phase | — |
| P0-010 | Pre-purchase inspection | Mechanic | Vehicle | P0-009 | This phase | Van in hand |
| P0-011 | Sense-check all cargo area dimensions | Architect | Planning | P0-010 | This phase | Van in hand |
| P0-012 | Define Phase 1 scope | Planner | Planning | P0-011 | This phase | Van in hand |

---

After creating all files, run the IT worker: read `build-phases.md` and the just-created build files, write the initial `dashboard/data.json` with the full 14-phase backbone and all phases at `not started`. Then state in one sentence what was set up, then move immediately into Stage 4 — no confirmation prompt.

---

## Stage 4 — Vision, Components, and Close

### G. Build.md — Facilitated Conversation (All Paths)

Two stages: purpose first, then a zone-by-zone walk. Do not pre-fill Build.md and ask for approval — the conversation is the capture.

**Tone**: The owner has just confirmed setup and is now describing what they want their life to look like. This is the most human part of the conversation. Ask questions like someone who is genuinely curious about how they want to live — not like someone filling in a requirements document. Let answers land before moving to the next zone.

---

#### Stage A — Purpose confirmation

**A1 — Go one level deeper on purpose**

The owner already described the van's purpose in intake. Don't repeat that back as a summary — pick the most concrete thing they said and ask what that actually looks like in practice.

Example: if they said "long trips across Europe", ask what a typical day looks like — are they driving long stretches and arriving at camp late, or moving slowly and spending most of the day outside?

One question. Wait for the answer.

**A2 — Non-negotiables**

> "What are the things this van absolutely must have, regardless of cost or space?"

Invite a list. Wait for the response before moving on.

---

#### Stage B — Zone-by-zone walk

Walk through each area in conversation. Cover only areas plausible for this build — skip what clearly doesn't apply. Don't announce the area before asking about it; the question itself signals the topic. One follow-up only, and only if something was vague or contradictory. After each area, confirm understanding in one sentence before moving on. The goal is to leave each area with enough to make real design decisions.

**Areas and what to have understood by the end:**

**Sleeping**
Open: "How many people need to sleep comfortably, and does the bed need to be permanently ready or is making it up each night fine?"
Understand: how many people; whether the bed needs to be permanently ready or making it up is acceptable; how much floor space matters during the day; any physical constraints affecting bed height or access (e.g. tall people, bad back, travelling with a dog).

**Kitchen area**
Open: "How important is cooking properly in this van?"
Understand: whether proper meals are a priority or convenience; fuel preference if any; whether cooking happens inside, outside, or both; fridge expectations and how often they'll be near shops.

**Seating / work area**
Open: "Do you need somewhere to sit and work, or is this more about a place to eat and relax?"
Understand: whether extended sitting is needed; what working actually requires (screens, peripherals, connectivity); whether a dedicated surface is needed or doubling up with another zone is fine; how many people need to sit at once.

**Water**
Open: "How do you feel about water — big tank and self-sufficient, or topping up regularly is fine?"
Understand: attitude to tank size vs refilling hassle; whether hot water matters and what for (washing up, showering, both); whether they'll mostly be at sites with facilities or genuinely off-grid.

**Shower / wet room**
Open: "Do you want any kind of shower or toilet in the van?"
Understand: whether they want either; comfort with maintenance and emptying; whether a hidden/fold-out arrangement would be acceptable or they want a dedicated space.

**Garage**
Open: "What bulky or awkward things do you bring on trips?"
Understand: what needs to be stored (bikes, boards, tools, camping gear); whether quick access to specific items matters or everything can be packed away; whether loading from the rear is important.

---

#### Features & Systems Table

As each zone is completed, log the features and systems that emerged — don't wait until the end. Accumulate `F-{NN}` entries across the zone walk, grouped by zone/category, all with status `Planned`.

After Stage B is complete, present the accumulated list for confirmation before writing. Use natural language — not a table or bullet list. Example: "Here's what I've got: fixed bed, diesel heater, solar setup, 12V compressor fridge, roof fan, under-bed storage. Anything to add or drop?" The table format lives in Decisions.md; this is just a verbal check.

Only write after owner confirmation. This runs in all sub-states.

---

### G2. Inspiration & References (All Paths)

After the Features & Systems confirmation, ask:

> "Last thing — have you seen any vans or builds you really like? Could be a YouTube channel, an Instagram account, a specific van you spotted somewhere. Drop any links, images, or names — and tell me what specifically you like about them."

Accept anything: URLs, image uploads, names, descriptions, vague recollections. If the owner has nothing, move on without pressing.

For each reference provided, extract the design signal the owner called out — not a summary of the van, but what specifically they liked about it: a layout choice, a material, a spatial solution, a feeling. Ignore anything they didn't comment on.

---

Synthesise all of Stage A, Stage B, and any inspiration references into Build.md in one write. State: "Got it — writing your vision doc now."

Set frontmatter: `last_updated: {today}`, `last_updated_by: auto — add-van`.

---

### H. Conversion.md (All Paths)

Create `build/Conversion.md` — the master status file. Pull from all previously created components:
- Current phase:
  - Path A: "Phase 0 — Setup"
  - B1: "Phase 0 — Pre-Purchase"
  - B2: "Phase 0 — Size Selection"
  - B3: "Phase 0 — Van Selection"
- Timeline: hard deadline if stated, otherwise `-tbd-`
- Budget: capture structure, not just a number:
  - Total budget
  - Van purchase included? (Y / N / unknown)
  - Labour allowance (if mentioned)
  - Contingency (if mentioned)
  - All unknown fields: `-tbd-`
- Open decisions count: 0 (unless Features & Systems entries were just confirmed — count those)
- Current tasks: pulled from Scope.md Phase 0 — reflects actual starting state, not boilerplate

---

### I. First Session Log (All Paths)

Create `logs/sessions/session-{today}.md`. Record:
- Build initiated
- Sub-state (Path A / B1 / B2 / B3), and whether a specific unit was identified under B1
- Van details captured (or: size not yet chosen / model not yet chosen)
- Foundational components created
- Features & Systems confirmed (list the F-{NN} entries)
- What's still needed (first action items) — build tasks only; do not include usage instructions

---

### J. Completion Summary

#### Path A — Van Owned

| Component | Status |
|----------|--------|
| `build/Conversion.md` | Created — Phase 0 active |
| `build/Van.md` | Created — {N} fields populated, {M} dimensions still need measuring |
| `build/Build.md` | Created — use case hierarchy confirmed |
| `build/Decisions.md` | Active — {N} features and systems logged |
| `build/Requirements.md` | Skeleton ready |
| `build/Scope.md` | Skeleton ready — Phase 0 tasks listed |
| `build/Weight.md` | Skeleton ready — kerb weight {populated or -tbd-} |
| `build/ShoppingList.md` | Skeleton ready — empty |
| `build/Knowledge.md` | Created — {N} terms pre-populated |
| `build/Lessons.md` | Created — empty |
| `logs/sessions/session-{date}.md` | Created — this session logged |
| `documents/index.md` | Created — empty |
| `conversations/index.md` | Created — empty |
| `dashboard/data.json` | Created — 14-phase arc loaded |

**What's next:**

Van.md is pre-filled from published specs for your make/model/size — layout planning can start now. Physical measurement is only needed before irreversible cuts (floor, framing, roof apertures), not before design.

**Want to start with the layout?** I'll bring in the Architect.

If you have any technical resources to ingest first (manuals, wiring diagrams, build specifications), run `/new-doc` before the layout session — knowledge before design.

---

#### B1 — Size known (pre-purchase)

| Component | Status |
|----------|--------|
| `build/Conversion.md` | Created — Phase 0 (Pre-Purchase) active |
| `build/Van.md` | Created — published specs loaded, all marked unverified |
| `build/Build.md` | Created — use case hierarchy confirmed |
| `build/Decisions.md` | Active — {N} features and systems logged |
| `build/Requirements.md` | Active — ready for requirements |
| `build/Scope.md` | Created — Phase 0 tasks listed |
| `build/Weight.md` | Created — kerb weight from published specs, marked unverified |
| `build/ShoppingList.md` | Active — empty |
| `build/Knowledge.md` | Created — {N} terms pre-populated |
| `build/Lessons.md` | Created — empty |
| `logs/sessions/session-{date}.md` | Created — this session logged |
| `documents/index.md` | Created — empty |
| `conversations/index.md` | Created — empty |
| `dashboard/data.json` | Created — 14-phase arc loaded |

If no specific unit identified:

> "Your build is set up in pre-purchase mode. Published specs are loaded for [make/model/size] — all marked unverified until you have the van in front of you. You can design the entire build now.
>
> **Want to start with the layout?** I'll bring in the Architect now."

If a specific unit was identified:

> "Your build is set up in pre-purchase mode. You've got a specific unit in mind — before designing anything, that van needs an inspection.
>
> **Want to run through the pre-purchase inspection now?** I'll bring in the Mechanic."

---

#### B2 — Size unknown

| Component | Status |
|----------|--------|
| `build/Conversion.md` | Created — Phase 0 (Size Selection) active |
| `build/Van.md` | Created — make/model populated, cargo dimensions -tbd- |
| `build/Build.md` | Created — use case hierarchy confirmed |
| `build/Decisions.md` | Active — {N} features and systems logged |
| `build/Requirements.md` | Active — use-case requirements only; dimension-dependent requirements held |
| `build/Scope.md` | Created — Phase 0 tasks listed |
| `build/Weight.md` | Partial — model-level payload range only, dimensions -tbd- |
| `build/ShoppingList.md` | Active — dimension-independent items only |
| `build/Knowledge.md` | Created — {N} terms pre-populated |
| `build/Lessons.md` | Created — empty |
| `logs/sessions/session-{date}.md` | Created — this session logged |
| `documents/index.md` | Created — empty |
| `conversations/index.md` | Created — empty |
| `dashboard/data.json` | Created — 14-phase arc loaded |

> "Your build is set up in size-selection mode. Your vision and use cases are captured — now we need to turn that into a specific wheelbase and roof height before any design work can start.
>
> **Want to do that now?** I'll bring in the Architect to work through which size fits your use cases."

---

#### B3 — Model unknown

| Component | Status |
|----------|--------|
| `build/Conversion.md` | Created — Phase 0 (Van Selection) active |
| `build/Van.md` | Created — headers only, all fields -tbd- |
| `build/Build.md` | Created — use case hierarchy confirmed |
| `build/Decisions.md` | Active — {N} features and systems logged (vision and use-case decisions only) |
| `build/Requirements.md` | Active — use-case requirements only |
| `build/Scope.md` | Created — Phase 0 tasks listed |
| `build/Weight.md` | Skeleton only — model not chosen |
| `build/ShoppingList.md` | Skeleton only — model not chosen |
| `build/Knowledge.md` | Created — {N} terms pre-populated |
| `build/Lessons.md` | Created — empty |
| `logs/sessions/session-{date}.md` | Created — this session logged |
| `documents/index.md` | Created — empty |
| `conversations/index.md` | Created — empty |
| `dashboard/data.json` | Created — 14-phase arc loaded |

> "Your build is set up in van-selection mode. Build.md captures your vision — that's the filter for choosing a van. Detailed design is on hold until we have a model and size.
>
> **Want to work through van selection now?** I'll bring in the Architect — they'll take your use cases and tell you what make, model, and size actually fits."

---

## K. Acquisition Trigger

There is no `/add-van` re-run on acquisition. All transitions are handled in-conversation without re-running any command.

### B3 → B2 (model chosen, size not yet decided)

Detected when owner confirms a make/model in conversation but has not yet decided the size. Update CLAUDE.md `{van-make-model-year}` field. Note: size-dependent work remains blocked.

### B3 → B1 or B2 → B1 (size confirmed)

Detected when owner confirms make/model/wheelbase/roof in conversation. Invoke Architect to pre-fill Van.md cargo dimension fields from published specs, converting `-tbd-` dimension fields to `~{value} (unverified)`. Update Scope.md to reflect the B1 task list. Phase name in Conversion.md changes to "Phase 0 — Pre-Purchase". No file conflicts, no overwrite risk.

### B1 → owned (van purchased)

Detected when owner confirms purchase, or when the purchase task is marked complete. Trigger this sequence without re-running `/add-van`:

1. **Mechanic** — runs pre-purchase inspection (A1 checklist). Flags any blockers. Build does not proceed past inspection failures.
2. **Architect** — sense-checks critical dimensions against published specs. Notes any deviations in Van.md. Updates `~{value}` entries where the physical van differs from spec.
3. **Mechanic + Architect** — all remaining `~{value} (unverified)` fields reviewed. Each confirmed, corrected, or flagged for follow-up.
4. **Planner** — runs Phase 0 quality gate. Checks all unverified fields referenced by any design decision or cut list are resolved.
5. **Planner** — proposes Phase 1 scope. Most design work is already done — Phase 1 is execution, not planning.

---

## Rules

- **One checkpoint.** Intake → Checkpoint 1 (owner confirms before any files are written) → file creation → Stage 4 (Build.md conversation, no prompt). The only other hard stops are irreversible actions.
- **Intake is sequential: one question at a time.** Q1–Q7, in order, each waiting for an answer. Skip any question whose answer is already clear. Never combine questions.
- **Sub-state is silent.** Never use Path A, B1, B2, B3 labels with the owner. These resolve from intake answers and shape what gets created — they do not surface in conversation.
- **Sub-state detection is mandatory.** Never create Path B components without a confirmed sub-state (B1, B2, or B3). If sub-state is unclear after Q1–Q2, resolve with Q2 branch before proceeding.
- **Checkpoint 1 is a single confirmation, not a review.** No summary table. Corrections to intake data can be made next session.
- **Full component set in B1.** Never defer Requirements.md, Weight.md, ShoppingList.md, or Knowledge.md in B1.
- **Published specs are `~{value}`, not `-tbd-`.** If a value can be estimated from manufacturer data for the confirmed size, mark it unverified. Reserve `-tbd-` for fields that genuinely cannot be estimated.
- **B2 cannot pre-fill cargo dimensions.** Size (wheelbase + roof height) must be confirmed before any cargo dimension can be estimated. Do not fill dimension fields with guesses from a non-specific model.
- **Dimensions come from published specs.** Pre-fill from `references/van-sizes.md` for the confirmed make/model/size, marked `~{value} (source: published specs — verify before irreversible cuts)`. Owner-provided specs or corrections follow the same pattern. `-tbd-` is for fields that cannot be estimated at all.
- **Build.md is a conversation, not a confirmation.** Run Stage A (purpose) then Stage B (zone-by-zone walk). Do not show a pre-filled draft.
- **Features & Systems table is populated at Build.md facilitation.** Always, in all sub-states. Not deferred to post-purchase.
- **Layout decisions made pre-purchase are flagged.** Any Decisions.md layout entry created before dimensions are verified must carry the note `~layout (pending dimension verification — revisit after purchase)`.
- **No irreversible action until post-inspection.** In B1 with a specific unit identified, no irreversible action may be confirmed until the Mechanic pre-purchase inspection is complete and clear.
- **No `/add-van` re-run on acquisition.** Use the acquisition trigger sequence in section K. Re-running `/add-van` on an existing build risks overwriting confirmed decisions.
- **B3 van selection requires an Architect flow.** The Architect's SKILL.md must contain a van selection procedure before P0-005 can be run. If it doesn't exist yet, surface this as a gap.
- **Scope.md reflects actual starting state.** Assess what the owner has already done before writing tasks. Mark completed tasks as complete.
- **Autonomous between checkpoints** — no interaction during file creation except for existing file conflicts (ask: overwrite, skip, or merge) and the Features & Systems confirmation before writing Decisions.md.
- **Phase order matters.** For all paths: Van.md → skeleton components → Build.md facilitation → Conversion.md → session log.
- **Verify templates before creating files.** Before creating any component file, confirm the template exists at the path listed in `.claude/index.md`. If a template is missing, stop and notify the owner — do not proceed with that component.
