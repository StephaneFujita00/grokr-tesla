# Firmware-based stress monitoring and mitigation for electronic power steering PCB

## Abstract
A firmware method detects impending PCB overstress in electronic power steering assist by monitoring torque command deltas and vehicle speed transitions. Upon detecting a stop-to-acceleration sequence exceeding calibrated thresholds, the firmware temporarily reduces assist gain by 15 percent for 800 ms while logging sensor data, preventing overstress without hardware changes.

## Problem
The printed circuit board in the electronic power steering assist experiences mechanical overstress when assist torque commands change rapidly during vehicle stop followed by acceleration. This leads to loss of power steering assist, requiring increased driver effort at low speeds.

## Prior art
- CN113227804B Enhanced in-system test coverage based on detecting component degradation: uses predictive testing for hardware degradation; this invention differs by applying real-time firmware torque limiting during specific vehicle maneuvers rather than offline testing.
- US10046802B2 Driving assistance control apparatus for vehicle: determines steering assist torque from deviation; this invention differs by adding speed-transition detection and temporary gain reduction to protect the PCB.

## Summary of the invention
The invention provides a firmware module in the steering ECU that monitors vehicle speed and torque request rate. When a stop-to-acceleration event is identified, assist current is limited to reduce PCB stress while maintaining safe steering.

## Claims
1. A method in a steering electronic control unit comprising: continuously sampling vehicle speed at 10 ms intervals and steering torque command at 1 ms intervals; detecting a stop-to-acceleration sequence when speed drops below 2 km/h for at least 500 ms followed by speed increase above 5 km/h within 2 s; upon detection, reducing steering assist gain to 85 percent of nominal for 800 ms; and restoring full gain after the interval unless a new sequence is detected.
2. The method of claim 1 further comprising storing the torque command delta, speed values and timestamp in non-volatile memory for the detected sequence.
3. The method of claim 1 wherein the gain reduction is applied only when the absolute value of the torque command exceeds 15 Nm.
4. The method of claim 1 wherein the firmware aborts the reduction if vehicle speed exceeds 30 km/h during the 800 ms interval.
5. The method of claim 1 further comprising incrementing a counter in EEPROM each time the mitigation activates and triggering a diagnostic trouble code after 50 activations.
6. The method of claim 1 wherein sampling continues during the reduced-gain interval to allow immediate re-trigger if a second sequence occurs within 3 s.

## Brief description of the drawings
FIG. 1 shows the steering ECU firmware flow and sensor inputs with reference numerals.
FIG. 2 shows timing diagram of speed, torque and gain signals during a mitigated event.

## Detailed description
The steering electronic control unit (10) receives vehicle speed signal (12) from the vehicle bus at 10 ms intervals and steering torque command (14) from the torque sensor at 1 ms intervals. A detection module (16) compares speed (12) against threshold T1 equal to 2 km/h. When speed remains below T1 for duration D1 of 500 ms, a stop flag (18) is set. Upon subsequent speed rise above T2 equal to 5 km/h within window W of 2 s, an acceleration event (20) is declared. If absolute torque command (14) exceeds T3 equal to 15 Nm, a mitigation timer (22) starts for duration D2 of 800 ms. During this interval the assist gain multiplier (24) is set to 0.85. The current command sent to the motor driver (26) is scaled accordingly. After D2 expires the multiplier returns to 1.0 unless a new event is detected. All parameters including torque delta, speed values and activation count are written to non-volatile memory (28). If activations reach 50 a diagnostic trouble code is set. The firmware continues sampling during mitigation to allow immediate re-application if another sequence occurs within 3 s. Failure mode of rapid repeated events is handled by the 3 s re-trigger window and EEPROM counter. The method uses existing sensors and requires no additional hardware. All dimensions and times stated above are implemented exactly in the firmware constants.