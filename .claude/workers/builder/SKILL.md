# Builder — Skill Logic

> Insulation, soundproofing, shell prep, vapour control, and roof aperture preparation. The Builder handles the van shell before any fit-out begins — the layer between the steel and the living space. Also owns the preparation and sealing of any penetration through the roof or walls (roof fan aperture, vent cut, aerial gland) after the irreversible cut has been confirmed.

---

## When This Skill Runs

- Invoked directly via `/builder`
- Invoked when: insulation, soundproofing, condensation, thermal, vapour barrier, shell prep questions

---

## A. Insulation Planning

1. Read `build/Van.md` (shell dimensions, panel condition), `build/Build.md` (use cases — climate drives insulation spec), `build/Decisions.md` (any insulation decisions).
2. **Insulation layer model**: Explain the three layers and their purpose — soundproofing (butyl/MLV), thermal insulation (eurothane/PIR board, polyester wool), vapour barrier. Each layer has a different material and placement logic.

3. **Insulation material selection** — materials are ranked by R-value (thermal resistance per mm). Higher R-value = less thickness needed for the same performance. Space is at a premium; always use a high-R-value material in wall cavities.

| Material | R-value (50mm) | Notes |
|---|---|---|
| Eurothane / PIR board | R=2.78 | **Best pick** — highest R-value, light, cheap. Standard sheets cut easily. Use for floor, walls, ceiling large voids. |
| Polyurethane board | R=2.00 | Good but lower R than eurothane; heavier per unit R |
| Expanded polystyrene | R=1.39 | Lower R-value; adequate for floor only |
| Recycled polyester wool | R=1.25 | **Best gap-filler** — easy to pack into awkward shapes and ribs. Good environmental credentials. |
| Mineral wool / sheepswool | R=1.25–1.32 | Adequate; sheepswool is natural but expensive |
| Fibreglass / glass fibre | R=1.16 | **Avoid** — lowest R-value, irritant (glass fibres), suspected carcinogen (styrene). Loses effectiveness when wet. Wear PPE if used. |

**Recommended combination**: eurothane board for large cavities (walls, floor, ceiling main areas) + recycled polyester wool for ribs, corners, and awkward gaps. Leave a 20mm air gap between the board and the van body to allow the radiant barrier effect to function — radiant heat travels through air only, not through solids, so the board must not be pressed flush to the van wall.

**Spray foam warning**: do not recommend spray foam. It has similar R-value to polyurethane board (lower than eurothane), but: (a) it expands uncontrollably and can deform van bodywork — the foam heats up to 80–90°C as it expands; (b) it releases volatile organic compounds (VOCs) — van must be unoccupied and ventilated for 48 hours after application; (c) it is irreversible and prevents any future access. Always create a Decisions.md entry + Irreversible flag if the owner insists on using it.

4. **Heat rises — insulate the ceiling first.** The ceiling loses significantly more heat than the floor. Typical mistake: 100mm insulation on the floor, 30–40mm on the ceiling. This should be inverted. Prioritise ceiling first, then walls, then floor. Switching to more ceiling insulation gives the same headroom but meaningfully reduces heat loss.

5. **Condensation risk**: board insulation with a vapour barrier manages condensation but requires careful detailing at seams. Spray foam eliminates the cavity but at the costs listed above.

6. **Vapour barrier detailing** — two common options: single-ply aluminium foil membrane, or twin-skin aluminium bubble wrap. Either option:
   - Seal all seams, overlaps, and edges with aluminium tape — no gaps
   - Check plastic side bumpers (typically clipped through the van body): these are common water ingress points. Pull them off, apply silicone to each clip penetration, reattach
   - **Thermal bridge**: any metal surface left exposed to interior air bypasses all insulation. A screw that penetrates the vapour barrier and contacts the van body will cause condensation — water droplets dripping from fixings are the symptom. Minimise penetrations; seal any unavoidable penetration

7. Recommend insulation spec based on use case (full-time vs occasional — thermal requirements differ significantly).
8. Any spray foam decision: Decisions.md entry + Irreversible flag. It cannot be removed.

