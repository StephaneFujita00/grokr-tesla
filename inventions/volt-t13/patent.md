# Crash-Triggered Door Latch Inhibit Firmware for Model S

## Abstract
A firmware module in the body control module monitors vehicle acceleration via the airbag control unit. Upon detection of a side impact exceeding 5 g for 10 ms, the module asserts a 500 ms lock command to the door latch actuators. The command overrides unlock signals from interior switches until the timer expires. This meets FMVSS 214 requirements without hardware changes.

## Problem
During a side impact the cabin doors of 2021-2023 Model S and X vehicles can receive an unlock command from the body controller before the latch has mechanically settled. The latch then releases, allowing the door to open. The condition violates FMVSS 214 side impact protection.

## Prior art
- US20110137507A1, System having crash unlock algorithm, describes an ACU that compares acceleration to a threshold and sends an unlock signal to the BCM. The present invention inverts the logic to send a lock-inhibit signal instead.
- US9174597B2, Electro-mechanical protector for vehicle latches during crash conditions, adds a mechanical inertia lever. The present invention achieves the same result entirely in firmware with no added parts.
- CN108136880A, Double-hinge chain closure member with horizontal direction locking, addresses closure kinematics but does not address post-impact electrical unlock commands.

## Summary of the invention
The invention adds a 30-line firmware routine to the body control module that receives a crash flag from the airbag control unit over the vehicle CAN bus. When the flag is set the routine forces the four door latch motors to the locked state for a fixed 500 ms window and ignores all switch inputs during that window. The routine clears the flag after the window and returns normal operation.

## Claims
1. A method in a vehicle body control module comprising: receiving an acceleration signal from an airbag control unit; comparing the signal to a threshold of 5 g sustained for at least 10 ms; when the threshold is exceeded asserting a lock command to each door latch actuator for a duration of 500 ms; and blocking all unlock commands from door switches during the 500 ms interval.
2. The method of claim 1 wherein the acceleration signal is sampled at 1 kHz.
3. The method of claim 1 wherein the lock command is transmitted on the CAN bus at 500 kbps with message identifier 0x2A4.
4. The method of claim 1 further comprising clearing the lock command after 500 ms and restoring normal switch response within 20 ms.
5. The method of claim 1 wherein the threshold and duration values are stored in non-volatile memory and are updatable by authenticated over-the-air command.
6. A non-transitory computer-readable medium storing instructions that, when executed by a processor in a body control module, perform the method of claim 1.

## Brief description of the drawings
FIG. 1 shows the signal flow from the airbag control unit through the body control module to the four door latches.
FIG. 2 shows the timing diagram of the acceleration trigger, lock assertion, and switch inhibit window.

## Detailed description
The airbag control unit (20) continuously measures lateral acceleration with an internal MEMS sensor sampled at 1 kHz. When the measured value exceeds 5 g for ten consecutive samples the unit sets bit 3 of CAN message 0x1B3. The body control module (10) receives the message on its high-speed CAN transceiver (12). Firmware routine CrashLock (14) running on the 32-bit microcontroller (16) reads the message every 1 ms. If bit 3 is set the routine immediately transmits CAN message 0x2A4 with data byte 0x0F to the four door latch actuators (30, 32, 34, 36). Each actuator (30) contains a brushed DC motor (38) driven by an H-bridge (40) that moves the latch pawl (42) into the locked position. The routine also sets a 500 ms software timer (18) and masks the four interior switch inputs (44, 46, 48, 50) for the duration of the timer. After the timer expires the routine clears message 0x2A4, unmasks the switch inputs, and returns control to the normal door state machine. The 500 ms value is stored at address 0x0800F000 in flash memory and may be changed by an authenticated OTA update. In the event of a false positive the 500 ms window is short enough that a conscious occupant can still exit after the timer ends. The firmware also monitors the CAN bus health bit; if the bus reports an error the routine defaults to the locked state for safety. All timing values are stated with ±2 ms tolerance due to the 1 ms task cycle. The implementation uses 184 bytes of flash and 12 bytes of RAM.