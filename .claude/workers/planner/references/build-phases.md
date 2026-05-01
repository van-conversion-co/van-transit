# Canonical Build Phase Sequence

This is a scaffold, not a script. The Planner reasons from it — it does not copy it. The output in `Scope.md` is always build-specific.

---

## Hard Ordering Constraints

These constraints are non-negotiable. Violating them causes rework or safety failures.

- **P1 before any conversion work** — van must be owned and serviced before any build begins
- **P2 before P3** — vehicle must be mechanically sound before exterior modifications
- **P3 before P4** — roof penetrations must be cut and sealed before insulation goes around them
- **P5 before P6** — framing defines furniture positions which constrain cable and pipe routes
- **P6 before P7** — rough-in must be complete before electrical components are fitted
- **P6 before P8** — no surface closes up until all hidden services are signed off
- **P9 before P10 and P11** — furniture positions must be confirmed before tank fitting and appliance connections

---

## Split-Phase System Ownership

Three systems span multiple phases. Assign the right worker to the right sub-phase:

| System | P6 (rough-in) | Later phase (fit-out) |
|---|---|---|
| Electrical | Electrician owns cable runs and conduit | Electrician owns component fitting and commissioning (P7) |
| Water | Plumber owns pipe routes | Plumber owns tank fitting, pump, and connections (P10) |
| Gas & heating | Mechanic owns gas pipe routes | Mechanic owns appliance connections and heater first fire (P11) |

---

## Phase Entries

---

### P0 — Setup

**Goal**: Establish project infrastructure — files, tools, and build identity — before any physical work begins.

**Typical task categories**: project file creation, van research, budget framing, supplier shortlisting

**Hard dependencies**: none

**Worker ownership**: Assistant (file setup), Planner (budget framing)

**Common omissions**: not setting a budget ceiling before sourcing a van

**Drop conditions**: never dropped — always the first phase

**Quality gate**: `Build.md` exists with use cases and non-negotiables owner-confirmed; phase structure generation flow run and owner-confirmed (adapted phase list written to `Scope.md`); project setup complete

---

### P1 — Van purchase

**Goal**: Acquire the base vehicle and confirm it is mechanically ready to convert.

**Typical task categories**: van sourcing, pre-purchase inspection, purchase, insurance, registration, full service, MOT check

**Hard dependencies**: P0 complete

**Worker ownership**: Mechanic (inspection, service), Administrator (purchase admin, insurance)

**Common omissions**: skipping independent inspection before purchase; buying without service history; underestimating van cost as share of total budget

**Drop conditions**: never dropped

**Quality gate**: van purchased, registered, and insured; full service completed; no outstanding mechanical issues flagged

---

### P2 — Vehicle preparation

**Goal**: Strip the van interior and address all structural, rust, or moisture issues before the build begins.

**Typical task categories**: interior strip-out, rust treatment, bare-metal priming, cavity injection, damp assessment, panel repair, underseal inspection

**Hard dependencies**: P1 complete

**Worker ownership**: Builder (rust, proofing), Mechanic (underseal, mechanical prep)

**Common omissions**: missing rust behind wheel arch liners; not treating cut edges immediately; skipping underseal refresh on high-mileage vans

**Drop conditions**: never dropped

**Quality gate**: interior fully stripped; all rust treated and primed; no active damp; underseal assessed; van ready for exterior work

---

### P3 — Exterior

**Goal**: Complete all exterior modifications — roof penetrations, body work, external fixings — before interior work begins.

**Typical task categories**: roof fan aperture, solar panel mounting points, roof rack fitting, cable entry glands, body repair, paint correction, sealing all penetrations

**Hard dependencies**: P2 complete

**Worker ownership**: Architect (position decisions — irreversible), Builder (aperture cutting, sealing), Mechanic (body work, roof rack)

**Split-phase notes**: Architect owns roof fan position decision in P3 and raises a `Decisions.md` entry marked `Irreversible: Yes` and `blocks_worker: Builder`. Builder executes aperture and sealing only after that entry is confirmed.

