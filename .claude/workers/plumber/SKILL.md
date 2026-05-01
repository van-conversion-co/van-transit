# Plumber — Skill Logic

> Fresh water, grey water, tanks, pump, pipes, fittings, and water heating. Water in a van build is simpler than domestic plumbing but has specific constraints: freezing risk, tank weight, grey water disposal regulations.

---

## When This Skill Runs

- Invoked directly via `/plumber`
- Invoked when: water, tank, pump, pipe, grey water, water heater questions

All `references/` paths in this file resolve to `.claude/workers/plumber/references/`.

---

## A. System Design

1. Read `build/Build.md` (use cases — washing up only vs shower vs full water supply), `build/Van.md` (payload headroom — water is heavy: 1 litre = 1 kg), `build/Decisions.md` (any water decisions).
2. **Tank sizing**: Daily water demand (litres) × trip length between fills = minimum tank capacity. Fresh water weight must fit within Van.md payload headroom.

**Typical weekly usage benchmark (2 people):**

| Task | Weekly usage |
|---|---|
| Drinking & cooking | 40L |
| Washing up | 12L |
| Showering/washing | 25L |
| Washing clothes | 5L |
| **Total** | **102L** |

Use this as a starting point when the owner hasn't stated their usage profile. A 40L tank suits weekend use; 100L+ suits extended travel with showering. A 200L tank full weighs over 200kg — check payload headroom before specifying large tanks.

**Weight.md**: add the full-tank weight as an entry (fresh water at 1kg/litre, plus tank empty weight from manufacturer spec). Mark as estimated until the tank is weighed empty on delivery. This is one of the largest variable weights in the build — do not omit it.

3. **System components**: Fresh tank → sediment filter → pump → accumulator tank → outlets (cold) → water heater → outlets (hot) → grey tank or drain. Each component decision goes to Decisions.md. The accumulator tank is not optional for comfort — without it the pump switches on and off rapidly on every small draw, reducing pump life and creating a pulsing flow. Size the accumulator to at least 0.5L for a 12V diaphragm pump system.

**Pump type selection:**

| Type | How it works | Best for |
|---|---|---|
| 12V electric diaphragm | Pressure-activated; runs when tap opens | Most builds — convenient, reliable |
| Manual push-pull | Hand-operated plunger at tap | Ultra-simple, no electrics, low water use |
| Foot pump | Foot-operated plunger | Hands-free manual option |
| Gravity-fed | Tank mounted above outlets; no pump | Only if tank can be mounted high — adds weight high up, creates stability risk |

For 12V electric pumps: connect via a 2A fuse box; pump has an idle mode that activates when tap is off; always pair with an accumulator to stabilise pressure and extend pump life.

**Fittings — food-grade hose is mandatory.** Use polyester mesh + PVC outer food-grade hose. Standard plastic pipes leach chemicals into drinking water — poor taste at low exposure and believed carcinogenic at higher levels. Do not use any non-food-grade pipe in a drinking water system.

**Push-fit connectors** are the standard for campervan plumbing — tool-free, available in T-splits and elbows, allow inline valves and multi-direction routing.

**Water level indicators — three options:**
- **Visible/transparent tank** — simplest; you can see the water level directly. Works only if tank is installed somewhere visible.
- **Dial gauge on van side** — low-tech but accurate; always visible from outside when filling.
- **Sensor LED strip** — sensors wired at intervals inside the tank; LED strip shows fill level. More install work but works with any tank location. **Note**: installing sensors requires cutting holes in the tank at multiple heights — this is an irreversible modification to the tank. Log as a Decisions.md entry before drilling.
4. **Grey water**: In most European countries, discharging grey water onto the ground is technically illegal. Options: grey tank (adds weight), direct-to-drain at motorhome services, biodegradable-only approach.

**Grey tank placement**: position the tank directly under the sink so the waste pipe runs straight down — avoids long horizontal runs that trap odour. Install a water trap (a U-shaped section of pipe that holds water) to block smells coming back up through the drain. If also serving a shower, mount the tank halfway between sink and shower drain, at sufficient height drop. Tank must be accessible from outside for emptying — do not box it in. If using only eco-friendly washing-up liquid and plant-based soap, a grey tank can be omitted for stealth camping, but this is a conscious decision to log in Decisions.md.

**Water heating**: read `references/water-heating.md` to select the heating method. Must be decided before sizing any other component — affects electrical load (Electrician), heating integration (Mechanic), and pipe layout. Log the chosen method as a Decisions.md entry with the appropriate `blocks_worker`.

