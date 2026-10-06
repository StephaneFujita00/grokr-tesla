# Headlight Driver with Redundant PWM Feedback Loop for Flicker Prevention

## Abstract
A headlight control circuit for vehicles uses dual PWM controllers with cross-coupled voltage feedback to maintain constant LED current despite supply variations. Primary controller (12) drives LED array (20) at 400 Hz PWM. Secondary controller (14) monitors voltage across sense resistor (22) and adjusts duty cycle if deviation exceeds 2%. This prevents flicker in low-beam and parking lights while meeting FMVSS 108 illumination standards.

## Problem
Model X 2024 headlight and parking light circuits exhibit flicker due to PWM instability under battery voltage swings between 9 V and 16 V. Software updates alone cannot correct hardware-level current ripple exceeding 15% peak-to-peak, violating minimum luminous intensity requirements.

## Prior art
- US10808900B1 Automotive LED lighting module: Uses single DC driver without PWM feedback; invention adds redundant PWM loop for dynamic correction.
- US10807516B2 Lighting circuit: Series bypass switches for pattern control; invention focuses on current stabilization rather than pattern switching.

## Summary of the invention
The circuit employs a primary buck converter (12) generating PWM at fixed 400 Hz with 0.5% tolerance crystal (16). A secondary controller (14) samples voltage at sense resistor (22) every 2.5 ms. If measured current deviates more than 2% from target 1.2 A, the secondary overrides the PWM duty via AND gate (18). Tolerances on sense resistor are ±1%. Failure mode of primary oscillator drift is detected by secondary watchdog and switches to fixed 50% duty safe mode.

## Claims
1. A vehicle headlight driver comprising a primary PWM controller (12) connected to an LED array (20), a sense resistor (22) in series with the LED array, and a secondary controller (14) that samples voltage across the sense resistor and adjusts PWM duty cycle when deviation exceeds a predetermined threshold.
2. The driver of claim 1 wherein the primary controller operates at 400 Hz and the secondary controller samples at 400 Hz divided by 1.
3. The driver of claim 1 further comprising a crystal oscillator (16) providing timing reference to the primary controller with frequency tolerance of 0.5%.
4. The driver of claim 1 wherein the secondary controller activates a fixed-duty safe mode upon detection of primary oscillator failure.
5. The driver of claim 1 wherein the sense resistor has tolerance of ±1% and target current is 1.2 A for low-beam operation.
6. The driver of claim 1 wherein the adjustment threshold is 2% current deviation.

## Brief description of the drawings
FIG. 1 shows the overall circuit block diagram with primary and secondary controllers, LED array, and feedback path.
FIG. 2 shows detailed PWM generation and override logic with reference numerals for timing components.

## Detailed description
Primary buck converter controller (12) receives 12 V nominal vehicle supply and produces PWM output at 400 Hz to switch MOSFET (24) connected to LED array (20). Current flows through LED array (20) and sense resistor (22) rated 0.1 ohm ±1%. Voltage developed across resistor (22) is fed to both primary feedback pin and secondary controller (14) analog input. Secondary controller (14) compares sampled value to 120 mV reference every 2.5 ms. When absolute deviation exceeds 2.4 mV, secondary output drives AND gate (18) to shorten or lengthen the PWM pulse width by up to 5%. Crystal (16) at 8 MHz divided internally provides base clock. If primary PWM period deviates beyond 2.6 ms or 2.4 ms, secondary watchdog timer forces 50% duty cycle output through override line (26). All components rated for -40 °C to 105 °C operation. The circuit is mounted on a 1.6 mm FR4 PCB with thermal vias under MOSFET (24). This arrangement keeps current ripple below 3% peak-to-peak across the full voltage range.