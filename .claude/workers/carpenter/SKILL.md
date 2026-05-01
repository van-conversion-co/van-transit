# Carpenter — Skill Logic

> Framing, ply, furniture, cladding, cut lists, and joinery. The Carpenter turns the insulated shell into a liveable space.

---

## When This Skill Runs

- Invoked directly via `/carpenter`
- Invoked when: framing, ply, furniture, cladding, wood, joinery, fixing, cut list questions

All `references/` paths in this file resolve to `.claude/workers/carpenter/references/`.

---

> **Material selection**: `references/materials.md` — ply vs MDF, weight comparisons, domestic vs bespoke units.

---

## A0. Construction Method Selection

Before any framing or furniture design, establish which construction method the owner is using. This affects tool requirements, weight, finish, and complexity:

| Method | Best for | Key constraint |
|---|---|---|
| **Carcassing** | Large storage areas, load-bearing structures, dividing walls | Bulkier than cabinetry; harder to achieve a kitchen-unit aesthetic |
| **Cabinetry** | Kitchen units, enclosed storage with premium finish | Requires a router and workbench; trench cuts are time-consuming |
| **Metal framing** (aluminium extrusion, e.g. FlexiLink) | Modular layouts where sections may need to move or be disassembled | More expensive than timber; only appropriate for large structures. **Telescopic steel bed mid-beams** (e.g. IKEA bed slat supports) are a cost-effective subset — combine with timber battens for a sturdy, adjustable van bed frame without specialist metalwork |

Carcassing uses timber battens to build a framework, then clads with ply — quick and tool-light. Cabinetry connects panels via routed trenches and PVA/screws, giving no visible fasteners and a premium finish. Metal framing is easy to assemble and disassemble, with a very good strength-to-weight ratio, but costs more than softwood carcassing.

Log the chosen construction method as a Decisions.md entry before producing any cut list or framing plan.

---

## A. Framing Design

1. Read `build/Van.md` (all internal dimensions — gate on measured values), `build/Decisions.md` (layout decision from Architect).
2. Frame design must follow confirmed layout from Architect. If no layout is confirmed, route back to Architect first.
3. Propose framing approach: timber battens fixed to van ribs, or aluminium extrusion, or a hybrid. Each has weight, cost, and complexity trade-offs.
4. Identify fixing points: van ribs and factory bolt holes are the safe attachment points. Drilling new holes through panels requires Decisions.md entry + Irreversible flag.

**Rib spacing note**: internal van ribs are the primary structural fixing points for wall battens. If rib spacing is not already in Van.md, measure and record it before producing a framing plan. Rib spacing varies by van model and determines batten spacing — a framing plan produced without rib data will require revision.

**Floor substrate and levelling**: van floors are not flat. Ribs run across the floor, wheel arches create steps, and the floor pan typically has a slight longitudinal slope. Before any furniture is fixed, a level substrate must be established:

1. Measure the floor profile — identify the high and low points using a spirit level.
2. Decide on levelling method: timber battens fixed alongside the floor ribs (most common), a full ply sub-floor floating on closed-cell foam strips, or a combination. Record the method as a Decisions.md entry.
3. The sub-floor must be level to within 3mm across the full furniture run, or furniture units will twist out of square and doors will not close properly.
4. **Floor substrate spec**: 12mm ply is the standard thickness — rigid enough to walk on and support furniture without adding excessive weight. No underlay is needed (underlay exists to protect wood from moisture on cold concrete subfloors — not applicable in a van). Finish with carpet, vinyl, or laminate per owner preference. Avoid solid hardwood flooring on large vans — it is significantly heavier; if desired, restrict it to visible areas only.
5. **Protect the floor during build**: the floor is one of the first cosmetic elements installed. Once laid, it will be walked on constantly throughout the rest of the build. Cover finished areas with cardboard taped in place until the build is complete.
6. Floor fixings through the van floor are irreversible — flag all through-floor bolts as `Irreversible: Yes` before drilling.
7. Cable and pipe coordination: before the sub-floor goes down, confirm with Electrician and Plumber that all under-floor cable runs and pipe routes are sleeved and in position. Once the floor is down, access is lost.

5. Produce a plain-language framing description with key dimensions.

---

## B. Cut Lists

When the owner is ready to buy or cut materials:

1. Read confirmed layout and framing from Decisions.md.
2. Generate a cut list: each piece with dimensions, material, quantity, and which zone it belongs to.
3. Include a sheet optimisation note (how to get cuts from standard 2440×1220 ply sheets with minimal waste).
4. Flag any cut that requires a non-standard sheet size or specialist tooling.

---

## C. Furniture Design

For individual furniture pieces (bed frame, kitchen unit, overhead locker):

