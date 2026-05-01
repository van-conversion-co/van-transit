---
description: Log a conversation and route what was learned to build components
---

# new-conversation — Skill Logic

> Log any conversation — tradesperson, supplier, forum interaction, or video debrief — and route what was learned to the right build components. Accepts voice transcripts, typed notes, or bullet points.

---

## When This Skill Runs

Invoked directly via `/new-conversation` after any external interaction worth capturing.

---

## A. Accept Input

Accept any of the following:
- Voice transcript (pasted or typed)
- Bullet-point notes from memory
- Stream-of-consciousness debrief
- Copy-pasted forum exchange
- Notes from a YouTube video or podcast

Ask one clarifying question if needed: who was this with, and what was the main topic?

---

## B. Determine Metadata

| Field | How to determine |
|-------|-----------------|
| Date | Ask if not in input; default to today |
| Who with | Person name, company, or forum/channel name |
| Medium | Phone call, in-person, forum, video, email |
| Topic | Infer from content |
| Slug | `{YYYY-MM-DD}-{who}-{topic}.md` |

Slug examples:
- `2024-03-15-mike-electrician-quote.md`
- `2024-03-20-sprinter-forum-insulation.md`
- `2024-03-22-faroutride-solar-wiring.md`

---

## C. Structure the Log

```markdown
---
date: {YYYY-MM-DD}
with: {person / company / forum / channel}
medium: {call / in-person / forum / video / email}
topic: {brief topic label}
---

# Conversation — {who}, {date}

## Summary
{3-5 sentences: what the conversation was about and what matters from it}

## Key Findings
{Numbered list of concrete things learned — facts, prices, lead times, recommendations}

## Quotes
{Any exact words worth preserving — attributed}

## Action Items
- [ ] {task arising from this conversation}

## Open Questions
{Things that came up but weren't resolved}

## Routing Log
{Written after owner confirms routing}
```

Write to `conversations/{YYYY-MM-DD}-{slug}.md`.

---

## D. Extract & Route

After structuring the log, identify routing candidates:

**Decisions.md candidates** — any decision or constraint that emerged:
- "Electrician said the alternator on this year of Transit is smart — VSR won't work"
- "Supplier confirmed 200Ah battery fits within the wheel arch with 10mm clearance"

**Scope candidates** — any task or dependency identified:
- "Need to get a weighbridge ticket before ordering the battery bank"
- "Supplier lead time is 3 weeks — order before starting Phase 2"

**Administrator candidates** — contact details, pricing, lead times:
- Supplier name, what they sell, price quoted, validity, contact

**Knowledge candidates** — any term or technique explained:
- Technical terms the tradesperson used that should be recorded

**Shopper candidates** — any quoted price worth capturing in the Shopping List:
- Item, spec, price, supplier, date

Route extracted items as follows:

- **Decisions.md candidates** — surface each proposed entry for owner confirmation before writing. Never auto-write.
- **Knowledge, Scope, and Administrator candidates** — write immediately; note in the response what was routed.
- **Shopper candidates** — present for owner confirmation per ShoppingList.md rules.

---

## E. After Confirmation

1. Write approved items to target components.
2. Complete the Routing Log in the conversation file.
3. Append action items to the current session log.
4. Append audit entry to the current session log.

---

## Rules

- **Routing review before any write.** Nothing reaches Decisions.md without owner seeing it first.
- **Quotes from tradespeople are high-value Decisions.md candidates.** A qualified person saying "you need a B2B charger on this van" is a constraint worth logging.
- **Prices are time-stamped.** Always record the date with any price — quotes expire.
- **Action items go to the session log immediately.** Don't leave them only in the conversation file.
- **Slugs must identify who and what.** Future-you needs to find this without reading it.
