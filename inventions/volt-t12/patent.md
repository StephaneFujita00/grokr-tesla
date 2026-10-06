# Manufacturing Fixture with Integrated Electrical Continuity Probe for Steering Wheel Airbag Horn Pad Verification

## Abstract
A manufacturing fixture verifies correct horn pad installation on steering wheel airbags during assembly. The fixture includes a base plate supporting the airbag module, a probe assembly with spring-loaded contacts aligned to horn pad terminals, and a continuity tester connected to a controller. The controller signals pass or fail based on measured resistance below 0.5 ohms. This prevents installation of mismatched horn pads that interrupt the horn circuit.

## Problem
During airbag module assembly for Model S and Model X steering wheels, an incorrect horn pad may be installed. The horn pad provides the electrical contact surface for the horn switch. Mismatch prevents circuit closure when the driver presses the pad, leaving the horn inoperative. Manual visual inspection misses dimensional or material differences in the pad.

## Prior art
- US8801033B2, Airbag system, describes crash sensors and deployment but does not include post-assembly electrical verification of horn contacts.
- US9039038B2, Steering wheel mounted aspirated airbag system, covers airbag housing and deployment without horn pad continuity testing.
- KR101685237B1, Mounting section structure for airbag device, addresses mechanical mounting plates without electrical probe integration.

## Summary of the invention
The invention provides a fixture that mechanically seats the airbag module and electrically probes the horn pad terminals before the module leaves the production line. Spring-loaded probes contact specific points on the horn pad. A low-current continuity test confirms correct pad material and geometry. Failures trigger rejection and rework.

## Claims
1. A manufacturing fixture for verifying horn pad installation on a steering wheel airbag module, the fixture comprising a base plate (12) configured to receive the airbag module (14), a probe assembly (20) mounted above the base plate having at least two spring-loaded contacts (22) spaced 18 mm apart and aligned to horn pad terminals (16), and a controller (30) electrically connected to the contacts and configured to measure resistance and output a pass signal only when resistance is below 0.5 ohms.
2. The fixture of claim 1, wherein the probe assembly further comprises a linear actuator (24) that lowers the contacts with a force of 2.5 N per contact for a dwell time of 1.5 seconds.
3. The fixture of claim 1, wherein the controller (30) logs the measured resistance value and module serial number to a database.
4. The fixture of claim 1, further comprising a reject bin actuator (36) that diverts the module if the resistance exceeds 0.5 ohms.
5. The fixture of claim 1, wherein the contacts (22) are gold-plated copper with a tip radius of 0.8 mm to ensure repeatable contact on the horn pad surface.
6. The fixture of claim 2, wherein the actuator stroke is limited to 35 mm to prevent damage to the airbag cover.

## Brief description of the drawings
FIG. 1 shows a side view of the fixture with the airbag module seated and probes lowered.
FIG. 2 shows a top view of the probe alignment relative to the horn pad terminals.

## Detailed description
The fixture base plate (12) is machined from 6061-T6 aluminum, 25 mm thick, with locating pins (18) at 120 mm spacing that engage mounting holes in the airbag module (14). The airbag module rests on four support pads (19) that maintain the horn pad plane parallel to the probe plane within 0.2 mm. The probe assembly (20) rides on two linear guide rails (26) and is driven by the pneumatic actuator (24) supplied at 5.5 bar. Each spring-loaded contact (22) has a travel range of 8 mm and exerts 2.5 N at mid-stroke. The contacts align to the two horn pad terminals (16) that are 18 mm apart and 12 mm from the module centerline. When the actuator reaches bottom dead center, a limit switch (28) triggers the controller (30) to apply 10 mA at 5 V DC across the contacts. If resistance is below 0.5 ohms for the full 1.5-second dwell, the controller illuminates a green indicator (32) and releases the module. If resistance exceeds 0.5 ohms, the controller activates the reject bin actuator (36), records the serial number and resistance value, and illuminates a red indicator (34). The gold-plated copper contacts with 0.8 mm tip radius maintain contact resistance stability within 0.05 ohms over 10,000 cycles. Failure modes addressed include incorrect pad material causing high resistance, misaligned pad shifting terminals outside probe reach, and debris on the pad surface; the fixture detects all by the resistance threshold. Every reference numeral appears in a figure.