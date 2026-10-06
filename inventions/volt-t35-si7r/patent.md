# Seat Frame Fastener Torque Verification System

## Abstract
A system for verifying torque on seat back to seat bottom fasteners during vehicle assembly. Strain gauges mounted on the seat frame side members detect preload after torquing. A controller compares measured strain to a calibrated range of 1800-2200 microstrain corresponding to 45-55 Nm torque on M10 bolts. If out of range, the station halts and flags the unit. The system integrates with existing robotic torque tools and logs data to the vehicle ECU.

## Problem
Fasteners attaching the seat back frame to the seat bottom frame may receive incorrect torque during assembly. This leads to insufficient clamping force, allowing relative motion between frames under crash loads and potential failure to restrain the occupant.

## Prior art
- USRE47232E1 Assembly system for monitoring proper fastening of an article of assembly at multiple fastening locations: uses torque-angle signature on a general assembly line; this invention adds direct strain measurement on the seat side member after final torque for closed-loop verification specific to seat hinge joints.
- AU2021333394A1 Fasteners, fastener arrangements and tools for application and/or release of …: describes reaction portions on threaded fasteners for torque reaction; this invention retains standard bolts and instead measures frame deformation downstream of the joint.

## Summary of the invention
The invention mounts four strain gauges on the inner faces of the seat back side members 40 mm above the hinge bolts. Signals feed a local microcontroller that computes average preload strain. Threshold logic rejects assemblies outside the calibrated window and triggers a rework station alert. Calibration is performed once per shift using a master seat with known torque.

## Claims
1. A seat assembly verification apparatus comprising a seat back frame having left and right side members, at least two strain gauges bonded to each side member at a distance of 35-45 mm above the hinge bolt centerline, a microcontroller configured to read strain values after application of 45-55 Nm torque to M10 fasteners and to compare the values against a stored range of 1800-2200 microstrain, and an output signal that inhibits vehicle release when any gauge reading falls outside the range.
2. The apparatus of claim 1 wherein the strain gauges are semiconductor type with gauge factor 150 and are wired in a full Wheatstone bridge per side member.
3. The apparatus of claim 1 wherein the microcontroller stores the strain data together with the vehicle VIN in non-volatile memory accessible via the vehicle CAN bus.
4. The apparatus of claim 1 further comprising a temperature sensor mounted adjacent to the gauges, the microcontroller applying a temperature compensation coefficient of 0.3 microstrain per degree C between 10 C and 50 C.
5. The apparatus of claim 1 wherein the microcontroller is powered only during the final torque station cycle and enters sleep mode within 5 seconds after data transmission.
6. The apparatus of claim 1 wherein the side members are 2.0 mm thick high-strength steel and the gauges are located on the neutral axis of bending to minimize sensitivity to occupant load.

## Brief description of the drawings
FIG. 1 shows the seat frame assembly with strain gauge locations and wiring.
FIG. 2 shows the signal flow from gauges through the microcontroller to the assembly line controller.

## Detailed description
The seat back frame consists of two vertical side members (10) formed from 2.0 mm HSLA steel tube, joined at top and bottom by cross members. Each side member receives two M10 class 10.9 bolts (12) at the lower end that thread into weld nuts on the seat bottom frame (14). The design torque is 50 Nm plus or minus 5 Nm. Four semiconductor strain gauges (16) are bonded with epoxy 40 mm above the bolt centerline on the inner face of each side member. Gauge active length is 3 mm and they are oriented axially. Leads (18) route inside the frame to a microcontroller module (20) mounted on the rear cross member. The module contains a 24-bit ADC, temperature sensor (22), and CAN transceiver. After the robotic torque tool completes the final pass on all four bolts, the station controller sends a trigger signal over CAN. The microcontroller averages the four bridge outputs, applies the temperature correction, and checks whether the result lies between 1800 and 2200 microstrain. If within range the module transmits a pass code containing the measured values and VIN. If outside range it transmits a fail code and asserts a discrete output that lights a red lamp and locks the conveyor. The calibration procedure uses a master seat frame pre-torqued to 50 Nm on a calibrated bench; the resulting strain values are stored as limits. Failure modes addressed include under-torque (strain below 1800), over-torque causing thread damage (strain above 2200), and gauge drift, which is detected by periodic zero-load checks during station idle periods. All dimensions and limits stated above are repeated in the claims.