# Adjustable Pitch Mount for Forward Camera in Vehicle Windshield Assembly

## Abstract
An adjustable pitch mount for a forward-facing camera in a vehicle windshield assembly uses a two-piece bracket with a pivot pin and micrometer-style adjustment screw. The mount allows pitch angle setting to within 0.05 degrees during manufacturing. A strain gauge sensor monitors preload on the adjustment screw. The design prevents post-assembly drift due to thermal cycling or vibration.

## Problem
Forward-facing cameras in Model Y vehicles can become misaligned in pitch angle after windshield installation. This misalignment disables active safety features without driver notification. Manual post-production adjustment requires service visits and does not address root causes in the assembly process.

## Prior art
- US9491450B2, Vehicle camera alignment system, uses inclination sensor but lacks integrated factory adjustment screw and preload monitoring.
- JP2011213193A, On-vehicle camera, provides fixed bracket without fine pitch adjustment mechanism or sensor feedback during mounting.

## Summary of the invention
The invention provides a camera mount bracket assembly (10) with a fixed base (12) attached to the windshield header and a pivoting camera carrier (14) connected by a 4 mm diameter pivot pin (16). An M3 adjustment screw (18) with 0.5 mm pitch thread engages a threaded boss (20) on the base. Rotation of the screw by 1/4 turn changes pitch by 0.125 degrees. A strain gauge (22) bonded to the screw shank measures preload between 8 and 12 N to prevent loosening. The carrier holds the camera module (24) with three locating pins (26) at 120 degree spacing. Assembly tolerance stack-up is controlled to +/-0.02 mm at the lens plane.

## Claims
1. A vehicle forward camera mount comprising a fixed base attached to the windshield header, a pivoting carrier holding the camera module, a pivot pin of 4 mm diameter connecting the base and carrier, and an M3 adjustment screw of 0.5 mm pitch thread engaging a threaded boss on the base, wherein rotation of the screw adjusts camera pitch angle.
2. The mount of claim 1 further comprising a strain gauge bonded to the adjustment screw shank configured to output preload force between 8 N and 12 N.
3. The mount of claim 1 wherein the carrier includes three locating pins spaced at 120 degrees to engage corresponding holes in the camera module housing.
4. The mount of claim 1 wherein the adjustment screw head includes a 2 mm hex socket accessible through an opening in the windshield header trim.
5. The mount of claim 2 wherein the strain gauge signal is read by the vehicle camera ECU during end-of-line calibration and stored as a baseline value.
6. The mount of claim 1 wherein the pivot pin is retained by a circlip and the adjustment screw is secured by a thread-locking compound applied at the boss interface.

## Brief description of the drawings
FIG. 1 shows a side sectional view of the camera mount assembly installed on the windshield header.
FIG. 2 shows an exploded isometric view of the base, carrier, pivot pin, and adjustment screw.

## Detailed description
The fixed base (12) is injection-molded from 30% glass-filled nylon with a mounting flange 80 mm wide and 3 mm thick. Two 5 mm mounting holes (28) accept self-tapping screws into the windshield header metal. The pivoting carrier (14) is molded from the same material and includes a cylindrical boss (30) of 12 mm diameter that receives the pivot pin (16). The pivot pin is 4 mm diameter stainless steel with 0.01 mm clearance fit to the boss bore. The adjustment screw (18) is M3 x 0.5 mm pitch stainless steel, 25 mm long, with a 6 mm diameter head containing the 2 mm hex socket. The threaded boss (20) is integrally molded into the base and accepts 8 full threads of engagement. The strain gauge (22) is a 3 mm x 5 mm foil gauge with 350 ohm resistance bonded to the screw shank 10 mm below the head. During manufacturing, the camera module (24) is seated on the three locating pins (26) and secured with two M2 screws torqued to 0.4 Nm. Pitch is adjusted by turning the adjustment screw until the camera optical axis is within 0.05 degrees of nominal using a collimated target at 10 m. Preload is verified at 10 N +/-2 N. Failure mode of screw back-out is mitigated by the thread-locking compound and monitored preload value; if strain drops below 6 N the ECU sets a diagnostic trouble code. Thermal expansion mismatch between nylon and steel is accommodated by the 0.01 mm radial clearance at the pivot. Vibration testing to 20 g at 50 Hz showed no pitch drift exceeding 0.02 degrees after 10^6 cycles.