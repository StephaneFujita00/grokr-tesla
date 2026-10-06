# Software Module for Enhanced Autosteer Control Prominence and Driver State Verification

## Abstract
A software module in a vehicle ADAS controller increases visual and haptic prominence of Autosteer engagement indicators and implements periodic driver attention verification at intervals of 5 to 15 seconds when the system detects low steering torque input below 0.5 Nm. The module logs driver interaction events and forces a transition to standby mode if verification fails within 3 seconds.

## Problem
When Autosteer is engaged the existing interface displays a low-contrast icon on the instrument cluster and allows continued operation with insufficient driver torque input. Drivers may fail to notice cancellation events or remain disengaged, increasing crash risk in SAE Level 2 operation. The software lacks timed prompts and escalation to require explicit driver acknowledgment.

## Prior art
No prior patents were located in searches for Autosteer driver monitoring or ADAS control prominence.

## Summary of the invention
The invention adds a driver state verification routine and an enhanced indicator rendering layer to the Autosteer firmware. It monitors steering wheel torque sensor values, issues visual pop-up alerts of 2-second duration at 80 percent screen brightness, and triggers a steering wheel vibration motor pulse of 200 ms if torque remains below threshold. Failure to respond escalates to full system disengagement and audible chime at 85 dB.

## Claims
1. A method in a vehicle ADAS controller comprising: monitoring steering torque sensor output at 100 Hz sampling rate; rendering an enlarged Autosteer status icon occupying at least 15 percent of instrument cluster area when engaged; initiating a driver attention prompt every 8 seconds when torque input is below 0.5 Nm for more than 2 seconds; and transitioning Autosteer to standby if no driver response is detected within 3 seconds.
2. The method of claim 1 further comprising logging each prompt event and response time to non-volatile memory for post-incident analysis.
3. The method of claim 1 wherein the driver attention prompt includes both a visual overlay and a 200 ms haptic pulse on the steering wheel rim.
4. The method of claim 1 wherein the controller requires a minimum 1.0 Nm torque input for 500 ms to confirm driver engagement before allowing continued Autosteer operation after a prompt.
5. The method of claim 1 wherein system cancellation due to verification failure generates an audible chime of 85 dB and displays a text message stating "Autosteer disengaged, driver must take control".
6. The method of claim 1 wherein the sampling rate, torque threshold, and prompt interval are stored in calibration tables modifiable via OTA update.

## Brief description of the drawings
FIG. 1 shows the software control flow and instrument cluster rendering.

## Detailed description
The ADAS controller (20) executes the verification routine at startup of Autosteer engagement detected via steering rack angle command (22). Torque sensor (24) provides analog signal conditioned to digital values at 100 Hz. When filtered torque remains below 0.5 Nm for 2 seconds the routine activates the enhanced display layer. Icon (26) is rendered at 15 percent of cluster area with white fill on black background and 2-second timeout. If no torque increase above 1.0 Nm is measured within 3 seconds the haptic driver (28) activates a 200 ms pulse at 50 Hz. Failure triggers standby state (30) and logs timestamp plus response latency. All thresholds are held in EEPROM calibration block (32) updated during OTA sessions. Failure mode of sensor dropout defaults to immediate disengagement to prevent silent operation. The module runs in a 10 ms task on the main ADAS processor with watchdog timer reset every cycle.