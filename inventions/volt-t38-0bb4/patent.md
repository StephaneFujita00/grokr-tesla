# Redundant Camera Feed Routing with Voltage Monitoring Firmware

## Abstract
A firmware module in the vehicle computer monitors power rail voltage to the infotainment and camera processing board. Upon detecting a short-induced voltage drop below 3.0 V for more than 50 ms, the module switches rearview camera data path to a secondary low-power encoder on the body control module and routes the feed over the vehicle CAN-FD bus at 2 Mbps to the display controller. The switch completes in under 200 ms and maintains FMVSS 111 compliance without requiring the primary board.

## Problem
The computer circuit board may experience an internal short that collapses the 3.3 V and 5 V rails supplying the rearview camera decoder and video pipeline. This removes the image from the center display, violating FMVSS 111. Hardware replacement addresses only failed units; a software-level mitigation is required for vehicles already in the field and to prevent recurrence on marginal boards.

## Prior art
None of the searched patents address firmware detection and rerouting of camera video around a shorted infotainment board.

## Summary of the invention
The invention adds a voltage supervisor (12) and a firmware task (14) that continuously samples the camera power rail via ADC channel 3. When the rail drops below the 3.0 V threshold for the programmed 50 ms debounce, the firmware asserts a GPIO that enables a secondary H.264 encoder (16) located on the body control module. Simultaneously it reconfigures the display controller to source video from a newly created CAN-FD virtual channel rather than the PCI-express link from the primary board. All timing parameters and thresholds are stored in non-volatile memory and are updatable via the existing OTA mechanism.

## Claims
1. A method for maintaining rearview camera availability in a vehicle, the method comprising: monitoring voltage on a power rail supplying a primary camera decoder; detecting a voltage below 3.0 V sustained for at least 50 ms; enabling a secondary encoder on a body control module; and routing encoded video frames over a CAN-FD bus to a display controller within 200 ms of detection.
2. The method of claim 1 further comprising storing the voltage threshold and debounce time in non-volatile memory that is writable by an over-the-air update.
3. The method of claim 1 wherein the secondary encoder operates at a maximum of 15 frames per second and 720p resolution when activated.
4. The method of claim 1 further comprising logging the event with timestamp and rail voltage value to a persistent fault buffer readable by service tools.
5. The method of claim 1 wherein the CAN-FD virtual channel uses message identifier 0x3F2 and a data payload of 64 bytes per frame segment.
6. The method of claim 1 further comprising reverting to the primary path only after the monitored voltage remains above 4.5 V for a continuous 30 seconds.

## Brief description of the drawings
FIG. 1 shows the primary infotainment board, body control module, rear camera, and display controller with power and data paths and reference numerals for the monitoring and switching elements.

## Detailed description
The primary infotainment computer board (10) contains the main camera decoder powered from a 3.3 V rail (11). A voltage supervisor integrated circuit (12) connected to ADC channel 3 of the main processor (13) samples the rail every 10 ms. Firmware task (14) running at 100 Hz compares the sampled value against the stored 3.0 V threshold. When the comparison indicates a sustained low for 50 ms, the firmware sets GPIO pin 17 high. This signal enables the secondary H.264 encoder (16) on the body control module (15). The encoder receives raw frames from the rear camera (18) via an existing LVDS link that remains powered from a separate 12 V battery feed. Encoded frames are packetized into 64-byte segments and transmitted on CAN-FD bus (19) using message ID 0x3F2 at 2 Mbps. The display controller (20) receives these segments, reassembles the frame, and renders it on the center display (21) at 720p and 15 fps. A 200 ms timeout timer (22) in the display controller triggers a “camera unavailable” icon only if no valid frame arrives. After activation the firmware continues to monitor the primary rail. Reversion to the primary path occurs only after the rail voltage stays above 4.5 V for 30 continuous seconds, at which point GPIO 17 is deasserted and the CAN-FD channel is released. All parameters (3.0 V, 50 ms, 4.5 V, 30 s, 200 ms) are held in a 256-byte calibration block in flash memory that is updated by the existing OTA service. Failure modes addressed include intermittent shorts that recover, permanent shorts that keep the secondary path active, and CAN bus congestion; the latter is mitigated by priority arbitration of message 0x3F2 above all non-safety traffic.