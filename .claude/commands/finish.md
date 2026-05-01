---
description: Session close — summary, audit, decisions, lessons, staleness
---

# finish — Skill Logic

> Session close workflow. Triggered by `/finish` or end-of-session signals. Reviews what happened, audits unrouted items, captures lessons, checks phase status, then writes the session log on owner confirmation.

---

## When This Skill Runs

- Owner invokes `/finish` explicitly
- Owner signals end of session: "I'm done", "let's wrap up", "that's it for today", "done for now", "end session"

---

## Steps

### 0. GATE

Check whether `build/Conversion.md` exists. If it does not: output "No build found. Run `/add-van` to get started." and stop — do not run any further steps.

### 1. AUDIT

Scan the conversation for unrouted items:

- Decisions made but not in Decisions.md
- Measurements taken but not in Van.md
- Parts ordered or received but not in Conversion.md
- Terms used that should go in Knowledge.md
- Irreversible actions taken this session without the owner typing "confirm" before execution — flag as a protocol gap and propose a retroactive Decisions.md entry with `irreversible: true`

Also check `documents/index.md` and `conversations/index.md` for entries added since the last session whose extracted knowledge has not yet been routed to any build component. Surface any un-actioned entries.

Also run the staleness conditions defined in each component's `Stale when` field in `.claude/index.md` — surface failures here, not as a separate step.

Present a routing review for each unrouted item. Owner confirms, skips, or defers each individually.

### 2. ACTION ITEMS

Combine: audit findings that require follow-up + unchecked items from previous session log (mark these `[carry-forward]`) + any new items raised this session.

Present the combined list:

> "These are your open items going into next session: [list]. Anything to add or remove?"

### 3. SUMMARY

Draft a 3–6 sentence session narrative. Focus:
- What was the session about
- What was resolved
- What is still open
- What context matters next time

Present to the owner before writing. Do not write until confirmed.

### 4. LESSONS

Review the session for one genuinely useful generalizable insight. Apply the filter: "Would this help someone doing the same build who hadn't made this mistake?"

If yes: draft the lesson in the format below and present it to the owner with:

> "I'd like to log this as a lesson — does this belong in Lessons.md? Confirm, skip, or adjust."

Do not write to `build/Lessons.md` until the owner confirms. On skip: do not write. Most sessions: zero or one lesson.

Lesson format:
```
### LES-{NNN}

| Field | Value |
|-------|-------|
| ID | LES-{NNN} |
| Date | {YYYY-MM-DD} |
| Category | {Electrical / Insulation / Plumbing / Planning / Carpentry / Vehicle / Sourcing / General} |
| Phase | {phase slug} |

**Lesson**
{Generalised insight — 1-3 sentences, useful without knowing this specific build}

**Context**
{What specifically happened in this build — the concrete situation that produced the lesson}
```

### 5. PHASE CHECK

If any task was completed or irreversible action taken this session: check whether the current phase is now complete.

If yes: "All Phase [N] tasks are complete. Want me to run the quality gate?" Do not advance without owner decision.

### 6. WRITE

On owner confirmation of the summary:

1. Write `logs/sessions/session-{YYYY-MM-DD}.md` using the template below.
2. Update `build/Conversion.md` — last session date, one-line summary.
3. Set `status: closed` in the session log frontmatter.
4. Run IT worker: read build state, write `dashboard/data.json`, append `[AUTO] dashboard/data.json updated` to the session log audit section.
5. Run: `git add -A && git commit -m "Session {YYYY-MM-DD}: {one-line summary from Step 3}" && git push`

---

## Session Log Template

```markdown
---
date: {YYYY-MM-DD}
status: open
phase: {current-phase-slug}
last_updated: {YYYY-MM-DD}
---

# Session — {YYYY-MM-DD}

## Summary

{3-6 sentence narrative — focus, decisions, open questions, context for next time}

## Action Items

- [ ] {item} — {owner} — from {source}

## Audit Log

{[AUTO] or [MANUAL] entries — one line each}

## Lessons

{LES-NNN references if any captured this session, or "None this session"}
```

---

## Rules

- Steps 1–5 are review and confirmation only. Step 6 is the only write step.
- If the session was short (under ~10 exchanges) with no decisions made: "This was a short session — I'll log a brief note. Anything specific to capture?"
- Never write the session log without owner seeing the summary first.
- Carry-forward is explicit — never silently drop action items.
- Lessons are selective — one genuinely useful lesson beats five marginal ones.
- Phase completion is owner's call — the skill flags it, the owner decides whether to advance.
