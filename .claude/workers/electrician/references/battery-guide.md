# Battery Type Guide

Use when deciding on battery chemistry. Present after load calculation and sizing are complete — the right chemistry depends on how the van will be used.

---

Only **leisure batteries** are suitable for campervan electrical systems. Starter batteries are designed to deliver a large burst of current and be immediately recharged — they are not suitable for sustained deep discharge. Never use a starter battery as the leisure bank.

---

## Types

| Type | Max DoD | Typical lifespan at 50% DoD | Notes |
|---|---|---|---|
| Flooded lead acid (FLA) | 50% | 200 cycles | Must be mounted upright; requires topping up with de-ionised water; hydrogen gas when charging — must be vented. **Not recommended** for van builds. |
| Sealed lead acid (VRLA) | 50% | ~200 cycles | Maintenance-free, sealed. Shorter lifespan than AGM for the same cost. **Not recommended** — pay the small premium for AGM. |
| AGM | 80% | 750 cycles | Thin fibreglass mat holds electrolyte. Can be mounted on its side. No maintenance. Best for cold climates. More sensitive to overcharging than FLA. **Recommended for most builds.** |
| Gel | 80% | 600 cycles | Thick paste electrolyte — mount in any orientation. Performs best in hot climates. Very sensitive to overcharging (easy to damage permanently). Requires a charger with a specific gel charge profile. |
| Lithium ion (LiFePO₄) | 95–97% | 5,000 cycles at 50% DoD | Lightest. Longest lifespan. Can be discharged almost completely. Does not perform below 0°C (heated versions available). High upfront cost. Requires a BMS (Battery Management System). **Recommended for full-time van life or space-constrained builds.** |

---

## Lifecycle at depth of discharge (cycles to end of life)

| Type | 30% DoD | 50% DoD | 80% DoD |
|---|---|---|---|
| Flooded FLA | 460 | 200 | not advised |
| AGM | 1,800 | 750 | 500 |
| Gel | — | 600 | 400 |
| Lithium ion (LiFePO₄) | 10,000 | 5,000 | 2,500 |

A lithium battery used to 50% DoD regularly will outlast an AGM by ~7:1. Because lithium can be discharged to 97% without damage, a smaller Ah lithium bank can deliver the same usable capacity as a larger AGM bank.

---

## Recommendation by use case

| Use case | Recommended chemistry | Rationale |
|---|---|---|
| Occasional weekends | AGM | Low upfront cost, good lifespan for infrequent use |
| Regular weekends + holidays | AGM | Best value, tolerates partial cycling, most charger-compatible |
| Full-time van life | LiFePO₄ | Upfront cost justified by 7× longer lifespan; weight and space saving critical |
| Budget build | AGM | Sealed FLA is cheaper but short lifespan makes it false economy |
| Very hot climate | Gel or LiFePO₄ | AGM degrades in sustained heat; gel performs better; lithium is unaffected |
| Very cold climate (<0°C regularly) | AGM or heated LiFePO₄ | LiFePO₄ cannot charge below 0°C; standard lithium cells stop accepting charge |

---

## Sourcing note

Cheap sealed lead acid batteries from unrecognised manufacturers often do not achieve their advertised capacity. Source AGM batteries from established manufacturers (Victron, Platinum, Banner). The rated capacity of a budget battery may be measured at a very slow discharge rate (C20) — actual usable capacity at typical van loads (C10 or faster) will be lower.
