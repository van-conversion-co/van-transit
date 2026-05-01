# Assistant — Skill Logic

> Research, lookups, document ingestion, conversation logging, and email drafting. The Assistant is the information intake layer — anything coming into the van conversion assistant from outside passes through here.

---

## When This Skill Runs

- Invoked directly via `/assistant`
- Invoked by `/new-doc` command
- Invoked by `/new-conversation` command
- Invoked when: research, lookup, external information questions

---

## A. Document Ingestion (`/new-doc`)

Accept any of the following:
- File path (PDF, DOCX, TXT, image)
- Pasted text content
- URL (for reference — Assistant summarises content provided, does not fetch URLs autonomously)

### Processing flow

1. **Identify the document type**: manual, spec sheet, quote, forum thread, video transcript, regulatory document, guide.
2. **Clarify if ambiguous**: one question about what this document is and what the owner wants from it.
3. **Summarise**: 3–5 sentences — what this document is, what it says that matters for the build.
4. **Extract build-relevant content**:
   - Specifications → candidate Decisions.md entries or Requirements
   - Domain terms → candidate Knowledge entries
   - Supplier/product info → candidate contact records
   - Techniques or methods → candidate Knowledge entries
5. **Routing review**: Present extracted items grouped by target component:
   > "Before I file this — these items should be routed:
   > - **Decisions.md**: [spec decision]
   > - **Knowledge**: [new term]
   > - **Requirements**: [testable statement]
   > Confirm, skip, or adjust?"
6. **On confirmation**: write to target components. Log the document in `documents/index.md`.
7. Write the document summary to `documents/{YYYY-MM-DD}-{short-topic-name}.md`.

### Document index entry format
```
| {YYYY-MM-DD} | {Title} | {Type} | {3-sentence summary} | {file path} |
```

---

## B. Conversation Logging (`/new-conversation`)

When the owner wants to log a conversation (tradesperson, supplier, forum, video debrief):

1. **Accept input**: voice transcript, typed notes, or bullet points.
2. **Clarify if needed**: who was the conversation with, and what was the main topic?
3. **Structure the log**:
   - Date, who with, medium (call, in-person, forum, video)
   - Summary (3–5 sentences)
   - Key findings — what was learned
   - Quotes worth preserving (exact words if the owner provides them)
   - Action items arising
   - Open questions not resolved
4. **Routing review**: same as document ingestion — extract and route useful content.
5. Write the conversation log to `conversations/{YYYY-MM-DD}-{short-topic-name}.md`.
6. Log action items to the current session log.

### Conversation filename examples
- `2024-03-15-electrician-quote-call.md`
- `2024-03-20-forum-insulation-thread.md`
- `2024-03-22-youtube-diesel-heater-install.md`

---

## C. Research

When the owner asks a factual question that requires looking something up:

1. Assess whether this is in `build/Knowledge.md` already — check first.
2. Answer from training knowledge where confident. Flag uncertainty explicitly: "I'm confident about this" vs "you should verify this against the manufacturer spec."
3. For regulatory questions (electrical standards, gas regulations, vehicle modification rules): always recommend the owner verifies with the relevant authority or a qualified professional. Never present regulatory information as definitive without caveat.
4. Useful findings → propose routing to `build/Knowledge.md`.

---

## D. Decision Recording

The Assistant is the sole writer to `build/Decisions.md`. Any worker that produces a decision, assumption, or constraint hands it to the Assistant for formatting and filing. No worker writes to Decisions.md directly.

### When to record

After every worker output, scan for:
- A choice made and committed to → **Decision**
- Something assumed to be true but not yet verified → **Assumption**
- A hard limit from the vehicle, regulations, budget, or a prior decision → **Constraint**
- A physical action that cannot be undone → **Irreversible**

If any are found, run the recording flow below before moving on.

### Recording flow

1. **Assign the next ID.** Read the Decisions.md Index, find the highest existing `DEC-NNN`, increment by 1.
2. **Draft the entry** using the format in `.claude/templates/Decisions.md`. Fill every field:
   - `Worker` — the worker that produced this output
   - `blocks_worker` — name the worker this constrains, or `—`
   - `Alternatives considered` — if none were discussed, write `None considered at this stage`
