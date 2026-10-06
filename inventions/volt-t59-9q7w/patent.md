# Airbag Roof Rail Alignment Verification System

## Abstract
A manufacturing verification system for Model 3 side curtain airbags uses torque-angle sensors on roof rail fasteners combined with a post-installation imaging station. The system detects and corrects twist before the vehicle leaves the line, ensuring compliance with FMVSS 214 and 226 without relying solely on manual inspection.

## Problem
During assembly the side curtain airbag may be secured to the roof rail with a rotational offset exceeding 15 degrees. The offset produces a twisted bag that fails to deploy in the required plane. Manual realignment at service centers occurs after the defect has already left the factory, exposing vehicles to non-compliance during side impact and ejection mitigation tests.

## Prior art
No patents were retrieved from the searches performed.

## Summary of the invention
The invention adds a torque-angle sensor to each roof rail fastener station and an overhead camera array immediately downstream. Fastener data and image analysis together flag any airbag whose mounting points deviate more than 5 degrees from nominal orientation. A robotic end effector then rotates the bag into correct alignment before the next station.

## Claims
1. A method for verifying side curtain airbag orientation on a vehicle roof rail comprising: measuring angular displacement of each mounting fastener with a torque-angle sensor during installation; capturing an image of the airbag after installation; comparing the measured angular displacement and image-derived orientation against a 5-degree tolerance; and actuating a robotic arm to rotate the airbag when the tolerance is exceeded.
2. The method of claim 1 wherein the torque-angle sensor reports data at 100 Hz and stores values for at least 30 seconds after each fastener reaches target torque of 9 Nm.
3. The method of claim 1 wherein the image is acquired by a line-scan camera positioned 800 mm above the roof rail with 0.2 mm pixel resolution.
4. The method of claim 1 further comprising logging the pre-correction and post-correction orientation values to a vehicle-specific traceability record.
5. The method of claim 1 wherein the robotic arm applies a maximum corrective rotation of 30 degrees at a controlled rate of 5 degrees per second to avoid fabric damage.
6. The method of claim 1 wherein failure to achieve alignment after two correction attempts triggers an audible and visual station alert and halts the conveyor.

## Brief description of the drawings
FIG. 1 shows the roof rail station with torque-angle sensors and overhead camera. FIG. 2 shows the robotic correction arm engaging the airbag.

## Detailed description
Roof rail (10) extends longitudinally above the side window opening. Side curtain airbag assembly (12) attaches to roof rail (10) at three points using fasteners (14). Each fastener (14) passes through a mounting tab (16) on the airbag and into a threaded insert (18) in roof rail (10). Torque-angle sensor (20) is integrated into the nut-runner spindle at each station and measures angular displacement to 0.5 degree resolution while applying 9 Nm target torque. After the third fastener reaches torque, overhead line-scan camera (22) positioned 800 mm above roof rail (10) acquires a 2048-pixel image of the airbag. Controller (24) processes the image to determine the angle of reference edge (26) on the airbag relative to roof rail datum plane (28). If the combined sensor and image data indicate twist greater than 5 degrees, controller (24) commands six-axis robot (30) whose end effector (32) grips the airbag at two non-inflatable zones. End effector (32) rotates the airbag about an axis parallel to roof rail (10) at 5 degrees per second up to a maximum of 30 degrees. After correction a second image verifies final orientation within 3 degrees. All values are written to the vehicle traceability database. If two successive corrections fail to bring the airbag within tolerance, station light (34) illuminates red and the conveyor stops. The system prevents twisted airbags from leaving the manufacturing line, eliminating the root cause of the recall condition.