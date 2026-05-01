# Appliance Selection

Use when building the appliance inventory for the load calculation. The fridge is typically the decision with the largest impact on system sizing — establish it first.

---

## Fridges

The fridge is typically the highest-continuous-draw appliance in a van build (~35–45W running, ~24h/day). Getting this decision wrong has knock-on effects on battery bank and solar sizing.

**Do not use a household fridge**: household fridges are not designed for the temperature swings, movement, and orientation changes of van life. They consume significantly more power (average household fridge ~1,000Wh/day vs ~500Wh/day for a 12V compressor fridge). They are also much heavier and harder to fix to the van structure securely.

| Type | Voltage | Cost range | Notes |
|---|---|---|---|
| Electric coolbox (thermoelectric) | 12V | £50–£80 | Cools to ~20°C below ambient — not a true fridge. Won't reach safe food storage temperature in warm weather. Cheap but limited. |
| 12V compressor fridge | 12V | £200–£1,500 | True refrigeration. Low power draw. Self-contained. **Recommended for most builds.** e.g. Dometic CRX50 |
| 3-way fridge (absorption) | 12V or LPG | £400–£2,000 | Can run on gas — useful for extended off-grid without solar. Relies on ambient air circulation; less effective in hot weather. Noisier. More complex installation. e.g. Dometic RM5310 |

For most builds: specify a 12V compressor fridge. The 3-way option is worth considering only if extended off-grid use in cold climates without solar is a real use case.

**Impact on system sizing**: the fridge must be included in the load calculation from the start — it is not an afterthought. A 45W fridge running 24h = 1,080Wh/day = 90Ah/day at 12V. This alone often drives the minimum battery bank size.
