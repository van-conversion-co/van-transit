# Solar Panel Selection and Wiring

Use when solar panels are in scope. Panel type must be confirmed before the Architect finalises the roof layout.

---

## Panel types

**Rigid solar panels**

Monocrystalline or polycrystalline cells in an aluminium frame with a protective glass face. Mounted on brackets with a gap between the panel and the roof.

Pros: efficient, durable, long lifespan (20–25 years), easy to source and install, the gap under the panel acts as a heat sink which prolongs panel life.

Cons: heavy, visible from the ground (relevant for stealth camping), harder to install on curved or unusual roofs.

**Flexible solar panels**

Thin, bendable panels — glued or taped directly to the roof surface, or stored inside the van.

Pros: lightweight, low profile (nearly invisible from ground level — good for stealth), can conform to a gently curved roof, easy to relocate.

Cons: less efficient than rigid, shorter lifespan (5–15 years vs 20–25 for rigid), typically shorter warranty, generate more heat against the roof surface which degrades them faster, generally not suitable as primary charging on a full-time build.

**Recommendation**: use rigid panels for any build where solar is the primary charging source. Flexible panels are a reasonable choice only when the roof is too curved for rigid mounting, or stealth is an explicit use-case priority. If the owner is considering flexible panels as primary charging on a full-time build, flag the shorter lifespan and lower efficiency before confirming.

If rigid panels are chosen: flag to the Architect to confirm no conflict with roof rack, roof fan, or cable entry gland positions. Multiple roof penetrations should share a single cable entry housing to minimise leak risk.

---

## Series vs parallel panel wiring

When the owner has more than one solar panel, they must be wired either in series or in parallel. **Do not mix panel sizes** — if panels of different ratings are wired together, the output of the whole array is limited to the smallest panel's rating. Always spec the same panel model throughout an array.

**Parallel wiring**: panels are connected positive-to-positive, negative-to-negative. Voltage stays the same as a single panel; current (amps) adds up.
- Use when: limited cloud cover, partial shade is unlikely, or when the array voltage is already sufficient to charge the batteries
- The advantage: if one panel is shaded or faulty, the others continue to contribute
- Requires heavier cable to carry the higher current

**Series wiring**: panels are connected positive of one to negative of the next. Current stays the same as a single panel; voltage adds up.
- Use when: the climate has variable cloud cover or limited sun (UK default) — higher voltage allows the controller to extract more power in poor light conditions
- Allows thinner cable runs (lower current)
- Weakness: if one panel is shaded or damaged, the entire series string's output drops

**UK default**: series wiring is generally preferred for UK and northern European climates where cloud and partial shade are common. Series gives the array a higher open-circuit voltage, which keeps the charge controller working in poor light when parallel arrays may fall below the minimum charging threshold.

**Important constraint**: in series, the combined open-circuit voltage of the array must stay within the MPPT charge controller's maximum input voltage rating. Check the controller spec before adding panels in series.

Example: 3 × 100W panels wired in series.
- Voltage: 22V × 3 = 66V (check controller max input)
- Current: 6A × 1.25 (safety factor) = 7.5A
- Need an MPPT rated for at least 7.5A continuous and 66V+ input

---

## Charge controllers: PWM vs MPPT

A charge controller regulates the power from solar panels to the battery bank, preventing overcharge.

**PWM (Pulse Width Modulation)**: acts as a simple switch between panel and battery. Cheap. Effectively wastes any panel voltage above the battery voltage — a 22V panel charging a 12V battery through a PWM controller loses roughly 45% of potential output. Suitable only as a trickle/backup controller on very small systems where cost is paramount.

**MPPT (Maximum Power Point Tracking)**: continuously adjusts the electrical operating point of the array to extract the maximum available power regardless of battery state. Converts the excess voltage to additional current. Typically 25–30% more efficient than PWM in real conditions, and the difference is even larger in partial shade or cold weather. **Recommended for all primary solar systems.**

When specifying an MPPT controller:
- Input voltage rating must exceed the array's open-circuit voltage (add 25% safety margin)
- Current rating must cover the array's short-circuit current (add 25% safety margin)
- Verify compatibility with the battery chemistry — gel batteries require a specific charge profile; confirm the controller supports it