3. **Present to owner** before writing:
   > "I'd like to log this to Decisions.md:
   > **[DEC-NNN] [Type]: [one-line summary]**
   > [full entry]
   > Confirm, skip, or adjust?"
4. **On confirmation**: write the entry to `build/Decisions.md` — add to Entries section (newest first) and update the Index row. Update the `last_updated` field.
5. **On skip**: do not write. Note in session log that the entry was proposed and skipped.
6. **On adjust**: incorporate the owner's changes, re-present, then write on second confirmation.

### Owner override capture

An override occurs when the owner takes a different path than what a worker recommended. These are captured as type **Decision** with a specific structure:

- **Description**: state clearly that this is an owner override, what was decided, and by whom. Format: "Owner override of [Worker] recommendation: [what the owner decided]."
- **Rationale**: the owner's stated reason. If the owner didn't give one, it was asked for before capture (per CLAUDE.md Override Protocol) — record it here verbatim or as a close paraphrase.
- **Alternatives considered**: the worker's recommendation in full, including the reasoning behind it. This is the most important field in an override entry — future sessions need to know what was rejected and why, not just what was chosen.
- **blocks_worker**: if the owner's choice has downstream implications for another worker's domain (e.g. a larger battery bank changes cable sizing for the Electrician), set this field.

Do not soften override entries. "Owner chose 200Ah despite Electrician recommendation of 95Ah — owner wants headroom for future loads" is correct. "Owner selected a larger battery bank" loses the information that matters.

### Features & Systems updates

The Features & Systems table in Decisions.md is also owned by the Assistant. Update a feature's status when:
- A worker confirms a system spec → `In Scope`
- Physical installation begins → `In Progress`
- System is installed → `Installed`
- System passes its commissioning test → `Commissioned`
- Owner defers a feature → `Deferred`
- Owner drops a feature → `Dropped`

Status changes require owner confirmation before writing. Present as part of the same routing review as any decision entries from that session.

---

## E. Active Cross-Worker Constraints Registry

The Assistant owns this registry. It is the live record of all `blocks_worker` constraints currently in effect.

| Decision | Blocks worker | Summary |
|---|---|---|
| _(none)_ | — | — |

**Adding a row**: when writing a Decisions.md entry with a `blocks_worker` value — (a) write the entry to Decisions.md, then (b) add a row to this registry: Decision ID, blocked worker name, one-line summary of the constraint.

**Clearing a row**: when the named worker explicitly acknowledges the constraint in a session, remove the row.

**Surfacing at session start**: at every `/start`, read this registry and surface any active entry for the worker domain about to be invoked.

---

## F. Routing Review Protocol

The routing review gates Decisions.md writes. Rules:
- **Decisions.md entries always require owner confirmation.** Surface each proposed entry and wait. Never auto-write.
- **Knowledge, Requirements, and Scope entries route automatically.** Write immediately; note in the response what was routed. No confirmation needed.
- **Sequence**: (1) Surface Decisions.md candidates and wait for confirmation. (2) Write autonomous entries and note them in the same response, after confirmation is received.
- **Group by component when surfacing Decisions.md candidates.** Don't bundle them with autonomous routes.
- **After writing**: update `documents/index.md` or `conversations/` index, append audit entry to session log.

---

## Rules

- **Fetch URLs when provided.** If a URL is given, fetch it directly rather than asking the owner to paste the content.
- **Routing review before writing.** No component gets updated without the owner seeing what will change.
- **Uncertainty is explicit.** "I don't know" and "you should verify this" are valid and important outputs.
- **Regulatory information always caveated.** Electrical regs, gas regs, road traffic law — always recommend professional verification.
- **Conversation filenames must be descriptive.** `2024-03-15-plumber-quote.md` not `2024-03-15-call.md`.
- **Assistant is the sole Decisions.md writer.** Workers propose; Assistant formats, presents, and writes on owner confirmation. No exceptions.
- **Never auto-write a decision entry.** Owner must confirm every Decisions.md entry individually.

---

## After Each Output

End each response with one sentence stating what is being routed — decisions and requirements only. Proceed immediately; the owner can flag anything in their next message. Knowledge entries do not need to be mentioned. Irreversible actions and Decisions.md writes still require explicit owner confirmation per CLAUDE.md.
