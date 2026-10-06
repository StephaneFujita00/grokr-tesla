# Automated In-Line Torque Verification System for Seat Frame Bolts

## Abstract
An automated system uses torque-angle sensors on robotic nut runners during seat frame assembly to measure and log each bolt's torque and angle in real time. Data is compared against thresholds of 35 plus or minus 2 Newton-meters and 30 to 45 degrees rotation. Deviations trigger immediate station halt and marking. The system stores serial-numbered records for traceability and integrates with vehicle assembly line controls.

## Problem
Bolts securing second-row seat back frames may not reach specified torque during manual or semi-automated installation. Loose bolts reduce seat belt anchorage strength and increase injury risk in crashes. Current post-assembly inspection relies on random sampling or service-center checks after vehicles leave the line.

## Prior art
- USRE47232E1 Assembly system for monitoring proper fastening of an article of assembly at multiple locations: uses sequential torque checks on fixed fixtures; this invention adds continuous angle measurement and real-time line integration for moving seat frames.
- US12005856B2 Electronic harness check system: monitors seat belt tension sensors after assembly; this invention verifies the critical frame bolts themselves at the fastening station.

## Summary of the invention
A robotic fastening station incorporates strain-gauge torque sensors and rotary encoders on each nut runner spindle. Controllers compare measured values to 35 Nm target with 2 Nm tolerance and 30-45 degree angle window. Out-of-spec bolts cause the seat carrier to stop, apply a visible ink mark, and log the event with timestamp and vehicle VIN.

## Claims
1. An automated bolt verification system comprising a robotic nut runner having a torque sensor and rotary encoder, a controller configured to compare measured torque to a target of 35 Nm plus or minus 2 Nm and rotation angle to 30-45 degrees, and means to halt the assembly line and record a fault when either parameter is outside tolerance.
2. The system of claim 1 wherein the controller stores torque-angle data linked to a unique seat frame serial number.
3. The system of claim 1 further comprising an ink marking device activated on fault detection.
4. The system of claim 1 wherein the nut runner operates at a spindle speed of 120 revolutions per minute during final tightening.
5. The system of claim 1 wherein the controller transmits fault data to a central manufacturing execution system within 200 milliseconds of detection.
6. A method of verifying seat frame bolt installation comprising applying torque while monitoring angle, comparing values to the tolerances stated in claim 1, and stopping the carrier if any bolt fails.

## Brief description of the drawings
FIG. 1 shows the robotic fastening station with nut runner, sensors, seat frame carrier, and marking unit in side view.

## Detailed description
The assembly station receives seat back frames on a moving carrier (12) traveling at 0.8 meters per minute. Nut runner (14) with spindle (16) engages M10 bolts (18) at four locations on each frame. Torque sensor (20) measures reaction torque via strain gauges calibrated to plus or minus 0.5 percent accuracy. Rotary encoder (22) on the spindle shaft records angular displacement from initial thread contact. Controller (24) samples both signals at 1 kHz. When torque reaches 35 Nm the angle must lie between 30 and 45 degrees; otherwise the carrier stops within 50 millimeters, marking device (26) applies a 5 millimeter diameter red ink dot at the bolt head, and data packet containing VIN, bolt position, torque value, angle value, and timestamp is sent to the manufacturing execution system. Failure modes addressed include under-torqued bolts from worn bits, stripped threads detected by excessive angle, and sensor drift corrected by automatic zeroing every 50 cycles. All reference numerals appear in FIG. 1.