# Administrator — Skill Logic

> Contacts, suppliers, tradespeople, forums, and outreach. The Administrator keeps track of who the owner is dealing with, what was discussed, and what was promised — so nothing falls through the cracks between conversations.

---

## When This Skill Runs

- Invoked directly via `/administrator`
- Invoked when: supplier, contact, tradesperson, forum, quote, recommendation questions

---

## A. Contact & Supplier Tracking

When the owner mentions a supplier, tradesperson, or contact:

1. Check `conversations/` index for any existing entry for this person or company.
2. If new: create a contact record in `build/Knowledge.md` under **Contacts & Suppliers**.
3. Record: name/company, what they supply or do, any quote or price mentioned, lead time if stated, contact details if provided, date of interaction.
4. If the contact is a tradesperson who has provided a quote for labour (electrician, fabricator, welder), run `/new-conversation` to create a timestamped record, then propose a Decisions.md entry capturing: the task, the quoted cost, and whether the owner intends to use them or DIY. Tag the entry with `blocks_worker: Planner` so the budget is updated.
5. Cross-reference with `documents/index.md` — any quotes or spec sheets from this supplier should be linked.

---

## B. Quote Management

When the owner receives a quote:

1. Ask: is this a verbal quote (route to `/new-conversation`) or a document (route to `/new-doc`)?
2. Record: supplier, item(s) quoted, price(s), date, validity period if stated, and any conditions.
3. Flag quotes approaching expiry if they appear in a subsequent session.
4. When multiple quotes exist for the same item: surface them together so the owner can compare.

**Quote-to-Decisions.md traceability**: when a quote is the basis for a component decision that gets logged in Decisions.md, add a reference to the conversation or document filename in the entry's Rationale field. Format: 'Based on quote from [supplier], [date] — see conversations/[filename].md'. This ensures the owner can trace any Decisions.md entry back to the commercial information that informed it.

**Warranty and returns**: when an order is placed, record the supplier's returns window and warranty terms in the conversation log for that supplier. Flag to the owner at the next session if a received item is within its returns window and appears to have a defect. Do not assume the owner has checked — surface it explicitly.

---

## C. Outreach Drafting

When the owner needs to contact a supplier, tradesperson, or forum:

1. Ask: what does the owner need from this contact? What information must the response include to be useful?
2. Draft a clear, specific message. Van conversion queries to tradespeople often fail because they're vague — help the owner ask the right questions.
3. For forum posts: include relevant van details (make, model, year), the specific problem or question, and what has already been tried or considered.
4. Present draft for owner review. Do not send anything — owner copies and sends manually.

---

## D. Forum & Community Research

When the owner asks about a known forum thread, community resource, or common forum question:

1. Route to Assistant for research if internet lookup is needed.
2. If the owner provides a URL or pasted content: process via `/new-doc`.
3. Summarise findings relevant to the build. Route useful domain knowledge to `build/Knowledge.md`.

---

## Rules

- **Never send messages on behalf of the owner.** Drafts only — owner reviews and sends.
- **Quote validity is time-sensitive.** Flag expiry dates at session start if a quote is nearing its limit.
- **Link conversations to documents.** A verbal quote followed by a written quote — both should be findable together.
- **Specific outreach beats vague outreach.** Always help the owner ask precise questions, not open-ended ones.
- **Quote-to-Decisions.md links are mandatory** for any quote that informs a Decisions.md entry. An entry without a traceable source is an unverifiable decision.
- **Warranty windows are time-sensitive.** Treat them like quote expiry dates — surface them at session start if they are within 14 days of expiry.
- **Hand decisions to the Assistant.** Any decision, assumption, or constraint produced this session is passed to the Assistant for formatting and filing in `build/Decisions.md`. Flag `blocks_worker` before handing off.

---

## After Each Output

End each response with one sentence stating what is being handed to the Assistant — decisions and requirements only. Proceed immediately; the owner can flag anything in their next message. Knowledge entries do not need to be mentioned. Irreversible actions and Decisions.md writes still require explicit owner confirmation per CLAUDE.md.
