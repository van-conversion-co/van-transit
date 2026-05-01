# Gas System Design

Use when LPG is in scope. Read before advising on tank selection, pipe runs, manifold layout, or commissioning requirements.

---

**Safety first**: all LPG gas work must be checked by a Gas Safe registered engineer before the system is commissioned. LPG is highly flammable and can cause carbon monoxide poisoning. Log this as a mandatory commissioning requirement in Requirements.md.

**LPG basics**: LPG (liquefied petroleum gas) is propane stored in a pressurised tank at ~7,600mbar at 21°C. It weighs approximately 1.75× the equivalent volume of water — a full 40L tank weighs ~70kg. Flag gas tank weight to Architect for payload calculation alongside the water tank. The 'rotten egg' smell is an odorant added specifically for leak detection — if you smell it, treat it as a real leak.

**High and low pressure sides**: every LPG system has two pressure zones separated by the pressure regulator. The **high pressure side** (7,600mbar) runs from the fill point through the cylinder to the pressure regulator. The **low pressure side** (~30mbar, max flow rate 1.5kg/h) runs from the regulator to all appliances. The pressure regulator is therefore a critical component — it must be correctly specified and installed. Everything downstream of it (all pipe runs, manifold, appliances) is low pressure; everything upstream is high pressure and must be treated accordingly.

**Tank type selection**:

| Type | Cost | Refill cost | Sizes | Notes |
|---|---|---|---|---|
| Replaceable gas bottle (e.g. Calor) | ~£160 (40L) | ~43p/litre | 3.9–13L | Swapped for a full bottle; widely available in UK; must be stored in a metal-lined locker with drop out vent |
| Refillable internal gas bottle | ~£210 | ~40–48p/litre | 2.7–11L | Refilled at LPG stations; can add an external fill point; also requires metal-lined locker |
| Refillable underslung tank | ~£250 | ~40p/litre | 16–100L | Mounted on underside of van exterior; largest capacity; needs external fill point installed; less available on mainland Europe |

**Europe travel note**: LPG fill point nozzles differ between UK and mainland Europe — purchase a multi-adapter before any European trip.

**Pipe and hose selection**:

| Type | Van use | Notes |
|---|---|---|
| Flexible rubber hose (synthetic rubber + thermoplastic mesh) | Moveable connections only, max 75cm (8mm OD) | The correct choice where appliances or tanks need to move while the gas supply is connected (e.g. tankless heater used outside, sliding appliances). NOT for permanent interior runs — degrades over time, vulnerable to vibration and chafing |
| Malleable tube (PVC-coated copper) | Permanent interior runs — the standard choice | Bend with a pipe/tube bender; minimum bend radius = outer diameter × 3; a split or kink is a weak point — replace, do not patch |
| Rigid copper pipe | Not recommended for van builds | Vibration cracks it over time; each elbow requires angled connectors — avoid |

**Sizing**: combined appliance capacity typically under 100ft³/hr. Design for 15–28mm pipe sizes; use reducers to transition between sizes.

**Gas manifold**: if feeding more than one appliance, fit a manifold in an accessible location (e.g. kitchen area). Allows individual appliances to be isolated. Good practice to turn each appliance off at the manifold when leaving the van. **If only one appliance is being supplied**, a manifold is not needed — connect directly from the cylinder using an isolator valve instead.

**Drop out vents — mandatory**: LPG is ~3× heavier than air and sinks to the floor. Install a drop out vent under every connection that could leak:
- At the gas manifold
- At any pipe-to-pipe connection
- Where gas connects to each appliance
- Any gas bottle stored inside the van must be in a metal-lined locker with its own drop out vent to the exterior

**Carbon monoxide alarms**: position near potential leak paths — at minimum near the manifold and in the primary living space.
