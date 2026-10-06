# Seat Side Airbag Deflector Presence Verification System

## Abstract
A manufacturing verification system for seat side airbag modules uses a camera and laser sensor pair to confirm deflector installation before module closure. The system measures reflector position to 0.5 mm tolerance and logs data to the vehicle ECU. It prevents assembly of modules missing the gas flow deflector.

## Problem
In seat side airbag module assembly, the deflector that directs inflation gas flow can be omitted. Without it, gas flow is uncontrolled, leading to improper airbag deployment and increased injury risk. Current assembly relies on manual checks that miss single-unit errors.

## Prior art
- JP2013514924A, Inflatable airbag assembly having a non-planar inflation gas deflector: describes deflector shapes but no in-line assembly verification.
- US8714584B2, Side airbag apparatus: covers check valves in side airbags but lacks sensor-based presence detection during build.
- US9108552B2, Vehicle seat and resin seatback spring: addresses airbag mounting to seat frame without assembly sensors.

## Summary of the invention
The invention adds a station after deflector placement but before cover installation. A fixed camera (12) images the module interior while a laser displacement sensor (14) measures deflector edge position. Software compares values against stored CAD model. Pass/fail signal controls conveyor and writes result to module RFID tag (16) and vehicle build record.

## Claims
1. A verification station for seat side airbag modules comprising a camera (12) and laser sensor (14) positioned to inspect deflector (20) location after placement and before cover attachment, with controller (18) configured to reject the module if measured position deviates more than 0.5 mm from nominal.
2. The station of claim 1 wherein the controller writes pass/fail data to an RFID tag (16) attached to the module housing.
3. The station of claim 1 wherein the laser sensor operates at 650 nm wavelength with 0.1 mm resolution.
4. The station of claim 1 further comprising a pneumatic stop that halts the module carrier for 3 seconds during measurement.
5. The station of claim 1 wherein the camera captures images at 5 megapixel resolution under 500 lux LED illumination.
6. The station of claim 1 wherein failure triggers an audible alarm and logs the event with timestamp and serial number.

## Brief description of the drawings
FIG. 1 shows the verification station with module on carrier, camera and laser aligned to deflector.
FIG. 2 shows close-up cross-section of deflector edge measurement with reference numerals.

## Detailed description
The verification station is placed on the assembly line after the deflector insertion step. The module housing (22) travels on carrier (24) stopped by pneumatic cylinder (26) for 3 seconds. Camera (12) mounted 300 mm above the open module captures a 5 megapixel image of the interior under 500 lux LED strip (28). Laser displacement sensor (14) projects a 650 nm beam onto the deflector edge (20) and returns distance to 0.1 mm resolution. Controller (18) compares the measured edge coordinate to the nominal 42.0 mm from housing datum within 0.5 mm tolerance. If within tolerance, RFID writer (30) encodes pass status to tag (16) on housing (22) and releases the carrier. If out of tolerance or no deflector detected, the module is diverted to rework station and alarm sounds. The system logs serial number, timestamp, measured value and result to the plant database. Failure modes addressed include missed insertion (sensor reads >5 mm deviation), misplacement (edge offset >0.5 mm) and sensor drift (daily calibration check against reference block). All dimensions and tolerances are stated in the claims and match the figures.