# Water Heating Options

Use when deciding the hot water method. This decision must be made before sizing any other plumbing component — the choice affects electrical load (Electrician), heating system integration (Mechanic), and plumbing layout.

---

## Options

| Option | Approx cost | Heat-up time | Notes |
|---|---|---|---|
| Gas boiler (standalone) | ~£400 | ~30 min | LPG; needs external flue; built-in hot water tank |
| Combi boiler (e.g. Truma Combi 4) | ~£1,250 | 20–45 min | LPG; provides space heating + hot water from one unit; expensive and complex to install; professional install recommended |
| Calorifier (e.g. Propex Malaga) | £200–400 | ~1 hr/tank | Uses engine coolant loop — free heat when driving; no flue; Mechanic installs coolant tap; Plumber routes water circuit |
| Tankless LPG (e.g. Camplux) | £150–250 | Instant | Good all-rounder for most builds; no tank to wait for |
| Solar shower | £5–40 | 3–6 hrs (sun) | Outdoor/fair-weather only; no installation |
| 12V inline heater | Varies | Fast | Dedicated 12V circuit; Electrician sizes |
| 240V immersion | Varies | Fast | Shore power only; Electrician designs circuit first |

---

## Critical notes per option

**Gas boiler**: built-in hot water tank is typically only 10–13 litres — one shower will likely empty it; allow reheat time before the next use. Flue exits through the roof or van side depending on the model — this is not a free choice; confirm flue routing with Architect before specifying a boiler model. Log as `blocks_worker: Architect`.

**Calorifier**: only heats water while the engine is running. If the owner is stationary for multiple days without driving, there is no hot water. This is a critical limitation for owners who camp off-grid for extended periods without moving — must be flagged explicitly when presenting this option.

**Tankless LPG**: uses LPG combustion and produces CO — must be well ventilated when in use. Windows or doors must be open. Using in a sealed van is dangerous. Note this in the commissioning plan.

**Combi boiler**: expensive and complex; requires external flue. Log as `blocks_worker: Architect`.

---

## Guidance on method selection

- For most builds: **tankless LPG** is the best value mid-range option — instant hot water, moderate cost, no complex integration. Ensure ventilation is addressed.
- For builds with a diesel heater: **calorifier** is worth considering — effectively free hot water while driving — but only viable if the owner drives regularly. Not suitable for extended stationary use.
- For a luxury build with space heating needs: **Truma Combi** covers both, but budget and installation complexity are significant.
- Solar shower is only appropriate as a supplement — not a primary hot water source.

Log the water heating choice as a Decisions.md entry with `blocks_worker` matching whichever other worker is affected (Mechanic for calorifier; Electrician for 12V or 240V options; Mechanic for LPG gas routing).