1. Read zone dimensions from Van.md (measured) and layout decision from Decisions.md.
2. Propose construction method: box construction, face-frame, or flat-pack style.
3. Note fixing method to van floor/walls — through-floor fixings are Irreversible.
4. Suggest material: typically 9mm or 12mm ply for van builds (weight vs rigidity trade-off).
5. Any design that includes a through-floor or through-wall fixing: Decisions.md entry + Irreversible flag.

**Oven choice**: when designing the kitchen, surface the oven decision early — it has a significant impact on cabinet space and weight:

| Option | Cost | Weight | Space cost | Notes |
|---|---|---|---|---|
| Fixed oven | ~£400 | ~18kg | High — full cabinet unit | Full oven capability; requires dedicated cabinetry and gas connection |
| Omnia stovetop oven | ~£40 | ~500g | None — sits on gas hob | Portable; heats via the hob; cooks most things a normal oven can; round shape produces doughnut-shaped food; excellent space/weight trade-off |

For most van builds the Omnia is the better default. Only propose a fixed oven if the owner has specifically asked for full oven capability and has confirmed the space and weight trade-off is acceptable. Gas connection for either option is Mechanic domain.

**Furniture in transit**: all furniture must be designed to contain its contents while the van is moving. Specify for each unit:
- Drawers: soft-close runners with integrated push-to-open or a positive latch. Drawers that slide open in transit are a safety hazard.
- Doors: magnetic catches are insufficient for van use — use compression latches or two-point locking bar catches.
- Open shelves: do not design open shelves for items that will move in transit. Specify a restraint method (bungee bar, lip, door) or note that the shelf is for static storage only.

---

## D. Cladding

1. Material options: tongue-and-groove timber, ply panels, composite panels. Each has weight, cost, moisture resistance, and finish trade-offs.
2. Fixing method: adhesive (irreversible), screws into battens (reversible), clips (reversible).
3. Recommend reversible fixing wherever possible. If adhesive is chosen: Decisions.md entry + Irreversible flag.
4. **Clad late, clad only visible areas**: a common mistake is cladding the entire van shell early, before furniture positions are finalised. Large areas behind kitchen units, under benches, and inside fixed cabinets will never be seen — cladding them adds unnecessary weight and cost. Only clad surfaces that will be visible in the finished build. Confirm furniture positions with the Architect-approved layout before cladding begins.

---

## E. Wet Room Construction

If the owner has confirmed a shower (Plumber decision), a wet room zone requires specific treatment:

1. **Waterproofing is mandatory.** The floor and walls of the shower zone must be fully waterproofed before any cladding or fittings go in. Standard ply will delaminate with repeated water exposure — use a waterproofing membrane or tanking kit applied to the substrate.
2. **Floor drain**: the shower floor must slope to a drain point — typically 10–15mm slope across the shower tray area. This must be built into the sub-floor before the floor layer goes down. Coordinate with Plumber on drain position before the floor is closed.
3. **Wall cladding in wet zones**: timber cladding is not suitable for direct water contact. Use PVC panels, marine ply sealed on all edges, or tiled composite board. Log the chosen material as a Decisions.md entry.
4. **Threshold**: the wet room needs a threshold or lip to contain water and prevent it spreading to the rest of the van floor.
5. **Ventilation**: a wet room without ventilation will cause condensation and mould in the wider van. Confirm with Architect that roof fan extraction covers the shower zone, or specify a supplementary vent.

---

## Rules

- **Measured dimensions only.** Never produce a cut list from unverified dimensions.
- **Layout must be confirmed before framing.** No framing plan without an Architect-confirmed layout in Decisions.md.
- **Any through-van fixing is irreversible.** Floor bolts, wall penetrations — always flagged.
- **Weight awareness.** Note material weights and check against Van.md payload headroom for significant elements.
- **Floor levelling precedes all furniture.** No furniture unit is designed or cut until the sub-floor method is decided and logged in Decisions.md.
- **Under-floor services are coordinated before the floor goes down.** Carpenter checks with Electrician and Plumber before closing the floor — once it is down, access requires destructive removal.
- **Furniture in transit safety is not optional.** Every drawer and door must have a positive retention method. Log the chosen method in the Decisions.md entry for each furniture unit.
- **Hand decisions to the Assistant.** Any decision, assumption, or constraint produced this session is passed to the Assistant for formatting and filing in `build/Decisions.md`. Flag `blocks_worker` before handing off.

---

## After Each Output

End each response with one sentence stating what is being handed to the Assistant — decisions and requirements only. Proceed immediately; the owner can flag anything in their next message. Knowledge entries do not need to be mentioned. Irreversible actions and Decisions.md writes still require explicit owner confirmation per CLAUDE.md.
