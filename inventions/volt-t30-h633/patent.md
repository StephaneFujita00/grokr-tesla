# Camera Feed Watchdog And Recovery System For Vehicle Infotainment

## Abstract
A software-based watchdog monitors the rearview camera feed process on FSD computer 4.0. If the feed stalls for more than 200 ms during reverse, the system restarts the camera pipeline within 300 ms while preserving vehicle state. The fix prevents display loss without hardware changes.

## Problem
Software instability in versions 2023.44.30 to 2023.44.100 on FSD computer 4.0 can cause the rearview camera image process to hang. When the vehicle is shifted into reverse the display remains blank, reducing driver visibility and increasing crash risk. The official remedy was an OTA update; therefore a firmware-level software mechanism is required.

## Prior art
- US12325434B2 Vehicle intelligent unit: describes general vehicle control units but does not monitor or recover camera display processes on FSD hardware.
- CN116208805A Failsafe surround view: provides camera redundancy but lacks a dedicated watchdog timer tied to reverse gear state for single rear camera recovery.

## Summary of the invention
The invention adds a dedicated camera watchdog task (20) running at 50 Hz on the infotainment CPU. It samples a heartbeat counter (22) incremented by the camera feed thread (24). When reverse is detected via gear position sensor (26) and heartbeat stalls beyond 200 ms, the watchdog issues a restart command to the camera pipeline (28) while logging the event and maintaining steering and brake functions.

## Claims
1. A method for recovering a stalled rearview camera feed on a vehicle infotainment system comprising: monitoring a heartbeat counter (22) updated by a camera feed thread (24) at least every 50 ms; detecting a reverse gear state from gear position sensor (26); and restarting the camera pipeline (28) if the heartbeat does not update within 200 ms while the vehicle is in reverse.
2. The method of claim 1 wherein the restart completes within 300 ms and the prior vehicle control state is preserved.
3. The method of claim 1 further comprising logging the stall event with timestamp and thread ID to non-volatile memory.
4. The method of claim 1 wherein the watchdog task (20) runs on a separate core from the camera feed thread (24) with priority above 80.
5. The method of claim 1 wherein the camera pipeline (28) is restarted by sending a SIGUSR1 signal followed by a 100 ms grace period before forced termination if needed.
6. The method of claim 1 wherein the system disables the recovery action if vehicle speed exceeds 5 km/h in reverse to avoid unnecessary resets during parking maneuvers.

## Brief description of the drawings
FIG. 1 shows the software architecture and data flow between the watchdog task, camera feed thread, and hardware interfaces.

## Detailed description
The camera watchdog task (20) executes on core 3 of the infotainment CPU at 50 Hz with scheduling priority 85. It reads the heartbeat counter (22) maintained by the camera feed thread (24). The camera feed thread (24) increments the counter every frame received from the rear camera via MIPI CSI-2 interface. Gear position sensor (26) provides a digital signal updated every 20 ms. When gear position sensor (26) indicates reverse and the difference between current time and last heartbeat update exceeds 200 ms, the watchdog issues a restart. The restart sequence sends SIGUSR1 to camera pipeline process (28), waits 100 ms, then checks for new frames. If no frame arrives within 300 ms total, the process is terminated and relaunched with the same command line arguments and shared memory buffers. Vehicle speed from wheel speed sensors must remain below 5 km/h or the recovery is skipped. All events are written to a 4 kB ring buffer in eMMC with 1 ms timestamp resolution. Failure mode of repeated stalls triggers a fallback to ultrasonic sensor overlay on the display after three restarts within 60 s. The mechanism adds less than 2% CPU load and uses existing 512 MB shared memory region. All numeric values match the claims exactly.