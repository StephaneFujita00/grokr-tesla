# Redundant Mechanical Clamp for Adhesively Attached Windshield Light Bar

## Abstract
A redundant mechanical clamp assembly secures an off-road light bar accessory to a vehicle windshield when adhesive bonding with primer may be compromised. The clamp uses adjustable brackets engaging the light bar housing and windshield frame edges with torque-limited fasteners providing 150-200 N retention force independent of adhesive. Sensors detect displacement and trigger a dashboard alert if movement exceeds 2 mm.

## Problem
Incorrect primer applied during service installation of the light bar accessory allows adhesive tape bond to degrade under thermal cycling and vibration, leading to detachment. No secondary retention exists, creating road hazard.

## Prior art
- US10604059B2 Modular light and accessory bar for vehicles: describes top rail spanning windshield but relies solely on pillar attachments without redundant windshield clamp for adhesive failure.
- JP6199863B2 Luminous glazing for vehicles: integrates LEDs into glazing with edge bonding but no external accessory clamp or displacement sensing.

## Summary of the invention
The invention adds a pair of C-shaped aluminum clamps (yield strength 200 MPa) that hook over the light bar extrusion and grip the upper windshield frame with M5 bolts torqued to 4 Nm. An integrated Hall-effect sensor monitors relative motion between clamp and bar. Firmware in the body control module logs displacement and illuminates a warning if threshold crossed.

## Claims
1. A redundant attachment system for a windshield-mounted light bar comprising: a light bar housing (12) adhesively bonded to windshield (14); at least one C-shaped clamp (20) having a first arm engaging the housing and a second arm engaging the windshield upper frame edge; and a fastener (22) applying 150-200 N compressive force between the arms.
2. The system of claim 1 further comprising a displacement sensor (30) mounted between clamp (20) and housing (12) outputting a signal when relative displacement exceeds 2 mm.
3. The system of claim 2 wherein the body control module receives the sensor signal and activates a visual warning on the instrument cluster within 500 ms.
4. The system of claim 1 wherein the clamp (20) is formed of 6061-T6 aluminum with wall thickness 3 mm and the fastener is an M5 socket head cap screw torqued to 4.0 Nm ±0.2 Nm.
5. The system of claim 1 wherein two clamps are spaced 400 mm apart along the 1200 mm light bar length.
6. The system of claim 1 wherein the clamp second arm includes an elastomeric pad (24) of 2 mm thickness and 60 Shore A hardness to distribute load without glass damage.

## Brief description of the drawings
FIG. 1 shows the clamp assembly installed on the light bar and windshield in side cross-section view.
FIG. 2 shows the top view of dual clamps with sensor wiring.

## Detailed description
The light bar housing (12) is a 1200 mm long aluminum extrusion adhesively attached via tape to the outer surface of windshield (14). To provide redundancy, two C-shaped clamps (20) are installed. Each clamp (20) is machined from 6061-T6 aluminum bar stock 3 mm thick. The first arm (21) extends 25 mm over the top of housing (12) and the second arm (23) extends 30 mm under the upper edge of the windshield frame (16). An M5×0.8 socket head cap screw (22) passes through a clearance hole in arm (21) and threads into a tapped hole in arm (23). The screw is tightened to 4.0 Nm producing 175 N nominal clamp force. An elastomeric pad (24) of 2 mm thickness and 60 Shore A hardness is bonded to the contact face of arm (23) to avoid point loading on glass. A Hall-effect displacement sensor (30) is potted into a recess in arm (21) with its sensing face 1 mm from a ferrous target (32) embedded in the housing (12). Sensor output is a 0-5 V analog signal linear from 0 mm to 5 mm displacement. Body control module firmware samples the signal every 100 ms; if value exceeds 2 mm for three consecutive samples, a CAN message is sent to the instrument cluster to illuminate the accessory warning icon. Failure mode of adhesive creep is countered by the mechanical clamp maintaining position. Failure mode of clamp loosening is detected by the sensor and reported before detachment. All dimensions are nominal with tolerance ±0.5 mm unless otherwise specified. The assembly adds 180 g mass and installs in under 10 minutes per vehicle.