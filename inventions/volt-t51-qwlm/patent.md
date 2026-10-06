# Redundant Seat Belt Reminder Logic Verification in Vehicle Control Software

## Abstract
A software method verifies seat belt status signals in vehicle ECUs by running dual independent logic paths and cross-checking outputs every 100 ms. If mismatch or missing chime occurs for unbelted driver, a fallback audible tone activates via separate audio channel. Handles sensor faults and ignition state transitions.

## Problem
The seat belt warning system relies on a single software path to monitor driver occupancy via seat sensor and buckle switch. In certain conditions the logic fails to trigger the light and chime per FMVSS 208 requirements, leaving the driver unalerted.

## Prior art
No patents returned from searches.

## Summary of the invention
The invention adds a secondary verification module in the body control module firmware. Primary path processes occupancy and buckle inputs. Secondary path runs identical algorithm on duplicated signals. Comparator detects discrepancy and forces warning state. Audio output routes through independent DAC to bypass main chime failure.

## Claims
1. A method in a vehicle electronic control unit for seat belt reminder comprising: receiving driver occupancy signal from seat pressure sensor (12) and buckle switch state (14); executing primary logic module (20) to determine warning condition within 500 ms of ignition on; executing secondary logic module (22) on duplicate inputs; comparing outputs of modules (20) and (22) every 100 ms; activating visual indicator (30) and audible chime (32) via primary audio path if either module indicates unbelted driver; and activating fallback tone (34) on secondary audio channel if outputs mismatch or primary chime absent for more than 200 ms.
2. The method of claim 1 wherein the secondary logic module (22) uses a 50 ms debounce filter on buckle switch (14) different from the primary debounce of 100 ms.
3. The method of claim 1 further comprising logging mismatch events to non-volatile memory with timestamp and sensor values for diagnostic retrieval.
4. The method of claim 1 wherein fallback tone (34) uses a 2 kHz square wave at 80 dB for 6 seconds repeating until belted or ignition off.
5. The method of claim 1 wherein the comparator (24) resets warning state only after both modules agree belted for three consecutive 100 ms cycles.
6. The method of claim 1 applied during low voltage conditions below 10 V by using watchdog timer (26) to force fallback activation.

## Brief description of the drawings
FIG. 1 shows the dual logic paths and signal flow from sensors to actuators with comparator.

## Detailed description
Driver seat pressure sensor (12) outputs analog voltage 0.5-4.5 V proportional to 10-100 kg load with tolerance +/-5%. Buckle switch (14) is normally open, closing on latch with 12 V signal. Both feed primary logic module (20) and secondary logic module (22) inside body control module. Primary module applies 100 ms debounce then checks occupancy above 30 kg and buckle open to set warning flag. Secondary module applies 50 ms debounce on same inputs. Comparator (24) samples flags every 100 ms. If flags differ or warning flag set but no chime output detected via feedback line (28) for 200 ms, comparator enables fallback tone generator (34) on secondary DAC channel. Visual indicator (30) is instrument cluster LED driven directly by either module. Watchdog timer (26) monitors 12 V rail and forces fallback if voltage drops below 10 V for 50 ms. Failure mode of single module hang is covered by independent execution on separate CPU cores. Mismatch log stores 50 events with 32-bit timestamp and raw sensor values. All timing values match those in claims. Reference numerals appear in FIG. 1.