**Common omissions**: forgetting to seal around cable glands; not planning cable entry point positions relative to internal routes; skipping roof rack fixing point reinforcement

**Drop conditions**: phase is reduced if no roof fan, no solar, and no rack — but cable entry points and sealing still apply; phase is never fully dropped

**Quality gate**: all exterior penetrations cut and sealed; no open holes; all external components weather-tight; Architect has confirmed all aperture positions in `Decisions.md`

---

### P4 — Insulating

**Goal**: Achieve full thermal and acoustic coverage of the van shell before framing starts.

**Typical task categories**: soundproofing (deadening mats), thermal insulation (spray foam, PIR boards, wool), vapour barrier, wheel arch insulation, condensation management

**Hard dependencies**: P3 complete

**Worker ownership**: Builder

**Common omissions**: missing wheel arch cavities; not insulating the floor slab before sub-floor goes down; leaving thermal bridges at structural ribs; no vapour barrier strategy

**Drop conditions**: never dropped — even minimal insulation is a phase entry

**Quality gate**: all panels insulated per specified strategy; vapour barrier fitted where specified; no exposed metal behind future cladding; Builder signs off before framing starts

---

### P5 — Sub-floor & framing

**Goal**: Build the structural skeleton — sub-floor, riser, and wall/ceiling framing — that defines furniture positions and constrains all service routes.

**Typical task categories**: sub-floor batten layout, sub-floor boarding, wheel arch boxing, riser construction, wall framing, ceiling framing, structural bed frame (if part of skeleton)

**Hard dependencies**: P4 complete

**Worker ownership**: Carpenter

**Common omissions**: not accounting for wheel arch height in bed riser; framing that leaves no service channels; sub-floor that blocks drainage; framing fixed before service routes confirmed with Electrician and Plumber

**Drop conditions**: sub-floor is always required; framing scope varies with build complexity but is never zero

**Quality gate**: sub-floor level and fixed; framing positions confirmed with Architect; service channels adequate for planned cable and pipe routes (confirmed with Electrician and Plumber); owner sign-off before any cables are run

---

### P6 — Cables & pipes

**Goal**: Run all hidden services — electrical cables, water pipes, and gas pipes — before the interior closes up permanently.

**Typical task categories**: 12V cable runs, 230V cable runs, conduit and cable management, fusing and bus bar positions, water pipe runs (fresh and grey), gas pipe runs, cable labelling

**Hard dependencies**: P5 complete

**Worker ownership**: Electrician (electrical), Plumber (water pipe routes), Mechanic (gas pipe routes)

**Split-phase notes**: all three systems start here (rough-in) and complete in later phases — see split-phase ownership table above.

**Common omissions**: not leaving enough cable length at endpoints; missing conduit for future serviceability; no earth continuity run; labels not applied before walls close; no draw wire left in conduit for future pulls

**Drop conditions**: phase scope varies with systems in scope — a gas-free build has no gas pipe runs, but the phase still exists for electrical and water

**Quality gate**: all cable runs complete and labelled; all pipe routes run and supported; no hidden service ends inaccessible; Electrician, Plumber, and Mechanic (where applicable) sign off before cladding

---

### P7 — Electrical system

**Goal**: Fit, connect, and commission all electrical components — batteries, solar, consumer unit, inverter, and 12V loads.

**Typical task categories**: battery installation, solar controller fitting, inverter fitting, consumer unit or fuse panel, 12V distribution, 230V distribution, shore power inlet, component commissioning and testing

**Hard dependencies**: P6 complete

**Worker ownership**: Electrician

**Common omissions**: not testing circuits before closing walls; no earth fault test; missing 230V RCD protection; battery monitoring not wired; shore power inlet not labelled

**Drop conditions**: 230V section is dropped if no inverter or shore power; phase always runs for any electrical system

**Quality gate**: all circuits tested; earth continuity verified; RCD trips tested where 230V is fitted; system operates at expected load; Electrician signs off before walls close

---

### P8 — Floors & walls

**Goal**: Close up the interior — floor, wall cladding, and ceiling — permanently covering all hidden services.

**Typical task categories**: floor laying (vinyl, LVT, ply), wall cladding (ply lining, T&G, strips), ceiling lining, trim and edge finishing