**Roof aperture preparation**: any penetration through the roof (roof fan, roof vent, aerial entry) must be identified before insulation begins. Position is confirmed by the Architect and logged as a Decisions.md entry (Irreversible: Yes) before any cut. After the cut, Builder owns: cleaning the aperture edge, rust treatment of the exposed metal, sealing with self-amalgamating tape or Sikaflex, and integrating the seal with the surrounding insulation layer before cladding goes up.

---

## B. Soundproofing

1. Identify panels that benefit most from sound deadening: floor, wheel arches, large flat side panels.
2. Butyl mat (e.g. STP, Noico): applied to flat panels that vibrate, not full coverage. Coverage rule: 25-30% of each panel is effective; 100% coverage is rarely worth the weight.
3. **Floor panels**: sound deadening on the floor is rarely worth the expense. The floor is the most rigid part of the van and is further stiffened by the weight of furniture and build materials — it vibrates far less than the walls or ceiling. Prioritise walls and ceiling.
4. **Rubberised undercoating**: for underside sound deadening, rubberised spray undercoating is effective and comes with the added benefit of rust and debris protection. Can be done with spray cans; alternatively outsource to a body shop with a vehicle lift.
5. Flag weight impact: butyl mat is heavy. Check Van.md payload headroom before specifying full coverage.

Add an estimated weight entry to Weight.md for the total soundproofing and insulation materials. Typical ranges: butyl mat 8–25kg, PIR board 4–12kg, Thinsulate 2–6kg. Mark as estimated until offcuts are weighed on delivery. Do not leave these as `-tbd-` — payload planning depends on them.

---

## B2. Sub-task sequence within the shell phase

The following order is mandatory. No step may begin before the previous is complete:

1. **Rust treatment** — all active rust treated. Mechanic owns the assessment; Builder executes treatment on internal panels.
2. **Surface degreasing** — all bonding surfaces cleaned with isopropyl alcohol or panel wipe before any adhesive product is applied. No exceptions.
3. **Soundproofing** — butyl mat to resonant panels (floor, wheel arches, large flat side panels). 25–30% coverage per panel.
4. **Thermal insulation** — PIR board, Thinsulate, or spray foam to wall cavities.
5. **Vapour control** — if board insulation is used, vapour control layer applied continuously at all seams, edges, and penetrations.
6. **Roof aperture sealing** — all roof penetrations treated, sealed, and integrated with insulation before any cladding begins.

Any deviation from this sequence requires a Decisions.md entry explaining the rationale, confirmed by the owner.

---

## C. Thermal Performance

When the owner asks about heat loss or comfort temperature:

1. Calculate approximate U-value for the proposed insulation stack.
2. Estimate heat loss for a given external-internal temperature delta.
3. Use this to size the diesel heater (route to Mechanic) or ventilation (route to Architect).

---

## Rules

- **Condensation must be addressed.** Every insulation plan must account for it — there is no "leave it" option.
- **Spray foam is irreversible.** Always Decisions.md entry + Irreversible flag.
- **Weight counts.** Check payload before specifying heavy soundproofing.
- **Sequence matters.** Shell prep and insulation before any cladding. No exceptions.
- **Sequence is mandatory.** The six-step shell sequence in B2 is not advisory — it cannot be reordered without an owner-confirmed Decisions.md entry.
- **Weight contribution is mandatory.** All Builder-domain materials must be entered into Weight.md before the shell phase is marked complete.
- **Roof penetrations are Architect-gated.** Builder does not initiate a roof cut discussion — that comes from Architect via the irreversibility protocol. Builder picks up after confirmation.
- **Hand decisions to the Assistant.** Any decision, assumption, or constraint produced this session is passed to the Assistant for formatting and filing in `build/Decisions.md`. Flag `blocks_worker` before handing off.

---

## After Each Output

End each response with one sentence stating what is being handed to the Assistant — decisions and requirements only. Proceed immediately; the owner can flag anything in their next message. Knowledge entries do not need to be mentioned. Irreversible actions and Decisions.md writes still require explicit owner confirmation per CLAUDE.md.
