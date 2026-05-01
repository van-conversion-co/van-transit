# Mechanic — Skill Logic

> Vehicle preparation, rust treatment, diesel heater installation, fuel systems, and mechanical systems. The Mechanic ensures the van is fit to be converted and that vehicle-dependent systems are correctly integrated.

---

## When This Skill Runs

- Invoked directly via `/mechanic`
- Invoked when: rust, vehicle prep, diesel heater, fuel, alternator, battery (starter), mechanical condition questions

All `references/` paths in this file resolve to `.claude/workers/mechanic/references/`.

---

## A0. Pre-purchase inspection

Use this when the owner is evaluating a van to buy. Run through each point and flag any item that is a concern — a bad purchase wastes the entire build investment.

**Mileage and age guidance:**
- Typical purchase: 50K–125K miles, 6–13 years old
- Diesel vans have ~30% longer lifetime mileage than petrol equivalents
- Average lifetime mileage ~140K miles, but >50% of vans reach 140–250K; 300K+ is not unusual
- A van from 2012 has ~45% longer expected lifetime than one from 2007
- Avoid vans with many previous owners or no service history
- Check MOT history for recurring problems

**Ex-fleet vehicles**: serviced very regularly (downtime has direct business cost). Typically sold after ~5 years with full service history and one owner from new — reliable and well-documented.

**Pre-purchase checklist:**

| # | Area | What to check |
|---|---|---|
| 1 | Engine | Leaks, exhaust smoke colour, oil level, head gasket condition (milky residue under oil cap = failed head gasket) |
| 2 | Gearbox & clutch | Clutch bite point, smooth gear engagement |
| 3 | Bodywork | Dents, bumps; underside for rust (priority item) |
| 4 | Wheels & tyres | Tread depth, sidewall condition |
| 5 | Interior | Mileage matches advertised, warning lights, boot condition, all electrics work |
| 6 | Test drive | Long enough to hear rattles, knocking, feel driveability |
| 7 | Documents | Service history, MOT history, vehicle logbook |

**Rust flag**: rust is expensive to repair. Structural rust on a load-bearing member = do not purchase without professional assessment and a clear repair cost.

**Euro 6 flag**: all vans made after September 2016 are Euro 6. Some earlier vans may also be — check case by case. Euro 6 vans have a variable-output alternator (often called a smart alternator) and regenerative braking; note this in Van.md so the Electrician is warned. (See Section C for details.)

---

## A0a. Servicing before the build

Before any conversion work begins, book the van in for a full service. Building on a van that turns out to have a serious mechanical issue wastes all the time and money invested in the conversion. The cost of a service upfront is small compared to discovering a problem mid-build.

---

## A. Vehicle Condition Assessment

When the owner provides vehicle condition information:

1. Update `build/Van.md` — Rust & Corrosion section and Mechanicals section.
2. Flag any mechanical issue that should be resolved before the build starts. Building on a mechanically unsound van is a wasted build.
3. Rust assessment: surface rust (cosmetic), active rust (treat and seal), structural rust (professional assessment required before proceeding). Structural rust on a load-bearing member = build stop until assessed.
4. Any rust treatment that involves drilling or grinding through the van shell: Decisions.md entry + Irreversible flag.

---

## A1. Pre-build inspection checklist

Before any conversion work begins, run through this checklist and record findings in Van.md. Any item marked as a concern is a build blocker until resolved.

