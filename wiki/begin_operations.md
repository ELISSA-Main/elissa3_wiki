# Begin Operations

To run the operations in the laboratory some major steps must be followed. This pages describes the necessary steps.

---
Table of Content:
- [Begin Operations](#begin-operations)
	- [Preparation](#preparation)
	- [Run the Software](#run-the-software)
	- [Freeflyer](#freeflyer)
	- [Operation](#operation)
- [Appendix](#appendix)
	- [Settings for the Blower Control](#settings-for-the-blower-control)
	- [Activate Hannibal Class Freeflyers](#activate-hannibal-class-freeflyers)
 
---
Other useful pages:
[Launch Scenarios](run_laboratory), [End Operations](end_operations)

---

## Preparation

- [ ] Open at least two windows in the laboratory
- [ ] Turn the LAN switch in the control room on
- [ ] Start the windows and the linux computer
- [ ] Activate the blowers in the basement
- [ ] Open a window in the blower room as well

## Run the Software

- [ ] Launch the calibrated MotiveTracker software (on the windows computer)
- [ ] Calibrate MotiveTracker using the existing manual
- [ ] Open Calibration File, than click "View" and than "Assets"
- [ ] Activate the blower control
	- Open Inverter twice, once for each half of the table
	- Click "Steuerung"
	- Set "Digitaleingang" to 1 and "Sollwert" to 60Hz
	- COM5: Left side of the table
	- COM3: Right side of the table

## Freeflyer

- Hamilcar Class
	- [ ] Check the battery charge (all > 7.6V)
	- [ ] Installing and connecting the battery (**Attention**: Motors may be active now)
- Hannibal Class
	- [ ] Check the battery charge (all > 27V)
		- Make sure the display is facing you and the red cable is on the right
	- [ ] Installing and connecting the battery
	- [ ] Activate the freeflyer (**Attention**: Motors may be active now)
	- [ ] Activate the flight computer

- [ ] Place the freeflyer on a glass plate on the table
- [ ] If necessary, add the freeflyer in the MotiveTracker software
	- [ ] Select the four markers (in square layout) on top of the freeflyer
	- [ ] Create a rigid body
	- [ ] Name the rigid body like *vrpn/hannibal*
	- [ ] Select the other markers and add them to the rigid body

## Operation

- [ ] Launch the wanted roslaunch file
- [ ] Activate the necessary blowers
	- Click "An/Aus" to activate blower

# Appendix

## Settings for the Blower Control

tbd

## Activate Hannibal Class Freeflyers

- [ ] Make sure the freeflyer is placed in the middle of the glass plate
- [ ] Activate PCDU
- [ ] Activate on board computer by holding the innermost red button for one second
- [ ] If necessary activate robot arm
