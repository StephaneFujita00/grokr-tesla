# System and Method for Detecting Steering Wheel Airbag Compatibility via Connector Signature

## Abstract
An electronic control unit in the steering column reads an electrical signature from the driver airbag module connector. If the measured resistance or pin configuration does not match the expected value stored for the installed steering wheel type, the system logs a fault, illuminates the airbag warning lamp, and prevents deployment until service confirms correct pairing.

## Problem
During steering wheel or yoke replacement, an airbag module from a different wheel style may be installed. The airbag inflator and vent geometry are tuned to the wheel spoke and cover design. Mismatch causes incorrect deployment kinematics, raising injury risk. Current service relies on visual inspection with no automated verification after reassembly.

## Prior art
- CN111051145B Sensor and method for vehicle occupant classification system: Uses weight and presence sensors for cabin occupants; does not address steering wheel module identity or connector-level verification.

## Summary of the invention
The invention adds a passive signature resistor or pin-short pattern inside the airbag module connector housing. The restraint control module (RCM) firmware measures the signature at power-up and after each ignition cycle. A mismatch triggers a diagnostic trouble code and inhibits the deployment circuit for the driver stage.

## Claims
1. A vehicle restraint system comprising a steering wheel assembly (10) having a connector (12) with at least one dedicated signature pin pair, an airbag module (14) containing a resistor (16) of 2.2 kOhm plus or minus 5 percent between the signature pins, and a restraint control module (18) programmed to measure resistance across the signature pins within 500 milliseconds of ignition on and to set diagnostic code B1Axx if the measured value falls outside 2.09 kOhm to 2.31 kOhm.
2. The system of claim 1 wherein the restraint control module (18) further compares the measured resistance against a stored value corresponding to the steering wheel part number read from the body control module (20) over the vehicle CAN bus.
3. The system of claim 2 wherein the restraint control module (18) opens the deployment enable relay (22) when mismatch persists for three consecutive ignition cycles.
4. The system of claim 1 wherein the connector (12) includes a mechanical key (24) that physically blocks insertion of an airbag module lacking the matching key profile.
5. The system of claim 1 wherein the resistance measurement circuit inside the restraint control module (18) applies a 5 volt reference through a 10 kOhm pull-up and samples the voltage at the analog-to-digital converter input with 12-bit resolution.
6. The system of claim 3 wherein the diagnostic code B1Axx is transmitted to the instrument cluster (26) causing continuous illumination of the airbag warning lamp until cleared by a service tool after verified replacement.

## Brief description of the drawings
FIG. 1 shows the steering column assembly with connector and signature resistor.
FIG. 2 shows the schematic of the resistance measurement circuit and decision logic.

## Detailed description
Referring to FIG. 1, the steering wheel assembly (10) carries connector (12) at the end of the clock spring harness. Airbag module (14) mates to connector (12). A 2.2 kOhm resistor (16) is molded into the connector housing of the airbag module. The restraint control module (18) is mounted under the instrument panel and receives the two signature wires from the clock spring. The body control module (20) supplies the installed steering wheel part number over the CAN bus. Deployment enable relay (22) is located inside the restraint control module housing. Mechanical key (24) is a molded tab on the connector that only permits full engagement when the airbag module matches the wheel style. Instrument cluster (26) displays the airbag warning symbol.

The resistance measurement occurs as follows. At ignition on the restraint control module (18) applies 5 V through the 10 kOhm pull-up resistor to one signature pin. The voltage divider formed with resistor (16) is sampled by the 12-bit analog-to-digital converter. The firmware converts the reading to resistance using the equation R = 10000 * (Vmeasured / (5 - Vmeasured)). If the result lies outside the 2.09 kOhm to 2.31 kOhm window, or differs by more than 10 percent from the expected value derived from the part number supplied by body control module (20), the system sets code B1Axx and opens relay (22) after three cycles. Failure modes addressed include open circuit (infinite resistance), short to ground (0 Ohm), or wrong resistor value from an incorrect module. The mechanical key (24) provides a secondary physical barrier that prevents full electrical connection of mismatched modules. All dimensions and tolerances are chosen to remain within standard automotive connector specifications while adding only passive components.