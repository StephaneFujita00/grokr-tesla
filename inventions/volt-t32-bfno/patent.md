# Torque Sensor Based Steering Wheel Fastener Retention Monitoring System

## Abstract
A system monitors steering wheel fastener torque using an integrated strain gauge sensor on the steering column interface. Firmware in the steering control module samples torque at 100 Hz, compares to 35 Nm threshold with 2 Nm hysteresis, and triggers a dashboard alert and reduced assist mode if deviation exceeds limits for more than 5 seconds. The fix addresses assembly torque variation by adding continuous verification without hardware replacement.

## Problem
The steering wheel fastener on certain 2022-2023 Model Y vehicles may be installed below the required torque specification. Understeer or vibration can cause progressive loosening, leading to decoupling between the steering wheel and column. Loss of steering input creates immediate control failure. Manual inspection at service centers catches only static conditions and cannot detect in-service relaxation.

## Prior art
- US8874320B2 Method for determining the understeering ratio of a vehicle provided with electric power steering: uses EPS motor current and angle sensors for vehicle dynamics estimation; this invention differs by applying the same sensors specifically to fastener preload monitoring rather than road handling.
- EP2572947B1 Road friction coefficient estimating unit: calculates cornering forces from steering inputs; this invention differs by focusing on static fastener retention rather than dynamic friction.

## Summary of the invention
The invention adds a torque retention algorithm to existing EPS firmware. A strain gauge (20) bonded to the steering shaft spline measures axial preload. The control unit (30) runs a state machine that logs minimum torque every ignition cycle and issues warnings if values fall below calibrated limits. No new mechanical parts are required.

## Claims
1. A steering wheel retention monitoring method comprising: mounting a strain gauge (20) on the steering shaft (12) adjacent the fastener interface, sampling output at 100 Hz, computing a moving average over 50 samples, and declaring a fault when the average deviates more than 2 Nm from the 35 Nm reference for longer than 5 seconds.
2. The method of claim 1 further comprising reducing electric power assist to 30 percent of nominal upon fault declaration.
3. The method of claim 1 further comprising storing the minimum recorded torque value in non-volatile memory at each key-off event.
4. The method of claim 1 wherein the strain gauge (20) is a 350 ohm foil gauge with 2.0 gauge factor calibrated at 25 °C.
5. The method of claim 1 wherein the control unit (30) performs a self-test of the strain gauge bridge at every power-up by injecting a 0.5 mV reference offset.
6. The method of claim 1 wherein the fault is cleared only after a service tool confirms torque restoration above 40 Nm.

## Brief description of the drawings
FIG. 1 shows the steering column assembly with integrated strain gauge and wiring to the control module.

## Detailed description
The steering shaft (12) is a 28 mm diameter steel tube with 0.8 mm wall thickness. The fastener (14) is an M14x1.5 bolt torqued to 35 Nm ±3 Nm at assembly. A foil strain gauge (20) is bonded 8 mm below the spline shoulder using epoxy rated to 150 °C. Leads route through a 3 mm groove to a connector (22) on the column housing (24). The electronic control unit (30) supplies 5 V excitation and reads differential voltage through a 16-bit ADC. Firmware applies the transfer function T = (Vout / 0.002) * 35 where T is torque in Nm. A 100 Hz interrupt updates a 50-sample circular buffer. If the buffer minimum falls below 33 Nm for five consecutive seconds the module sets DTC C1234 and illuminates the steering warning lamp. Power assist is limited to 30 percent by scaling motor current command. At key-off the lowest value is written to EEPROM. Failure modes addressed include gauge drift (self-test offset check rejects >5 percent error), wiring open (bridge voltage out of 0.5-4.5 V range triggers immediate fault), and temperature effects (compensation polynomial applied between -40 °C and 85 °C). The system requires no additional mechanical components beyond the gauge and firmware.