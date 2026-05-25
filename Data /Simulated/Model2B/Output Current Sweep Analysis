# Model 2b (SS3P5) Load Current Sweep

![Model 2b LTspice Schematic](Model2bLTspice.png)

## Objective

The purpose of this simulation was to evaluate the performance of the Stage 2b LM2596 converter model over a range of load currents while using an SS3P5 Schottky diode as a substitute for the SS34 diode installed on the physical converter module.

The load current was swept from 0.25 A to 3.0 A while maintaining:

- Input Voltage: 12 V
- Target Output Voltage: 3 V
- Inductor: 47 µH
- Output Capacitor: 220 µF
- Feedback Divider: 10 kΩ / 7.5 kΩ
- Schottky Diode: SS3P5

Steady-state measurements were collected between 1.5 ms and 2.0 ms to eliminate startup transients.

---

## Results Summary

The converter maintained regulation throughout the entire load-current sweep, with average output voltage remaining between approximately:

$$
2.89V \leq V_{OUT} \leq 2.95V
$$

Despite the simplified diode substitution and limitations of the LM2596 macromodel, the converter remained within approximately ±2% of the target 3 V output.

Inductor current increased with load current as expected, while output voltage ripple generally increased as the converter approached the boundary between discontinuous and continuous conduction modes.

---

## Conduction Mode Behavior

Analysis of the minimum inductor current indicates that the converter operates primarily in Discontinuous Conduction Mode (DCM) at lighter loads.

For load currents between:

$$
0.25A \leq I_{OUT} \leq 2.25A
$$

the minimum inductor current remains approximately zero, indicating that the inductor fully discharges before the beginning of the next switching cycle.

As load current increases beyond approximately 2.5 A, the minimum inductor current becomes positive:

| Iout (A) | IL(Min) (A) |
|-----------|-----------:|
| 2.50 | 0.121 |
| 2.75 | 0.434 |
| 3.00 | 0.972 |

This behavior indicates a transition into Continuous Conduction Mode (CCM), where the inductor current never reaches zero during a switching cycle.

---

## Output Voltage Ripple

The simulated output ripple ranged from approximately:

$$
102mV \leq V_{RIPPLE} \leq 304mV
$$

The largest ripple was observed near the DCM-to-CCM transition region, suggesting that converter operation becomes most dynamic as the conduction mode changes.

This behavior is consistent with the large variations in inductor ripple current observed throughout the sweep.

---

## Efficiency

The simulation predicted efficiencies ranging from approximately:

$$
73.9\% \leq \eta \leq 91.9\%
$$

The highest efficiencies were observed at lighter load currents, while the lowest efficiency occurred at the 3 A operating point:

| Iout (A) | Efficiency (%) |
|-----------|--------------:|
| 0.25 | 91.0 |
| 0.50 | 91.9 |
| 1.00 | 85.6 |
| 2.00 | 80.3 |
| 3.00 | 73.9 |

The efficiency value at 3 A is notable because it is close to the approximately 73% efficiency reported in the LM2596 datasheet for comparable operating conditions.

Because the model uses an SS3P5 diode rather than the physical SS34 diode, these results should be interpreted as preliminary estimates rather than final performance predictions.

---

## Key Observations

- Output voltage remained near the desired 3 V target throughout the sweep.
- The converter operated primarily in DCM at lower load currents.
- A transition to CCM occurred near 2.5 A load current.
- Output ripple increased near the conduction-mode transition region.
- Simulated efficiency at 3 A was approximately 74%.
- Results provide a baseline dataset for future comparison against an SS34-based model and eventual hardware measurements.

---

## Future Work

Future refinement of the model will focus on replacing the SS3P5 diode with an SS34-specific SPICE model and repeating the load-current sweep. Comparison of the two datasets will quantify the impact of diode selection on converter regulation, ripple performance, and efficiency.
