## Stage 1: Non-Ideal Open-Loop Buck Simulation (05/23/2026)

A simplified asynchronous buck converter was simulated at Vin = 12 V, target Vout = 3 V, and load current near 3 A. Initial ideal-duty operation produced output voltage below the 3 V target once diode drop, switch resistance, and passive losses were included. Increasing duty cycle restored the output closer to the desired operating point.

This confirms the role of feedback in the LM2596 module: the regulator must adjust duty cycle to compensate for nonideal losses and maintain output regulation.

# Refined LM2596-ADJ Module Simulation (05/23/2026)

## Objective

This simulation refines the earlier buck converter model by incorporating visible component values from the physical LM2596 adjustable buck converter module. The goal is to create a closer behavioral model of the actual board before taking bench measurements.

---

## Physical Board Details Used

The physical module appears to use:

| Component | Board Marking | Interpreted Value / Function |
|------------|--------------|------------------------------|
| LM2596S-ADJ | LM2596S-ADJ | Adjustable buck regulator |
| Potentiometer | W103 | 10 kΩ potentiometer |
| Inductor | 470 | Likely 47 µH |
| Input Capacitor | 100 µF / 50 V | Input filtering |
| Output Capacitor | 220 µF / 35 V | Output filtering |
| SMD Resistor | 271 | 270 Ω |
| SMD Resistor | 752 | 7.5 kΩ |
| Tan Unmarked Component | No marking | Likely ceramic capacitor |
| Diode | 1N582x family | Schottky freewheel diode |

These values are preliminary and will be verified through continuity mapping and resistance measurements on the physical board.

---

## Simulation Conditions

| Parameter | Value |
|------------|--------|
| Input Voltage | 12 V |
| Target Output Region | Approximately 3 V |
| Load Current Target | 3 A |
| Load Resistance | 1 Ω |
| Inductor | 47 µH |
| Output Capacitor | 220 µF |
| Input Capacitor | 100 µF |
| Schottky Model | 1N582x family model |
| Regulator Model | LM2596 adjustable behavioral model |

---

## Feedback Network Estimate

The adjustable LM2596 regulates its feedback pin to approximately:

```text
VFB ≈ 1.23 V
```

The reconstructed feedback network uses a 10 kΩ upper feedback resistance and a 7.5 kΩ lower feedback resistance.

The expected output voltage is:

\[
V_{OUT} = 1.23 \left(1 + \frac{R_{TOP}}{R_{BOTTOM}}\right)
\]

Using:

```text
RTOP = 10 kΩ
RBOTTOM = 7.5 kΩ
```

gives:

\[
V_{OUT}
=
1.23\left(1+\frac{10k}{7.5k}\right)
=
2.87V
\]

This matches the simulated output average closely.

---

## Simulated Waveform Results

The refined simulation produced the following approximate steady-state behavior:

| Quantity | Simulated Behavior |
|------------|--------------------|
| Switch Node Voltage | Pulses between approximately 0 V and 12 V |
| Inductor Current | Triangular ripple, roughly 1 A to 4.5 A |
| Average Inductor Current | Approximately 2.7 A to 3 A |
| Output Voltage | Approximately 2.8 V to 3.0 V |
| Average Output Voltage | Approximately 2.87 V |
| Feedback Voltage | Centered near 1.23 V |

---

## Waveform Interpretation

### Switch Node Voltage

The switch node exhibits the expected behavior of an asynchronous buck converter. The waveform alternates between approximately 12 V when the internal switch is conducting and approximately 0 V during the freewheeling interval through the Schottky diode.

Small corrective switching pulses are observed between the primary switching events. These pulses are interpreted as normal control-loop activity rather than random noise.

### Inductor Current

The inductor current exhibits the expected triangular waveform associated with buck converter operation.

The current varies approximately between:

```text
1 A and 4.5 A
```

with an average value near:

```text
3 A
```

This indicates that the converter is supplying the intended load current while maintaining regulation.

The relatively large current ripple is expected due to:

- Low output voltage (~3 V)
- High output current (~3 A)
- 47 µH inductance
- 150 kHz switching frequency

### Output Voltage

The output voltage settles near:

```text
2.87 V
```

which agrees closely with the value predicted from the estimated feedback divider.

A small periodic ripple is present at the output, corresponding to the charging and discharging behavior of the output capacitor during each switching cycle.

### Feedback Voltage

The feedback voltage stabilizes around:

```text
VFB ≈ 1.23 V
```

which is the expected reference voltage for the LM2596 adjustable regulator.

This is the strongest indication that the converter is regulating correctly.

---

## Correlation Between Feedback Divider and Output Voltage

The simulated output voltage closely matches the value predicted by the estimated feedback network:

\[
V_{OUT}
=
1.23\left(1+\frac{10k}{7.5k}\right)
=
2.87V
\]

The agreement between theory and simulation suggests that the estimated resistor values are plausible representations of the actual module's feedback network.

---

## Preliminary Conclusions

The refined LM2596-ADJ simulation produces behavior consistent with the expected operation of the physical module.

Key observations include:

- The feedback node regulates near the expected 1.23 V reference.
- The output voltage settles near the value predicted by the estimated feedback divider.
- The switch node exhibits normal buck converter switching behavior.
- The inductor current supports an average load current near 3 A.
- The simulated output voltage aligns closely with analytical calculations.

At this stage, the simulation should be considered a preliminary reconstruction of the physical converter. Further confidence in the model will be obtained through continuity mapping and resistance measurements of the actual hardware.

---

## Future Validation Activities

The following measurements will be performed on the physical LM2596 module:

1. Identify the exact feedback network connections through continuity testing.
2. Measure potentiometer resistance range and wiper connections.
3. Verify resistor values and their locations within the feedback network.
4. Determine the role of the unmarked ceramic capacitor.
5. Compare measured output voltage against simulated output voltage.
6. Compare measured switch-node waveforms against simulation results.
7. Estimate inductor current ripple and compare against simulation predictions.

These measurements will be used to produce a final hardware-correlated LM2596 model.
