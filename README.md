# Van Build Assistant

An AI co-pilot for campervan conversions. It gives you a structured way to manage a complex physical build — from first decisions through commissioning.

The assistant helps you plan work, route information to the right documents, track decisions, capture knowledge, and surface problems before they become expensive mistakes.

---

## What it does

The assistant is organised around three things:

**Build documents** — living files that define the van: what it is, what it needs to do, every decision made, every dimension measured. These live in `build/`.

**Domain workers** — specialists invoked by area: Architect for layout and dimensions, Electrician for the power system, Plumber for water, Carpenter for furniture, and so on. Each worker knows its domain deeply and hands off to others correctly.

**Logs** — session notes, weekly reviews, conversation logs, and ingested documents. Everything that happened and everything learned. These live in `logs/`, `conversations/`, and `documents/`.

---

## Getting started

**Requirements**: Claude Code (claude.ai/code), this repo cloned locally.

```
git clone <repo-url>
cd <repo-name>
```

Open the repo in Claude Code. Then:

```
/add-van
```

This runs once. It asks you about the van, your vision, and your ownership status — then creates all the foundational build documents. If you don't own the van yet, it branches into a pre-purchase mode and you can still plan the full build.

After `/add-van`, the assistant tells you exactly what to do next based on where you are.

---

## Commands

| Command | What it does |
|---------|-------------|
| `/add-van` | Start a new build. Run once. |
| `/start` | Begin a session — briefing on phase status, open decisions, carry-forward items |
| `/finish` | Close a session — summary, audit, lessons, action items for next time |
| `/new-doc` | Ingest a document: manual, spec sheet, quote, forum thread, installation guide |
| `/new-conversation` | Log a conversation: tradesperson, supplier, forum, video debrief |
| `/review` | Write a weekly review log |
| `/it` | Refresh the dashboard — regenerates `dashboard/data.json` from current build state |

Workers are invoked by name: `/architect`, `/electrician`, `/plumber`, `/carpenter`, `/mechanic`, `/planner`, `/shopper`, `/administrator`, `/assistant`.

---

## Recommended order

1. Run `/add-van`
2. Service the van before any conversion work begins
3. Ingest any existing research — `/new-doc` or `/new-conversation`
4. Measure the van — fill every dimension in `Van.md`
5. Run `/architect` to review what the space can and cannot support
6. Run `/planner` to generate the full phase structure for your build, then detail Phase 1 tasks
7. Work sessions by domain, close each with `/finish`

The order matters. Dimensions constrain layout. Layout constrains everything else. Skipping steps means rework.

---

## How decisions are tracked

Every design choice, assumption, constraint, and irreversible action is logged in `build/Decisions.md`. Nothing is written there without you seeing it first.

Irreversible actions — cutting the floor, drilling the roof, tapping the fuel tank — require an explicit confirmation before proceeding. The assistant stops, states what cannot be undone, and waits.

---

## Repository structure

```
build/          Core build documents — Van, Decisions, Scope, Requirements, etc.
logs/           Session logs and weekly reviews
conversations/  Logged interactions with tradespeople, suppliers, forums
documents/      Ingested manuals, spec sheets, quotes
dashboard/      Dashboard data file — data.json regenerated at every session close
.claude/        Assistant configuration — workers, processes, templates
```
