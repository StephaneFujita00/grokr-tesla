# Manufacturing Process for Reliable Pyrotechnic Battery Disconnect

## Abstract
A manufacturing method and apparatus for pyrotechnic battery disconnect units in electric vehicles uses automated vision inspection and redundant electrical continuity testing at multiple stages to detect defects in initiator squib placement and circuit integrity before final assembly. The process enforces tolerances of 0.2 mm on squib seating and applies 100% functional firing simulation on test circuits.

## Problem
Pyrotechnic battery disconnects in 2023 Model 3 and Y vehicles may contain manufacturing defects that prevent activation after crash or fault signals. Defective units fail to sever the high-voltage circuit, leaving battery voltage present and creating shock hazard. Root cause is inconsistent squib insertion depth and undetected continuity breaks during assembly.

## Prior art
- No prior patents returned by searches; this invention addresses assembly-line verification absent in existing pyrotechnic disconnect production.

## Summary of the invention
The invention adds in-line machine vision and dual-probe continuity stations to the pyrotechnic disconnect assembly line. Cameras verify squib depth to 0.2 mm tolerance and probe pairs confirm circuit resistance below 2 ohms before and after housing closure. Failed units are automatically rejected and logged for root-cause analysis.

## Claims
1. A manufacturing method for a pyrotechnic battery disconnect comprising: positioning an initiator squib into a housing bore; imaging the squib seating depth with a vision system calibrated to 0.05 mm resolution; rejecting the assembly if depth deviates more than 0.2 mm from nominal; performing a first continuity test across initiator leads with a 10 mA current source; closing the housing; and performing a second continuity test after closure.
2. The method of claim 1 further comprising logging each test result with a unique serial number and halting the line if three consecutive units fail.
3. The method of claim 1 wherein the vision system uses structured light projection and edge detection algorithms to measure squib shoulder position relative to housing datum.
4. The method of claim 1 wherein continuity tests apply a 5 V bias and measure resistance, rejecting if above 2 ohms or if open circuit is detected.
5. The method of claim 1 further comprising a simulated firing pulse of 1.2 A for 2 ms on a parallel test circuit without igniting the live squib.
6. An apparatus implementing the method of claim 1 comprising a conveyor, vision station, dual-probe continuity station, and reject bin controlled by a programmable logic controller.

## Brief description of the drawings
FIG. 1 shows the assembly line station with vision camera and continuity probes in side view.
FIG. 2 shows a cross-section of the pyrotechnic unit with reference numerals for squib, housing, and test points.

## Detailed description
The assembly line moves pyrotechnic battery disconnect housings (12) on a conveyor (14) at 0.5 m/s. At the vision station, a camera (16) with 5 megapixel resolution and telecentric lens images the initiator squib (18) seated in bore (20). Structured light projector (22) casts lines at 45 degrees; processor (24) calculates seating depth from edge positions. Nominal depth is 12.5 mm; tolerance is plus or minus 0.2 mm. Units outside tolerance are diverted to reject bin (26).

After vision pass, dual spring-loaded probes (28) contact initiator leads (30) and apply 10 mA at 5 V. Resistance is measured; values above 2 ohms or open circuit trigger rejection. Housing cover (32) is then pressed on with 150 N force. A second probe pair (34) repeats the continuity test through access ports (36) in the closed housing.

A parallel test circuit (38) applies a 1.2 A pulse for 2 ms to verify firing electronics without energizing the live squib (18). All measurements are stored with serial number in database (40). The PLC (42) stops the line if failure rate exceeds three units in succession. This catches squib misalignment and lead fractures that cause non-activation in the field. Materials are aluminum housing (12) with 6061-T6 alloy and stainless steel squib body (18). Probe contact resistance is calibrated daily to 0.05 ohms. Failure modes addressed include partial insertion, cracked leads, and poor crimps.