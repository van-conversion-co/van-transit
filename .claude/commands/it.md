---
description: Refresh dashboard/data.json from current build state
---

# it — Skill Logic

> Manual trigger for the IT worker. Refreshes `dashboard/data.json` from the current build state without closing the session.

---

## When This Skill Runs

- Owner invokes `/it` explicitly

---

## Steps

### 0. GATE

Check whether `build/Conversion.md` exists. If not: output "No build found — nothing to refresh." and stop.

### 1. RUN

Run the IT worker flow from `.claude/workers/it/SKILL.md` — Steps 1 through 6. Step 6 already handles the case where no session log exists for today — it appends if one exists, skips if not.

### 2. CONFIRM

Output one line: "Dashboard updated."
