# Software-based headlamp intensity calibration system for FMVSS 108 compliance

## Abstract
A firmware method and system that measures actual low-beam output via a forward camera and current sensor during a 30-second post-assembly or service calibration sequence, then applies a per-headlamp PWM duty-cycle offset stored in non-volatile memory to limit peak luminous intensity to 1500 cd at H-V while preserving beam pattern. The offset is recomputed every 5000 km or after voltage deviation exceeds 0.5 V.

## Problem
Certain 2017-2023 Model 3 and 2020-2023 Model Y headlamps exceed the FMVSS 108 maximum low-beam intensity of 1500 cd at the H-V point due to LED bin variation and reflector tolerance of ±8 %. Replacement of entire assemblies is required under recall 26V507000 because no factory calibration trims output after installation.

## Prior art
- EP4188754B1 Global headlamp (Tesla): describes matrix beam shaping but contains no closed-loop intensity measurement or PWM trimming for regulatory maximum output.
- US6429594B1 Continuously variable headlamp control (Gentex): uses imaging for glare reduction to oncoming traffic but does not enforce absolute photometric limits at H-V.

## Summary of the invention
The invention adds a one-time and periodic calibration routine executed by the body control module (BCM) that drives each low-beam LED string at stepped PWM values from 60 % to 100 % while the forward camera records lux at the H-V point and a shunt resistor measures LED current. The BCM solves for the PWM value that yields exactly 1500 cd, stores a signed 8-bit offset in EEPROM, and applies it on every ignition cycle. Failure modes such as camera obstruction or current sensor drift trigger a diagnostic trouble code and default to 85 % PWM.

## Claims
1. A method for limiting automotive headlamp low-beam intensity comprising: driving a headlamp LED driver with a base PWM value; measuring luminous intensity at the H-V point with a vehicle-mounted imaging sensor; computing a PWM offset that brings measured intensity to 1500 cd; storing the offset in non-volatile memory; and applying the offset on subsequent power cycles.
2. The method of claim 1 further comprising repeating the measurement and offset computation when odometer increment exceeds 5000 km or supply voltage deviates more than 0.5 V from nominal.
3. The method of claim 1 wherein the imaging sensor is the forward-facing camera already present for Autopilot and the measurement occurs with the vehicle stationary on level ground for at least 30 seconds.
4. The method of claim 1 wherein current through the LED string is measured simultaneously and the offset is rejected if current lies outside 2.8 A to 3.2 A at 13.5 V.
5. The method of claim 1 wherein a diagnostic trouble code is set and PWM is clamped at 85 % if the calibration sequence fails to converge within five attempts.
6. The method of claim 1 wherein the offset is applied independently to left and right headlamps.

## Brief description of the drawings
FIG. 1 shows the headlamp assembly, forward camera, BCM, and calibration signal flow with reference numerals.
FIG. 2 shows the PWM waveform, current-sense resistor placement, and camera field-of-view alignment to the H-V point.

## Detailed description
Headlamp assembly (10) contains low-beam LED string (12) driven by constant-current module (14) whose enable pin receives PWM signal (16) from body control module (BCM) (18). Forward camera (20) is mounted at the top center of the windshield and its optical axis (22) intersects the H-V point (24) at 25 m when the vehicle is on level pavement. During calibration the BCM (18) commands PWM from 60 % to 100 % in 2 % steps while camera (20) reports lux values through the vehicle CAN bus (26). A 0.01 Ω shunt resistor (28) in series with LED string (12) allows BCM (18) to read current via analog-to-digital converter input (30). The firmware solves the linear fit I = k·PWM + b and selects the PWM value that produces 1500 cd. The resulting signed offset, typically between −12 % and +4 %, is written to EEPROM location 0x3F8. On every key-on the BCM (18) adds the stored offset to the nominal 92 % PWM map value before outputting signal (16). If camera (20) reports obstruction or current lies outside the 2.8–3.2 A window at 13.5 V the routine aborts, sets DTC B12A3, and forces 85 % PWM. Recalibration is triggered automatically after 5000 km or when battery voltage deviates more than 0.5 V. All timing, current limits, and intensity targets match the values stated in the claims. The system prevents over-bright low beams without hardware replacement.