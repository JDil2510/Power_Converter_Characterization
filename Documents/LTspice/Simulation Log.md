## Stage 1: Non-Ideal Open-Loop Buck Simulation

A simplified asynchronous buck converter was simulated at Vin = 12 V, target Vout = 3 V, and load current near 3 A. Initial ideal-duty operation produced output voltage below the 3 V target once diode drop, switch resistance, and passive losses were included. Increasing duty cycle restored the output closer to the desired operating point.

This confirms the role of feedback in the LM2596 module: the regulator must adjust duty cycle to compensate for nonideal losses and maintain output regulation.
