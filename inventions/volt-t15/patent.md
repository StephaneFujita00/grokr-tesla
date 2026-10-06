# Seat belt pretensioner anchor connection verification system

## Abstract
A manufacturing verification system for front-row seat belt pretensioner anchor connections in vehicles uses a force sensor (22) integrated into the anchor assembly (12) to measure connection force during assembly. A controller (28) compares the measured force against a threshold of 180 N and logs the result with a timestamp. If below threshold, an alert is issued and the assembly station is halted until corrected. The system prevents incomplete connections from reaching final assembly.

## Problem
During seat belt installation on the pretensioner anchor (14), the buckle tongue connector may seat incompletely due to misalignment or debris, resulting in a connection that detaches under load. Manual inspection after assembly is prone to human error and does not detect marginal connections that pass visual checks but fail under crash loads exceeding 15 kN.

## Prior art
- US11661028B2 Seatbelt usage detection, Tesla, Inc.: Detects post-installation usage patterns via sensors but provides no manufacturing-stage verification of anchor connection force.
- US12122313B2 Seatbelt buckle engagement detection, Magna Electronics: Monitors marker movement after tensioner activation but does not verify initial mechanical seating force at the pretensioner anchor during production.

## Summary of the invention
The invention adds a strain-gauge force sensor (22) to the pretensioner anchor (14) that measures axial insertion force applied by the seat belt connector during the final 5 mm of travel. The sensor output is sampled at 1 kHz by a local microcontroller (26) that compares peak force to a stored threshold. A green indicator (30) illuminates only on successful connection; otherwise a red alert halts the line and records the VIN and station ID.

## Claims
1. A seat belt pretensioner anchor verification apparatus comprising: an anchor body (12) configured to receive a seat belt connector; a force sensor (22) mounted on the anchor body (12) and positioned to measure axial insertion force applied by the connector; a microcontroller (26) electrically coupled to the force sensor (22) and configured to compare a peak force value against a predetermined threshold of 180 N; and an output device (30) that provides a pass indication only when the peak force exceeds the threshold.
2. The apparatus of claim 1 wherein the force sensor (22) is a strain gauge bonded to a cantilever section of the anchor body (12) having a thickness of 3.2 mm.
3. The apparatus of claim 1 wherein the microcontroller (26) samples the force sensor (22) at a rate of at least 1 kHz and stores the maximum value recorded during a 2-second window after connector insertion begins.
4. The apparatus of claim 1 further comprising a data logger that records the peak force value, a timestamp, and a vehicle identification number upon each connection attempt.
5. The apparatus of claim 1 wherein the output device (30) comprises a green LED that illuminates for a pass condition and a red LED plus audible alarm that activates for a fail condition.
6. The apparatus of claim 1 wherein the predetermined threshold is set at 180 N plus or minus 10 N.

## Brief description of the drawings
FIG. 1 shows a side cross-section view of the pretensioner anchor assembly with integrated force sensor and connection to the seat belt connector.
FIG. 2 shows a schematic of the electronic verification circuit and data logging path.

## Detailed description
The pretensioner anchor assembly (12) is machined from 6061-T6 aluminum with an internal bore diameter of 12.7 mm plus 0.05 mm. The seat belt connector (16) is inserted along axis (18) until it seats against shoulder (20). A strain-gauge force sensor (22) is bonded to a 3.2 mm thick cantilever beam (24) machined into the anchor body. The sensor (22) produces an output voltage proportional to axial force with a sensitivity of 2 mV/V per 100 N. Microcontroller (26) samples the amplified signal at 1 kHz for a 2-second window starting when insertion force first exceeds 20 N. Peak force is compared to the 180 N threshold stored in non-volatile memory. If the peak meets or exceeds 180 N, the green LED (30) illuminates for 3 seconds and a pass record containing VIN, station ID, timestamp, and peak force is written to flash memory. If below threshold, the red LED and 85 dB buzzer activate continuously until a supervisor resets the station via key switch (32). Failure mode of sensor drift is handled by an automatic zero-calibration routine performed at the start of each shift that records baseline voltage with no load applied. Connection that passes the force test but later loosens is prevented by the 180 N threshold corresponding to full seating depth verified by destructive pull testing at 15 kN. The system is powered from the assembly station 24 VDC supply with a 500 ms hold-up capacitor to survive brief power interruptions. All reference numerals in the description appear in the figures.