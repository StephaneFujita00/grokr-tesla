# Subframe Lateral Link Fastener Verification System

## Abstract
A manufacturing verification system for front suspension lateral link fasteners on a vehicle subframe uses integrated torque-angle sensors and a controller to confirm proper attachment before the vehicle leaves the assembly line. The system prevents loose fasteners by enforcing a two-stage fastening sequence with real-time monitoring and automatic rejection of non-compliant assemblies.

## Problem
During subframe assembly, lateral link fasteners may receive insufficient torque or improper angle rotation due to operator error or tool variation. A loose fastener permits separation of the lateral link from the subframe under load, resulting in loss of vehicle stability.

## Prior art
- No relevant patents found in searches for Tesla Model Y suspension fastener torque monitoring or vehicle subframe lateral link fastener detection.

## Summary of the invention
The invention adds a strain-gauge torque sensor (12) and rotary encoder (14) to the fastening tool head. A controller (20) records torque versus angle data during the final 90-degree rotation phase after initial seating torque of 80 Nm is reached. The controller compares the recorded curve against a stored reference band and signals acceptance only when peak torque lies between 105 Nm and 115 Nm with angle between 85 and 95 degrees. Non-conforming fasteners trigger a station lockout and data log entry.

## Claims
1. A fastener verification apparatus comprising a torque sensor (12) mounted on a fastening tool, a rotary encoder (14) coupled to the tool drive, and a controller (20) configured to record torque-angle data during a final rotation phase after a seating torque of 80 Nm and to accept the fastener only when measured peak torque is between 105 Nm and 115 Nm and final angle is between 85 and 95 degrees.
2. The apparatus of claim 1 wherein the controller (20) stores the reference torque-angle band in non-volatile memory and compares each fastening cycle against upper and lower limit curves.
3. The apparatus of claim 1 further comprising an optical indicator (24) that illuminates green only upon acceptance and red upon rejection.
4. The apparatus of claim 1 wherein the controller (20) logs each fastening event with timestamp, torque curve, and vehicle identification number.
5. The apparatus of claim 1 wherein rejection by the controller (20) activates a station interlock preventing advancement of the subframe to the next assembly station.
6. The apparatus of claim 1 wherein the torque sensor (12) is a strain-gauge bridge calibrated to 0.5 percent accuracy over the range 0 Nm to 200 Nm.

## Brief description of the drawings
FIG. 1 shows the fastening tool head engaged with a lateral link fastener on the subframe.

## Detailed description
The subframe (30) supports the front suspension lateral link (32) at mounting boss (34). Fastener (36) is a 14 mm diameter grade 10.9 bolt inserted through the link eye and into a threaded hole in boss (34). The fastening tool (40) carries torque sensor (12) on its output shaft and rotary encoder (14) on the motor housing. During operation the tool first applies torque until sensor (12) reads 80 Nm, seating the bolt head against the link. The controller (20) then commands continued rotation while monitoring both torque and angle. Acceptance occurs only when the torque rises to a value between 105 Nm and 115 Nm after an angle change of 85 to 95 degrees. If the curve exits the stored acceptance band the controller (20) asserts a reject signal, illuminates red indicator (24), and energizes interlock relay (26) that prevents conveyor movement. The logged data includes the full torque-angle array, timestamp, and VIN read from the subframe RFID tag (28). Calibration of sensor (12) is verified daily against a reference load cell accurate to 0.2 Nm. Failure modes addressed include under-torque from worn sockets, over-angle from stripped threads, and sensor drift; each is detected by the curve comparison and results in station lockout until manual override with supervisor authorization.