**Hard dependencies**: P6 signed off and P7 commissioning complete

**Worker ownership**: Carpenter, Builder (where structural cladding)

**Common omissions**: not leaving access panels over junction points; floor not sealed at edges allowing water ingress; cladding that closes over an unlabelled junction

**Drop conditions**: never dropped

**Quality gate**: all floors and walls complete; access panels in place over all service junction points; no exposed cable runs; level and flush finish throughout

---

### P9 — Layout construction

**Goal**: Build all permanent furniture structures — units, berths, worktops — that define the living space.

**Typical task categories**: kitchen unit carcasses, worktop fitting, bed platform, storage unit frames, pull-out mechanisms, face frames, wall-mounted storage

**Hard dependencies**: P8 complete

**Worker ownership**: Carpenter

**Common omissions**: worktop height not confirmed with owner before fixing; no clearance checked for appliance doors; tall units not anti-tip fixed

**Drop conditions**: specific units may be dropped per build scope, but the phase always runs

**Quality gate**: all furniture structures in place and fixed; worktop height owner-confirmed; appliance openings dimensionally correct; owner sign-off before plumbing and gas connect

---

### P10 — Water system

**Goal**: Fit the fresh and grey water system — tanks, pump, filter, fittings, and connections.

**Typical task categories**: fresh water tank fitting, grey water tank fitting, pump installation, filter fitting, tap and shower connections, tank sensor wiring

**Hard dependencies**: P9 complete

**Worker ownership**: Plumber

**Common omissions**: no tank vent; grey tank positioned too high to drain by gravity; system not pressure-tested before closing up; no winterisation valve

**Drop conditions**: dropped if the build has no water system (rare but valid for a day-van build)

**Quality gate**: system pressurised and leak tested; pump operates at expected pressure; grey drains correctly; owner confirms before first use

---

### P11 — Gas & heating

**Goal**: Connect appliances, commission the gas system, and carry out the diesel heater first fire.

**Typical task categories**: gas appliance connections, gas system pressure test, diesel heater installation and first fire, flue routing and sealing

**Hard dependencies**: P9 complete

**Worker ownership**: Mechanic (gas connections, diesel heater), Plumber (if wet heating circuit)

**Common omissions**: no CO alarm fitted before first fire; diesel heater flue not sealed against exhaust gas ingress; gas system not pressure tested after final connections

**Drop conditions**: dropped if the build has no gas appliances and no diesel heater (electric-only heating)

**Quality gate**: gas pressure test passed; all connections leak tested with detector; diesel heater fires and holds temperature; CO alarm fitted and tested

---

### P12 — Furnishing

**Goal**: Complete the interior — doors, drawers, soft furnishings, accessories, and all finish details.

**Typical task categories**: cabinet doors and drawer fronts, handles and hardware, mattress and bedding, curtains and blinds, switch plates, ventilation covers, final trim

**Hard dependencies**: P9 complete

**Worker ownership**: Carpenter (doors, drawers, hardware), Owner (soft furnishings)

**Common omissions**: doors that clash when opened together; drawer runners not pre-fitted before face frames go on

**Drop conditions**: never dropped

**Quality gate**: all hardware fitted and operating correctly; interior complete to owner's specification; snag list raised

---

### P13 — Final checks

**Goal**: Commission the full system at load, run a sign-off inspection, and prepare the van for first trip.

**Typical task categories**: integrated electrical test at peak load, water system sign-off, gas safety check, payload verification, snag list resolution, first trip prep

**Hard dependencies**: P12 complete; all applicable system phases complete (P10 if a water system is in scope; P11 if gas or diesel heating is in scope)

**Worker ownership**: Planner (coordination), Electrician, Plumber, Mechanic (domain sign-off)

**Common omissions**: payload not re-checked with full kit on board; no snag list before first trip; electrical system not tested at sustained peak load

**Drop conditions**: never dropped

**Quality gate**: all systems pass domain sign-off; payload within legal limit with kit loaded; snag list resolved or deferred with owner agreement; owner signs off for first trip
