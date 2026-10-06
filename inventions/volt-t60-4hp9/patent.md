# Firmware-based Taillight Continuity Monitor with Redundant PWM Verification

## Abstract
A firmware module in the body control unit monitors PWM drive signals to taillight LEDs at 10 ms intervals. It compares commanded duty cycle against measured current draw and voltage feedback. On mismatch exceeding 8 percent for more than 200 ms, the module switches to a redundant output channel or logs a persistent fault for service.

## Problem
Intermittent taillight illumination occurs when the LED driver IC or its PWM output path experiences transient faults not caught by existing hardware self-tests. The software update must detect these conditions in real time and maintain illumination without requiring physical replacement of the lighting assembly.

## Prior art
No patents returned by searches; none cited.

## Summary of the invention
The invention adds a continuous verification loop inside the existing taillight driver firmware. Two independent timers and two ADC channels sample current and voltage on the output MOSFET. A state machine declares a fault only after three consecutive samples exceed tolerance, then activates a parallel MOSFET path rated for the same 1.2 A load.

## Claims
1. A method for monitoring a vehicle taillight comprising: commanding a PWM signal at a selected duty cycle D to a first MOSFET (12); sampling output current I and voltage V at intervals of 10 ms; computing expected current from D and known LED forward voltage; declaring a fault when absolute value of (I_measured - I_expected) exceeds 8 percent of I_expected for three consecutive samples; and activating a second MOSFET (14) connected in parallel to the first MOSFET upon fault declaration.
2. The method of claim 1 wherein the sampling interval is between 5 ms and 20 ms.
3. The method of claim 1 wherein the fault threshold is between 5 percent and 12 percent deviation.
4. The method of claim 1 further comprising storing a diagnostic trouble code with timestamp after five consecutive fault declarations.
5. The method of claim 1 wherein the second MOSFET remains active until ignition cycle reset and a manual service clear command.
6. The method of claim 1 wherein both MOSFETs are driven by independent timer peripherals in the microcontroller.

## Brief description of the drawings
FIG. 1 shows the taillight driver circuit with primary and redundant MOSFET paths and ADC feedback lines.

## Detailed description
The body control module microcontroller (10) executes the taillight firmware at 100 Hz. A first timer peripheral generates the primary PWM waveform applied to gate of MOSFET (12) whose drain connects to the positive supply through a 0.05 ohm sense resistor (16). Source of MOSFET (12) drives the anode bus of the taillight LED string (18). A second identical MOSFET (14) is wired in parallel with MOSFET (12) but remains off during normal operation. Two ADC channels (20, 22) sample voltage across sense resistor (16) and voltage at the LED anode bus every 10 ms. Firmware computes expected current as I_expected = D * (V_supply - Vf_LED) / R_series where D is the commanded duty cycle between 0.1 and 1.0, Vf_LED is stored as 3.1 V per LED for six LEDs, and R_series is 2.2 ohms. If the absolute difference between measured current and I_expected exceeds 8 percent of I_expected for three successive 10 ms samples, the state machine sets a flag and enables the gate drive to MOSFET (14). Both MOSFETs are rated 40 V, 2 A continuous. The redundant path remains active until the next ignition-off event and receipt of a service tool clear command. A persistent counter increments on each fault declaration; after five counts a DTC U1A23 is stored with 32-bit timestamp. Failure modes addressed include MOSFET gate oxide degradation causing partial conduction, solder joint micro-cracks on the driver board producing intermittent contact, and LED string open-circuit events that produce zero current despite commanded PWM. The dual-timer architecture ensures that a single timer peripheral fault cannot disable both paths. All tolerance values (8 percent, 200 ms, 10 ms) are stored in non-volatile calibration memory and are identical to those used in the OTA update calibration table.