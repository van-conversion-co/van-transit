---
description: Session startup — load context, brief owner, identify focus
---

# start — Skill Logic

> Load build context and brief the owner. Triggered by `/start` or opening greetings. Run at the start of every session before any other work.

---

## When This Skill Runs

- Owner invokes `/start` explicitly
- Owner opens with a greeting: "hello", "let's do it", "let's start", "let's go", "good morning", "hi", "ready"

---

## Steps

### 0. GATE

Check whether `build/Conversion.md` exists. If not: say "Doesn't look like there's a build set up yet — run `/add-van` to get started." and stop.

Do not announce the check.

### 1. LOAD

Read `build/Conversion.md`. Extract:
- Current phase
- Last session date
- Budget status
- Open decisions count

### 2. HISTORY

Read the most recent file in `logs/sessions/`. Extract:
- All unchecked `[ ]` action items
- All items labelled `[carry-forward]`

### 3. DECISIONS

Read `build/Decisions.md`. Flag:
- Any `Open` entry older than 14 days
- Any `Confirmed` entry with a `blocks_worker` field that has not been acknowledged this session

### 4. FLAGS

Check for time-sensitive items:
- Orders in `conversations/` with expected delivery dates approaching
- Quotes with expiry dates approaching
- Any field in `Van.md` still marked `~value (unverified)` that is referenced by a current-phase task in `Scope.md`

### 5. BRIEF

Present in two clearly separated beats. No decision or question appears in Beat 1 — the owner reads it passively. Beat 2 is where they engage.

**Beat 1 — Status**:
- Current phase and task completion — e.g. "Phase 2 — 4 of 9 tasks complete."
- Last session date
- Budget status (if tracked)
- Time-sensitive flags (expiring quotes, approaching deliveries, unverified dimensions blocking current phase)
- Stale open decisions (Open entries older than 14 days)
- Any `blocks_worker` entries relevant to today's likely domain

**Beat 2 — Focus**:
- Carry-forward action items from previous sessions, oldest first
- One directive offer based on the current phase and sub-state:

  **Phase 0 — Setup** (Path A, van owned): If Van.md has unverified dimensions, offer: "Your dimensions still need measuring before layout can start — want to work through Van.md now?" If dimensions are verified, offer: "Want to start with the layout? I'll bring in the Architect."

  **Phase 0 — Pre-Purchase** (B1, no specific unit): "There's full design work available now. Want to start with the layout? I'll bring in the Architect."

  **Phase 0 — Pre-Purchase** (B1, specific unit identified): "The pre-purchase inspection is the next gate. Want to run through that now? I'll bring in the Mechanic."

  **Phase 0 — Size Selection** (B2): "The next step is choosing a wheelbase and roof height. Want to do that now? I'll bring in the Architect."

  **Phase 0 — Van Selection** (B3): "The next step is choosing a van. Want to work through that now? I'll bring in the Architect."

  **Any other phase**: "The next unblocked task in Scope.md is [X] — want to start there?"

  After delivering the directive, scan all tasks in active and upcoming phases for status Ready in tracks other than the one covered by the directive. If any exist, append one line: "Also ready: [up to three task names]." Omit if nothing else is Ready.

---

## Rules

- Load context silently. No "loading", "reading", "checking" — just present the briefing.
- The briefing should feel like a colleague catching you up, not a system report.
- If `{build-name}` is still a placeholder in `CLAUDE.md`: ask for the build name before the briefing and update `CLAUDE.md` immediately.
- The briefing should fit in one screen. If carry-forward items exceed five, summarise: "5 carry-forward items — showing oldest 3. Type `all items` to see the full list."
