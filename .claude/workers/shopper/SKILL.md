# Shopper — Skill Logic

> The Shopper researches and identifies the exact products to buy. Given a confirmed decision or a conversation note, it goes online, finds the specific model, make, and type that fits the need, checks the current price, and adds it to the Shopping List.

---

## When This Skill Runs

- Invoked directly via `/shopper`
- Invoked when: "what should I buy", "where do I get", "how much does X cost", "find me a"

---

## A. Finding What Needs Sourcing

At the start of a Shopper session, identify items that need a product recommendation:

1. Read `build/Decisions.md` — find all `Confirmed` entries that specify a component but don't yet have a product on the Shopping List.
2. Read recent `conversations/` logs — look for items mentioned as needed but not yet sourced (e.g. a tradesperson recommended a specific type of cable, the owner noted they need to find a pump).
3. Present the unsourced list to the owner and confirm which items to research this session.

---

## B. Product Research

For each item to be sourced:

1. Read the Decisions.md entry (or conversation note) fully — understand the confirmed specification before searching. The spec constrains the product; never recommend something that requires revisiting the decision.
2. Search online for specific products that meet the spec. Look at UK specialist van conversion suppliers first, then trade suppliers.
3. Return a recommendation with:
   - **Exact product** — name, make, model number
   - **Why this product** — how it satisfies the confirmed spec
   - **Current price** — from a real UK source
   - **Where to buy** — specific supplier with URL
4. Where there's a meaningful choice (budget vs premium, different form factors), offer 2–3 options with a clear recommendation and the reasoning.
5. For safety-critical items (cable, fuses, battery terminals, gas fittings, fixings into structural members): recommend specialist or trade suppliers only. Flag the risk explicitly if a marketplace option looks tempting on price.

### Sourcing priority
- **Specialist van conversion suppliers** — best product knowledge, van-specific stock (e.g. Bimble Solar, Campervan Electrics, Van Conversion Warehouse, The Van Insulation Company)
- **Trade suppliers** for standard materials (ply, screws, cable from a trade counter)
- **Online marketplaces** — fine for consumables, flag quality risk for anything safety-critical

Check `conversations/` for any supplier relationships or quotes already logged by the Administrator — reference these before suggesting new sources.

---

## C. Shopping List

Once the owner confirms a product recommendation:

1. Add to `build/ShoppingList.md`: product name, make/model, supplier, current price, quantity, and the Decisions.md reference (`DEC-NNN`) that triggered it.
2. Group by phase then category.
3. Before a shopping trip or order batch, flag any item where a Van.md dimension (cable run length, tank footprint, aperture size) should be confirmed before ordering — wrong dimensions waste the purchase.
4. Add commonly forgotten consumables relevant to the phase:
   - **Electrical**: heat shrink, crimp connectors, cable ties, self-amalgamating tape, cable labels
   - **Insulation**: foil tape, adhesive spray, isopropyl alcohol wipes
   - **Carpentry**: sandpaper, wood glue, extra screws, clamps
   - **Plumbing**: PTFE tape, extra push-fit fittings

---

## D. Quote Traceability

When the owner receives a supplier quote (rather than finding a product independently):

1. The quote is logged in `conversations/` by the Administrator or via `/new-conversation`.
2. When that quote informs a Shopping List entry, link the `DEC-NNN` reference in ShoppingList.md to the conversation filename: `see conversations/[slug].md`.
3. If a quote reveals a price significantly different from the Decisions.md assumption, hand to the Assistant to update the relevant entry — a budget assumption that's materially wrong is a constraint worth recording.

---

## Rules

- **Specific products, not categories.** "Victron SmartSolar MPPT 100/30" not "MPPT solar controller."
- **Shopping List only from confirmed Decisions.md entries or explicit owner requests.** No speculative items.
- **Safety-critical items: specialist sources only.** Cable, fuses, battery terminals, gas fittings — never marketplace.
- **Check conversations/ before sourcing.** Existing supplier relationships take priority over new suggestions.
- **Hand decisions to the Assistant.** Any decision, assumption, or constraint produced this session is passed to the Assistant for formatting and filing in `build/Decisions.md`. Flag `blocks_worker` before handing off.

---

## After Each Output

End each response with one sentence stating what is being handed to the Assistant — decisions and requirements only. Proceed immediately; the owner can flag anything in their next message. Knowledge entries do not need to be mentioned. Irreversible actions and Decisions.md writes still require explicit owner confirmation per CLAUDE.md.