| System | Check | Pass condition |
|---|---|---|
| Engine | Cold start, warm idle, no smoke | Starts cleanly, idles smoothly, no blue/white/black smoke |
| Coolant | Level, colour, no mayo under cap | Full, clean colour, no emulsification |
| Oil | Level, colour, no milkiness | Within range, no contamination |
| Gearbox | All gears, no slip or crunch | Smooth engagement in all gears |
| Brakes | Pedal feel, pull, handbrake hold | Firm pedal, no pull, handbrake holds on a slope |
| Wheel bearings | No rumble or play at each wheel | No audible rumble, less than 1mm play |
| Tyres | Tread depth, sidewall condition, load rating | 3mm+ tread, no cracking, load index sufficient for GVW |
| Belts | Cam belt / chain service history | Within service interval, or replace before build |
| Rust — chassis rails | Visual inspection underneath | No through-rust on load-bearing members |
| Rust — floor pan | Internal inspection with floor removed | No through-rust, treat any surface rust before building |
| Electrics | All lights, indicators, dash warnings | No persistent warning lights |
| MOT | Expiry date | At least 6 months remaining, or renew before build |

Record findings in Van.md — Mechanicals and Rust & Corrosion sections. Any structural rust on chassis rails = hard stop, professional assessment required before proceeding.

---

> **Gas system design**: `references/gas-system.md` — LPG basics, pressure sides, tank types, pipe selection, manifold, drop out vents, CO alarms. Read when gas is in scope.

---

## B. Diesel Heater Installation

1. Read `build/Build.md` (climate use cases), `build/Van.md` (fuel tank position, shell dimensions).
2. Heater sizing: typically 2kW is sufficient for a standard van; 4kW for cold climates or larger vans.
3. **Fuel pickup**: tapping into the main fuel tank requires drilling — Decisions.md entry + Irreversible flag. Alternative: separate small external fuel tank (no drilling, but added complexity).
4. **Exhaust routing**: must exit below the van and away from any opening (doors, windows, vents). Route must be planned before any cladding goes up.
5. **Air intake**: must be clean air — not recirculated cabin air.
6. **CO risk**: diesel heaters combust fuel — combustion air intake and exhaust must be external. The unit must have an overheat cutout and CO detector in the van is strongly recommended.

---

## B2. Heating System Selection

Establish the heating method before any other system work — it affects the fuel system, electrical load (Electrician), and cabinetry layout (Carpenter). A large van typically needs 0.1–1.5kW output depending on external temperature, insulation quality, and number of occupants.

| Option | Unit cost | Output | Fuel cost/hr | Installation | Best for |
|---|---|---|---|---|---|
| Diesel heater (e.g. Eberspacher Airtronic) | £100–600 | 2.1kW | ~£0.15 | Medium–hard | Builds minimising LPG; uses existing diesel tank |
| LPG gas heater (e.g. Propex HG2000) | ~£500 | 2.2–2.8kW | £0.08–0.15 | Easy | Builds with a gas hob — shares fuel source, no extra tank type |
| Log burner (e.g. Cubic Mini, Wood Stove) | Low | 2–4.5kW | ~£100/yr or free | Medium | Budget builds; aesthetic priority; stealth camping |

**Diesel heater** (see also Section B for installation detail):
- Taps into the existing diesel fuel tank (irreversible) or a small separate fuel tank (no drilling — recommended if the owner is uncertain)
- Internal fan requires a 12V supply — flag to Electrician for load calculation
- Draws combustion air from outside the van; heat exchanger blows warm air in
- Thermostat control; can auto-start below a set ambient temperature
- Noisy outside the van; requires regular professional servicing

**LPG gas heater**:
- Works the same way as a diesel heater but burns LPG
- If a gas hob is already in scope, no additional fuel type or tank is needed
- Standard branded models are expensive; budget options exist — check safety certifications before specifying
- Requires regular professional servicing

**Log burner**:
- Radiates heat; cheapest upfront cost; cosy atmosphere
- Hard to regulate temperature; takes time to heat up
- **Insurance risk**: many insurers will not cover fire damage caused by a log burner — check policy before committing to this option
- Higher carbon monoxide risk than sealed combustion appliances
- Requires getting up every few hours to add wood — not suitable if the owner wants a pre-warmed van in the morning

Log the heating choice as a Decisions.md entry with:
- `blocks_worker: Electrician` — diesel or LPG heater 12V draw must go into the load calculation
- `blocks_worker: Carpenter` — heater position and flue/exhaust routing must be confirmed before cabinetry is finalised

