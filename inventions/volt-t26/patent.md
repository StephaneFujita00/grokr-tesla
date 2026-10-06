# Horn Ground Continuity Monitor with Redundant Crimp Retention

## Abstract
A steering wheel horn ground assembly incorporates a secondary retention clip and an integrated continuity sensor that monitors ring terminal torque and contact resistance. The system detects impending open circuits before horn failure and logs data for service. Dimensions and sensor thresholds are specified to prevent circuit opening due to improper ring terminal seating.

## Problem
The ring terminal of the horn ground wire may be improperly secured during steering wheel assembly. Vibration loosens the terminal, opening the ground circuit and disabling the horn. Replacement of the entire steering wheel is required. No in-service detection exists.

## Prior art
- US5333900A, Airbag cover retainer with wire retention feature and ground: Integrates wire retention but provides no continuity monitoring or redundant crimp.
- US10562448B2, Steering wheel horn assembly: Uses annular circuit board for horn contacts but lacks ground terminal retention or sensor.

## Summary of the invention
The invention adds a spring steel retention clip (12) over the ring terminal (14) on the steering wheel armature (16) and a Hall-effect current sensor (18) in the horn control module (20) that verifies ground path continuity each ignition cycle. If resistance exceeds 50 milliohms or current falls below 4 A during a 100 ms test pulse, a warning is issued via the vehicle bus.

## Claims
1. A horn ground assembly comprising a ring terminal (14) crimped to a ground wire, a spring steel retention clip (12) with 8 N preload force engaging the terminal and armature (16), and a current sensor (18) measuring continuity through the ground path.
2. The assembly of claim 1 wherein the retention clip (12) includes a detent (22) that engages a notch (24) on the ring terminal (14) with 0.5 mm tolerance.
3. The assembly of claim 1 wherein the current sensor (18) applies a 5 V, 100 ms test pulse every ignition cycle and compares measured current against a 4 A threshold.
4. The assembly of claim 1 further comprising a non-volatile memory (26) in the horn module (20) that stores fault counts and resistance values for retrieval during service.
5. The assembly of claim 3 wherein the sensor (18) is calibrated to detect contact resistance increase above 50 milliohms before the circuit opens.
6. The assembly of claim 1 wherein the clip (12) is formed from 1.2 mm thick 301 stainless steel with a 15 mm engagement length.

## Brief description of the drawings
FIG. 1 shows the retention clip and ring terminal installed on the steering wheel armature with sensor leads.
FIG. 2 shows the horn control module schematic including the continuity test circuit.

## Detailed description
The steering wheel armature (16) is aluminum alloy 6061-T6 with a machined boss of 12 mm diameter. The horn ground wire is 14 AWG with a tin-plated copper ring terminal (14) having 6.5 mm inner diameter and 1.5 mm thickness. The terminal is secured by an M6 bolt torqued to 5 Nm. The spring steel retention clip (12) of 1.2 mm 301 stainless steel is placed over the terminal and snaps into a 2 mm deep groove on the armature boss. The clip applies 8 N preload and includes a 0.8 mm high detent (22) that seats in a matching notch (24) on the ring terminal edge with 0.5 mm positional tolerance. 

A Hall-effect current sensor (18) is mounted on the horn control module PCB (20). At each ignition-on event the module issues a 5 V, 100 ms pulse through the horn relay driver while monitoring return current. Normal current is 6-8 A. If current drops below 4 A or calculated resistance exceeds 50 milliohms the module sets DTC B1A23 and illuminates the instrument cluster warning. The module stores up to 50 fault events including timestamp and resistance value in non-volatile memory (26). The clip prevents terminal rotation under 50 Hz vibration at 3 g amplitude. If the primary crimp loosens, the detent maintains electrical contact until service intervention. The sensor detects the resistance rise before total open circuit occurs, allowing proactive repair without steering wheel replacement. All dimensions are nominal with ±0.2 mm tolerance unless noted. The test pulse is limited to 100 ms to avoid audible horn activation. Failure mode of clip fatigue is mitigated by the 301 stainless yield strength of 275 MPa. Sensor drift is compensated by periodic self-calibration against a known 10 milliohm reference resistor inside the module.