---
description: Ingest a document — summarise, index, route extracted knowledge to build components
---
> Ingest any document into the build knowledge base. Accepts files, pasted text, or quoted content. Produces a structured summary, routes extracted knowledge to the right build components, and indexes the document for future reference.
---

## When This Skill Runs

Invoked directly via `/new-doc` with a document attached, pasted, or referenced.

---

## A. Accept Input

Accept any of the following:
- Uploaded file (PDF, DOCX, TXT, image of a spec sheet or label)
- Pasted text content
- Quoted forum post or video transcript
- Photograph of a product label, wiring diagram, or installation guide page

Auto-detect type: manual, spec sheet, quote, forum thread, video transcript, regulatory document, installation guide, product datasheet.

If the type is unclear, ask one question before proceeding.

---

## B. Summarise

Produce a structured document summary:

```markdown
---
date: {YYYY-MM-DD}
type: {manual / spec-sheet / quote / forum / transcript / regulatory / guide / datasheet / other}
source: {supplier / manufacturer / forum / owner / other}
original: {filename, URL, or description}
---

# {Document Title}

## Summary
{3-5 sentences: what this document is, what it says that matters for the build}

## Key Specifications
{Any specific numbers, ratings, dimensions, or performance figures}

## Installation / Usage Notes
{Anything that affects how a component is fitted or used}

## Warnings & Requirements
{Safety notices, regulatory requirements, compatibility constraints}

## Routing Log
{Written after owner confirms routing}
```

Write to `documents/{YYYY-MM-DD}-{slug}.md`.

---

## C. Extract & Route

After summarising, identify routing candidates grouped by target component:

**Decisions.md candidates** — any specification that constitutes a design decision or constraint:
- Component ratings (battery Ah, solar watts, cable mm², fuse rating)
- Compatibility requirements ("requires B2B charger with variable voltage alternators")
- Hard limits ("maximum 4 appliances on this circuit")

**Requirements candidates** — testable statements implied by the document:
- "Must not exceed X current draw"
- "Installation requires X clearance from combustibles"

**Knowledge candidates** — any term, technique, or product worth recording:
- Product names and their function
- Technical terms with definitions
- Techniques described in a guide

**Scope candidates** — any task implied by the document:
- "Before installation, clean surface with isopropyl alcohol" → task for Builder
- "Commission with a current clamp meter" → commissioning task for Electrician

Route extracted items as follows:

- **Decisions.md candidates** — surface each proposed entry for owner confirmation before writing. Never auto-write.
- **Knowledge, Requirements, and Scope candidates** — write immediately; note in the response what was routed.

---

## D. After Confirmation

1. Write approved items to target components.
2. Complete the Routing Log section in the document summary.
3. Add entry to `documents/index.md`:

```
| {YYYY-MM-DD} | {Title} | {Type} | {2-sentence summary} | {file path} |
```

4. Append audit entry to current session log.

---

## Rules

- **Routing review before any write.** Nothing reaches Decisions.md or Requirements without owner seeing it first.
- **Slugs must be descriptive.** `2024-03-15-victron-mppt-100-30-manual.md` not `2024-03-15-document.md`.
- **Specifications are Decisions.md candidates, not Knowledge.** A battery's Ah rating is a decision, not just a fact.
- **Safety warnings always surface.** Any installation warning or regulatory requirement is flagged in the summary and proposed as a Requirement or Decisions.md constraint.
- **Images are processed visually.** Wiring diagrams, label photos, spec plates — describe what's in them and extract any readable values.