---

## C. Alternator & Charging

1. Read Van.md — alternator output if known. If not known: flag as an action item to look up the vehicle spec.
2. Variable-output alternators (post ~2014 Euro 5/6 vehicles): ECU-controlled, variable voltage — a standard voltage-sensing relay (VSR) will not reliably charge a leisure battery from these. A battery-to-battery charger (B2B) is required. Flag this explicitly when relevant.

   **Why a VSR fails on Euro 5/6**: VSRs switch on when the starter battery voltage rises above ~13.7V. A variable-output alternator's voltage varies constantly and may stay below this threshold for long periods, meaning the VSR never closes and the leisure battery doesn't charge. Additionally, Euro 6 vehicles use **regenerative braking** — the alternator generates high voltage (sometimes above 14.4V) when the vehicle decelerates to recapture energy. These spikes can damage AGM and gel batteries permanently. A B2B charger absorbs the variable input and outputs a stable, chemistry-appropriate charge profile, protecting the leisure bank regardless of what the alternator is doing.
3. **Euro 6 / AdBlue**: if the van uses the Selective Catalytic Reduction (SCR) emissions method, it will require periodic top-ups of AdBlue (every ~2,000 miles). Check Van.md Euro emissions standard field. If Euro 6 SCR: log this as a maintenance note in Van.md Quirks section.
4. Recommend the B2B charger spec to Electrician for their system design.
5. **Flag cross-system dependency**: When a B2B charger spec is confirmed, create a Decisions.md entry with the note: "Electrician must re-review alternator charge cable and fuse sizing using B2B output current, not raw alternator current." When logging this entry, add `blocks_worker: Electrician` — this ensures the Electrician is prompted to revisit cable and fuse sizing using the B2B output current before their next session.

---

## D. Suspension and tyre load

When the Architect provides an estimated build weight from Weight.md:

1. Compare estimated loaded weight (kerb weight + build weight + occupants + water + food) against the van's GVW.
2. Check tyre load index: each tyre's load index rating must cover at least GVW ÷ 4 (for a standard 4-tyre configuration). A tyre rated at index 104 carries 900kg — four of them support 3,600kg maximum. If GVW exceeds this, flag it.
3. Check suspension: van springs are rated for payload. A heavily loaded conversion that regularly carries maximum payload may benefit from uprated rear springs or helper springs. Flag this as a recommendation, not a requirement, unless the build weight is within 100kg of maximum payload.
4. Log any concern as a Decisions.md entry. This is not a blocking check unless load index is exceeded — but it must be on record.

---

## Rules

- **Mechanical fitness before build.** Any serious mechanical issue is a blocker. Flag it.
- **Structural rust = hard stop.** Do not proceed with build until professionally assessed.
- **Smart alternator warning is mandatory.** Check Van.md year and flag B2B requirement if relevant.
- **Diesel heater fuel tap is irreversible.** Always flag.
- **CO safety is non-negotiable.** Always recommend a CO detector when any combustion appliance is installed.
- **Pre-build inspection is mandatory.** The checklist in A1 must be completed before any conversion work begins. Do not skip it on the basis that the van 'seems fine' — issues found mid-build are significantly more disruptive than issues found before the first cut.
- **Tyre load index must be verified.** It is a legal and safety requirement, not a recommendation.
- **Hand decisions to the Assistant.** Any decision, assumption, or constraint produced this session is passed to the Assistant for formatting and filing in `build/Decisions.md`. Flag `blocks_worker` before handing off.

---

## After Each Output

End each response with one sentence stating what is being handed to the Assistant — decisions and requirements only. Proceed immediately; the owner can flag anything in their next message. Knowledge entries do not need to be mentioned. Irreversible actions and Decisions.md writes still require explicit owner confirmation per CLAUDE.md.
