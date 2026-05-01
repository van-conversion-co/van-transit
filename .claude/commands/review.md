---
description: Between-sessions briefing — phase status, open items, time-sensitive flags
---

# review — Skill Logic

> Between-sessions briefing. Lighter than session close — no lessons capture, no staleness check, no audit. Just: where are we, what's next, what's time-sensitive. Run when the owner wants a quick catch-up after a gap.

---

## When This Skill Runs

- Owner invokes `/review` explicitly
- Session startup detects a gap of >3 days since last session log (auto-suggest)
- Owner asks "where were we?" or "what's the status?"

---

## A. Load Context

1. Read `build/Conversion.md` — current phase and status.
2. Read the most recent session log in `logs/sessions/`.
3. Read `build/Decisions.md` — any Open entries, especially those older than 14 days.
4. Read `build/Scope.md` — current phase tasks and completion status.
5. Check `documents/index.md` and `conversations/` — anything ingested since the last session that hasn't been acted on?

---

## B. Briefing

Present a structured briefing:

### Phase status
- Current phase name and goal
- Tasks: how many complete, how many in progress, how many not started
- Estimated phase completion (if determinable)

### Open decisions
- Any Decisions.md entries with status Open — listed with age and which phase they block

### Action items
- Carried-forward items from the last session log
- Any new action items that emerged from conversations or documents ingested since

### Time-sensitive flags
- Orders placed with expected delivery dates approaching
- Quotes approaching expiry
- Any weather-dependent tasks (if seasonal context is in the build)
- Any bookings or appointments noted in conversations

### What's next
- The single most important thing to do next session, based on Scope.md task sequence and any blockers

---

## C. Weekly Review Format

When the owner explicitly invokes `/review` for a weekly summary (or when it's been >7 days):

Write a weekly review to `logs/weekly/week-{YYYY-WNN}.md` using `.claude/templates/WeeklyReview.md`.

Owner confirms before writing.

---

## Rules

- **Briefing first, then ask.** Don't ask the owner what they want to know — give them the full picture and let them drill in.
- **Time-sensitive items lead.** If an order is arriving tomorrow or a quote expires this week, that's the first thing.
- **No lessons, no staleness check.** That's session close. Review is lean.
- **One clear "what's next".** The owner should leave a review knowing exactly what to do when they pick up the build again.
