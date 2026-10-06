# Contactor Weld Detection and Redundant Isolation System for Battery Packs

## Abstract
A system monitors battery pack contactors for weld or failure conditions using voltage differential sensing across contacts and current decay timing. Upon detection, the system isolates the pack via a secondary solid-state relay and signals the vehicle controller to limit power. The invention prevents loss of drive power by early intervention before complete failure.

## Problem
Battery pack contactors in Model 3 and Model Y vehicles can weld closed or fail to open, resulting in inability to disconnect the high-voltage battery from the propulsion system. This leads to sudden loss of drive power. Existing contactors lack real-time weld detection integrated with redundant isolation.

## Prior art
- US8618775B2 Detection of over-current shorts in a battery pack using pattern recognition: monitors cell voltages for shorts but does not detect contactor weld states or provide redundant isolation.
- EP2181481B1 Mitigation of propagation of thermal runaway in a multi-cell battery pack: focuses on thermal events after failure rather than preventing drive power loss from contactor issues.
- US8862414B2 Detection of high voltage electrolysis of coolant in a battery pack: addresses coolant electrolysis but not mechanical contactor failure modes.

## Summary of the invention
The invention adds voltage sensors across each contactor pole and a controller that measures voltage drop during commanded open states. A secondary solid-state switch in parallel with the main contactor provides isolation if weld is detected. Current sensors confirm decay within 50 ms.

## Claims
1. A battery pack contactor monitoring system comprising: a main contactor (10) with voltage sensor (12) connected across its poles; a controller (14) configured to command open and compare sensed voltage differential to a threshold of 2 volts within 10 milliseconds; and a solid-state relay (16) activated upon detection of weld condition to isolate the battery pack.
2. The system of claim 1 wherein the controller measures current decay time after open command and declares failure if decay exceeds 50 milliseconds.
3. The system of claim 1 further comprising a redundant voltage sensor (18) on the load side with cross-check logic in the controller.
4. The system of claim 1 wherein the solid-state relay is rated for 400 amperes continuous and activates within 5 milliseconds of detection.
5. The system of claim 2 wherein failure declaration triggers a vehicle controller message limiting propulsion torque to 20 percent.
6. The system of claim 1 wherein the voltage sensors have tolerance of plus or minus 0.1 volts and sample at 1 kHz.

## Brief description of the drawings
FIG. 1 shows the contactor assembly with sensors and redundant path in side view.
FIG. 2 shows the control logic schematic with timing diagram.

## Detailed description
The main contactor (10) is a 400 ampere rated mechanical relay with silver alloy contacts. Voltage sensor (12) is a differential amplifier with 0.1 volt tolerance connected directly across the contact poles. Controller (14) is a microcontroller sampling at 1 kHz. Upon open command, it checks if voltage differential remains below 2 volts after 10 milliseconds, indicating weld. Current sensor (20) measures pack output current. If current does not decay below 5 amperes within 50 milliseconds, failure is declared. Solid-state relay (16) is a MOSFET-based switch rated 400 amperes, 800 volts, placed in series on the positive rail, activated within 5 milliseconds. Redundant voltage sensor (18) on the inverter side provides cross-check. On failure, controller (14) sends CAN message to vehicle ECU to limit torque to 20 percent and illuminate warning. Failure modes addressed include contact welding from high inrush, mechanical fatigue, and sensor drift handled by periodic self-calibration against known pack voltage. All dimensions match standard 400 volt pack architecture with 2 millimeter air gaps for isolation.