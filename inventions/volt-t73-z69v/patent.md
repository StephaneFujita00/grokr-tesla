# Firmware Calibration Routine For Parking Light Output Compliance

## Abstract
A firmware module in a vehicle controller enforces parking light intensity limits by applying a calibrated PWM duty cycle cap derived from sensor feedback and stored calibration values. The routine runs on each ignition cycle, compares measured output against FMVSS 108 thresholds, and clamps drive signals within 2 percent tolerance. It logs deviations and triggers a safe-mode reduction if calibration drift exceeds limits.

## Problem
The vehicle controller software may command front parking lights above the maximum allowable light output specified in FMVSS 108. This occurs because the PWM drive values stored in the lighting ECU lack runtime verification against actual LED output or ambient temperature effects. Resulting glare affects oncoming drivers and causes regulatory non-compliance.

## Prior art
- WO2024195816A1 Vehicle lamp: describes marker light modes but does not include runtime intensity verification or PWM clamping based on sensor data.
- US11021095B2 Replacement multifunction automobile light system: covers LED selection and optics, lacks software calibration loop for regulatory output caps.
- CN109204117B Method for reporting glare: focuses on glare detection reporting, no closed-loop control of parking light drive signals.

## Summary of the invention
The invention adds a calibration routine to the lighting control firmware. On power-up the controller measures LED current and voltage through existing sense resistors, computes effective luminous intensity using a stored transfer function, and applies a PWM duty cycle limit if the value exceeds 80 percent of the FMVSS threshold. The limit persists until the next ignition cycle or until a service recalibration resets the stored offset.

## Claims
1. A method in a vehicle lighting controller comprising: reading a stored calibration offset (12); measuring LED forward voltage and current (14, 16); computing estimated luminous intensity using a polynomial transfer function; comparing the estimate to a regulatory maximum; and clamping PWM duty cycle to a value that keeps intensity below 102 percent of the maximum when the comparison indicates excess.
2. The method of claim 1 further comprising logging the measured intensity and applied clamp value to non-volatile memory with a timestamp.
3. The method of claim 1 further comprising entering a reduced-output safe mode when the computed intensity remains above the regulatory maximum after three consecutive clamp attempts.
4. The method of claim 1 wherein the polynomial transfer function uses coefficients stored at manufacture and updated only by authenticated service tool.
5. The method of claim 3 wherein safe mode reduces PWM duty cycle by an additional 15 percent relative to the clamped value.
6. The method of claim 1 wherein measurement occurs within 500 milliseconds after ignition-on and the clamp is applied before the parking lights are enabled.

## Brief description of the drawings
FIG. 1 shows the lighting ECU connected to the front parking LED array with sense resistors and temperature sensor.

## Detailed description
The vehicle lighting electronic control unit (ECU) (10) contains a microcontroller (20) executing firmware that includes the calibration routine. On ignition-on the microcontroller reads the stored calibration offset (12) from EEPROM. It then enables a low-side sense resistor (14) of 0.05 ohm and samples LED forward voltage across a 10 k ohm divider (16). A thermistor (18) mounted on the LED heatsink provides temperature data. The firmware applies the stored third-order polynomial I = a0 + a1*V + a2*V^2 + a3*V^3 + offset to compute estimated luminous intensity in candela. If the result exceeds 80 percent of the FMVSS 108 parking light limit the routine calculates the maximum allowable PWM duty cycle Dmax such that intensity remains below 102 percent of the limit. The PWM generator (22) is then restricted to Dmax for the duration of the drive cycle. The routine repeats the measurement every 30 seconds while the lights are active; if drift greater than 5 percent is detected the clamp is tightened by 2 percent steps. A persistent deviation beyond three attempts forces entry into safe mode where duty cycle is further reduced by 15 percent. All measurements and clamp values are written to a 128-byte circular buffer in flash with 32-bit timestamps. Service recalibration requires authenticated CAN messages that replace the polynomial coefficients and reset the offset. The firmware rejects any command that would drive the LEDs above the clamped limit. Failure modes addressed include sensor open-circuit (treated as maximum intensity, immediate clamp to 50 percent duty), short-circuit (immediate shutdown of that channel), and coefficient corruption (fallback to conservative factory default values stored in ROM). All timing values, resistor tolerances of 1 percent, and voltage measurement resolution of 10 mV are enforced in the firmware constants.