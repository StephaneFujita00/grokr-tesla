# Redundant Reverse Lamp Wiring Monitor and Switchover for Model Y

## Abstract
A wiring harness for vehicle reverse lamps incorporates a primary conductor pair and a parallel secondary conductor pair connected at the body control module output. A current sensing comparator monitors voltage drop across a 0.05 ohm shunt in the primary path. When primary current falls below 1.2 A for more than 200 ms while reverse gear is selected, a solid-state relay switches to the secondary path. The system logs the event via CAN and illuminates a dash indicator. All components are rated for 12 V automotive environment, -40 C to 85 C, IP67.

## Problem
Reverse lights may fail to illuminate due to an open circuit or high-resistance joint in the reverse facia harness. The single-point wiring path between the body control module and the rear lamps provides no alternate route, violating FMVSS 108 when the fault occurs. Replacement of the entire harness addresses the symptom but does not prevent recurrence from vibration or connector corrosion.

## Prior art
- US7932623B2 Method and system for driving a vehicle trailer tow connector: uses solid-state drivers for trailer circuits but provides no parallel path or automatic switchover for primary lamp failure.
- US7967617B2 Trailer tow connector assembly: describes interface electronics between connectors and vehicle bus but does not monitor or reroute power to redundant lamp wiring.
- CN111585130B Semi-trailer and its wiring harness: discloses main and branch harnesses for trailers without real-time current monitoring or automatic failover.

## Summary of the invention
The invention adds a parallel secondary conductor set and an automatic failover circuit inside a sealed module mounted adjacent to the rear fascia connector. A microcontroller continuously compares primary current against a threshold derived from lamp specification. Upon detection of primary path failure the module energizes a MOSFET relay to transfer load to the secondary conductors while maintaining compliance with lamp intensity requirements.

## Claims
1. A vehicle reverse lighting system comprising a body control module output connected to a primary conductor pair (14) having a series shunt resistor (16) of 0.05 ohm, a secondary conductor pair (18) connected in parallel at the module output, a current sense amplifier (20) measuring voltage across the shunt, a microcontroller (22) that activates a solid-state relay (24) when measured current remains below 1.2 A for more than 200 ms while reverse gear signal is active, and a CAN transceiver (26) that transmits a diagnostic trouble code upon activation.
2. The system of claim 1 wherein the solid-state relay (24) is a 40 V, 30 A N-channel MOSFET with on-resistance less than 5 milliohm.
3. The system of claim 1 wherein the primary and secondary conductor pairs each consist of 18 AWG stranded copper wire with cross-linked polyethylene insulation rated 125 C.
4. The system of claim 1 further comprising a dashboard tell-tale that illuminates when the relay (24) is closed.
5. The system of claim 1 wherein the microcontroller (22) samples current at 100 Hz and applies a 200 ms moving average filter before threshold comparison.
6. The system of claim 1 wherein the module enclosure meets IP67 and is mounted with vibration isolation grommets having durometer 50 Shore A.

## Brief description of the drawings
FIG. 1 shows the wiring module and harness routing in the rear fascia area with leader lines to all reference numerals.
FIG. 2 shows the internal schematic of the failover module including shunt, amplifier, microcontroller, and relay.

## Detailed description
The body control module (BCM) reverse output terminal connects to primary conductor pair (14) that runs 2.8 m to the left and right reverse lamp assemblies. A 0.05 ohm shunt resistor (16) is placed in series on the positive leg of the primary pair inside the failover module housing (12). The voltage developed across shunt (16) is amplified by current sense amplifier (20) with gain of 50 and fed to the 12-bit ADC input of microcontroller (22). When the vehicle is placed in reverse the BCM asserts a 12 V signal on the reverse gear sense line (28). Microcontroller (22) enables sampling and compares the filtered current value to the 1.2 A threshold. If the filtered current remains below threshold for 200 ms the microcontroller drives the gate of solid-state relay MOSFET (24) high, connecting secondary conductor pair (18) to the lamp load. Secondary pair (18) is routed in a separate bundle 40 mm away from the primary pair to avoid common-mode damage. Both conductor pairs terminate at a sealed four-pin connector (30) on the fascia. The microcontroller also asserts a CAN message containing DTC C1234 on the vehicle bus, causing the instrument cluster to illuminate the reverse lamp fault tell-tale. The module is potted with silicone gel inside an aluminum housing (12) measuring 80 mm x 60 mm x 25 mm and secured with two M6 bolts torqued to 8 Nm. The design tolerates a single open circuit anywhere in the primary path between the BCM and the lamps while still delivering at least 2.1 A to each 21 W reverse lamp at 13.5 V supply. In the event of simultaneous failure of both paths the system reverts to no illumination and sets a second DTC. All timing values and current thresholds are stored in non-volatile memory and can be updated via diagnostic tool.