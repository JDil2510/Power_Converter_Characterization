## Steady-State Waveform Analysis

### Simulation Conditions

| Parameter | Value |
|------------|------------|
| Input Voltage | 12 V |
| Output Voltage Target | 3 V |
| Load Current Target | 3 A |
| Switching Frequency | 150 kHz |
| Inductor | 47 µH |
| Output Capacitor | 220 µF |
| Diode | 1N582x Schottky |
| Feedback Reference | 1.23 V |

### Figure X. Steady-State Converter Operation

![Steady-State Waveforms](Power_Converter_Characterization/Figures/zoomed_waveforms_stacked_subplots.png)

The figure shows the steady-state behavior of the reconstructed LM2596 adjustable buck converter model operating from a 12 V input supply while delivering approximately 3 A to the load. The displayed time window spans from 4.8 ms to 5.0 ms, well after startup transients have settled.

### Switching Node Voltage (VSW)

The switching node alternates between approximately -1 V and 12 V. The positive level corresponds to the LM2596 internal switch connecting the inductor to the input supply, while the negative excursion occurs when the freewheeling Schottky diode conducts during the off-state.

The periodic switching behavior indicates stable regulator operation with no evidence of pulse skipping, burst mode operation, or loss of regulation.

### Output Voltage (VOUT)

The output voltage remains regulated near 3.096 V with a small periodic ripple component synchronized to the switching frequency. The ripple magnitude is significantly smaller than the DC output level, indicating effective filtering by the output LC network.

The average output voltage closely matches the intended operating point established by the feedback network.

### Inductor Current (IL)

The inductor current exhibits the expected triangular waveform associated with continuous-conduction mode (CCM) operation. Current oscillates about the nominal 3 A load current while remaining strictly positive throughout the switching cycle.

The absence of zero-current intervals confirms that the converter remains in CCM under the specified loading conditions.

### Feedback Regulation Verification

Additional examination of the feedback node shows that the feedback voltage converges to approximately 1.23 V, matching the LM2596 internal reference voltage. This confirms that the feedback network is correctly regulating the output voltage.

### Observations

- Stable periodic switching behavior observed.
- Output voltage regulated near 3.1 V.
- Inductor current remains in continuous conduction mode.
- Feedback voltage converges to the expected 1.23 V reference.
- No evidence of instability or loss of regulation in steady state.

### Relevance to Future Hardware Testing

These waveforms establish expected converter behavior prior to laboratory measurements. Future oscilloscope captures of the switching node, output voltage, and inductor current can be compared directly against these results to assess model fidelity and identify hardware nonidealities such as capacitor ESR, PCB parasitics, and diode recovery effects.