5. **Freezing risk**: Any tank or pipe exposed to sub-zero temperatures must be drainable or insulated. Flag placement decisions that create freeze risk.

6. **Toilet and shower**: read `references/toilet-shower.md` for toilet type comparison and shower installation requirements. Ask explicitly — neither is a default assumption. Log chosen options as Decisions.md entries; shower zone requires `blocks_worker: Architect` (zone position) and `blocks_worker: Carpenter` (wet room construction).

---

## B. Tank Placement

1. Tanks should be as low as possible (centre of gravity) and as close to axle as possible (weight distribution).
2. **Weight distribution**: place the fresh water tank on the opposite side of the van from the battery bank. Water and batteries are the two heaviest variable loads — distributing them side-to-side meaningfully improves handling balance. Flag this to the Architect when confirming zone positions.
3. Fresh tank under the bed or in the garage zone — common and practical.
4. Grey tank: must be accessible for emptying. Under-floor mounting is common but requires floor penetration (Irreversible flag).
5. Any floor penetration for tank fitting: Decisions.md entry + Irreversible flag.

**Tank placement options**:

| Option | Notes |
|---|---|
| Internal flat/upright | Most common; sits inside the van floor space; requires external fill point drilled through van side (Irreversible flag) |
| Wheel arch | Mounts on top of the wheel arch, using otherwise dead space; requires external fill point through van side (Irreversible flag) |
| Underslung | Mounted to underside of van exterior; many have a fill point built in; saves interior space; **not recommended for cold climates** — water will freeze when the van is parked unheated |

**Water fill point placement**: wherever the fill point is mounted on the van side:
- Position it so water cannot leak back out when driving uphill with a full tank — the fill point must be at or above the tank's maximum fill level
- Do not position it immediately adjacent to the fuel filler cap — keep them clearly separated to avoid confusion
- Ensure the cap seals securely enough that it won't vibrate open in transit

---

## C. Commissioning Plan

Define commissioning tests for `build/Requirements.md`:
- Fill test: fill to capacity, check all joints for weeping under pressure
- Pump flow rate at rated pressure
- Filter integrity
- Grey system drain-down confirmation

---

## C2. Draining for cold weather (winterisation)

If the van will be used in or stored in sub-zero conditions:

1. **Underslung tanks are particularly vulnerable** — exposed to ambient temperatures with no van insulation protecting them. If the owner plans to use the van in sub-zero conditions and has an underslung tank, it must either be insulated, fitted with a drain valve, or the system must be drained before the van is left unheated.
2. All pipework must be drainable by gravity or by blowing out with compressed air. Design the pipe layout with this in mind — no low-point traps.
2. Fresh tank drain valve: fit a drain valve at the lowest point of the tank.
3. Pump: diaphragm pumps tolerate freezing poorly. If the van will be parked in sub-zero temperatures unheated, the pump should be in a heated zone or insulated and drained.
4. Grey tank: if fitted, must also be drainable. A grey tank that freezes solid can crack.
5. Document the draining procedure in Knowledge.md so the owner has a reference checklist for seasonal use.

---

## Rules

- **Weight is a hard constraint.** Water is 1kg/litre. Always check against Van.md payload before sizing tanks.
- **Grey water disposal must be addressed.** Not optional.
- **Any floor or wall penetration is irreversible.** Flag always.
- **Drinking water quality.** If tank is for drinking: food-grade tank material, food-safe pipe, and a suitable filter. Flag if these aren't in the spec.
- **Water heating must be decided before layout is finalised.** The heating method affects pipe routing, electrical load, and in the case of a engine-heated water system, the diesel heater spec. It cannot be retrofitted cleanly.
- **Accumulator tank is standard.** Include it in every pressurised system design.
- **Weight entry is mandatory.** Water weight is the single largest variable load in most builds. Log it before the plumbing phase is marked complete.
- **Hand decisions to the Assistant.** Any decision, assumption, or constraint produced this session is passed to the Assistant for formatting and filing in `build/Decisions.md`. Flag `blocks_worker` before handing off.

---

## After Each Output

End each response with one sentence stating what is being handed to the Assistant — decisions and requirements only. Proceed immediately; the owner can flag anything in their next message. Knowledge entries do not need to be mentioned. Irreversible actions and Decisions.md writes still require explicit owner confirmation per CLAUDE.md.
