# Hood Latch Position Verification System Using Redundant Microswitch Polling

## Abstract
A software-based hood latch monitoring system for vehicles that performs periodic redundant polling of primary and secondary latch microswitches after each hood open event. The system records switch states at 50 ms intervals for 2 seconds, compares against expected transition sequences, and triggers a driver alert if the unlatched state is not confirmed. Firmware implements a state machine with debounce filters and cross-checks to prevent missed detections from contact bounce or wiring faults.

## Problem
After the hood is opened and closed, the latch assembly microswitches may remain in a state that falsely indicates a latched condition even when the hood is unlatched. This occurs because the switch contacts can stick or the mechanical linkage may not fully reset the secondary latch sensor. An undetected unlatched hood can open while driving, obstructing visibility.

## Prior art
- US5763957A Vehicular trunk unlatching device having a circuit for disabling an unlatching operation: describes switch disabling for anti-theft but lacks post-open verification polling of dual hood latches.
- DE102012212542B4 DUAL FUNCTION HOOD LOCK ASSEMBLY FOR ONE VEHICLE: covers mechanical dual locks with position sensing but no software state machine for post-event confirmation.
- US20250084675A1 Lock for a motor vehicle, in particular hood or hinged-panel lock: rotary latch with release lever but no redundant polling logic after open events.

## Summary of the invention
The invention adds firmware logic in the body control module that activates a verification routine immediately after a detected hood open command. The routine samples both primary (10) and secondary (12) microswitches every 50 ms for 2 seconds, stores the sequence in a 40-element buffer, and validates against a predefined transition table. If the expected unlatched confirmation is absent, a persistent alert is set until the next verified close cycle.

## Claims
1. A method for verifying hood latch state in a vehicle after an open event, comprising: detecting a hood release signal; initiating a 2-second polling window at 50 ms intervals on primary microswitch (10) and secondary microswitch (12); storing switch states in a buffer; comparing the sequence to an expected unlatched transition pattern; and activating a driver warning if the pattern is not matched within tolerance of 2 samples.
2. The method of claim 1 further comprising applying a 3-sample debounce filter to each microswitch input before storage in the buffer.
3. The method of claim 1 further comprising cross-checking the primary and secondary switch states for consistency at each sample interval and logging a fault if disagreement exceeds 100 ms.
4. The method of claim 1 wherein the polling window is restarted if a new hood open signal is received within the current window.
5. The method of claim 1 further comprising clearing the warning only after a verified latch-close sequence is recorded in a subsequent 1-second polling window.
6. The method of claim 1 implemented in body control module firmware with non-volatile storage of the last 5 verification results for diagnostic access.

## Brief description of the drawings
FIG. 1 shows the hood latch assembly with primary and secondary microswitches and signal paths to the body control module.

## Detailed description
The hood latch assembly includes a primary microswitch (10) mounted on the primary pawl that closes when the primary striker engages. The secondary microswitch (12) is mounted on the secondary pawl and closes only when the secondary striker is fully seated. Both switches connect via separate 0.5 mm² wires to body control module (14) inputs configured as pulled-up digital inputs with 10 kΩ internal resistance.

After the release actuator (16) receives a 12 V pulse from the body control module (14) to open the hood, firmware starts a state machine in verification mode. The state machine samples inputs at 20 Hz for exactly 2000 ms, yielding 40 samples. Each sample pair is stored as a 2-bit value in a circular buffer of depth 40. A 3-sample majority debounce is applied before writing, rejecting transients shorter than 150 ms.

The expected unlatched pattern requires that within the first 10 samples both switches read open (logic 0), and that the secondary switch remains open for at least 30 consecutive samples. If the observed sequence deviates by more than 2 samples from this pattern, the module sets a diagnostic trouble code and illuminates the hood ajar warning on the instrument cluster (18).

Failure modes addressed include contact bounce (mitigated by debounce), open-circuit wiring (detected by persistent 1 state after open command), and stuck secondary pawl (detected by missing secondary-open transition). The routine runs at priority level 3 and completes within 5 ms per cycle to avoid impacting other body control tasks. All timing values and buffer sizes are stored in non-volatile memory and may be updated via OTA. Every reference numeral in this description appears in FIG. 1.