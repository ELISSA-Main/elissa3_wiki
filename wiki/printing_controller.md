# Tutorials Regarding the Printing Controller

When the printing controller is mentioned in the scope of this page, all the necessary components for the printing without the robotic arm are considered.

---
Table of Content:
- [Tutorials Regarding the Printing Controller](#tutorials-regarding-the-printing-controller)

---
Other useful pages:
[Launch Scenarios](run_laboratory), [Run Printing Experiments](run_printing)

---

## Printing Controller

An Arduino Mega is used as a microcontroller to foreward the command for the printing. A [_RAMPS 1.4_](https://reprap.org/wiki/RAMPS_1.4) shield is used to translate the digital outputs to commands to the fans and the extruder and get the readings from the temperature sensor. 

Currently, the Arduino is controlling the following elements:

| Function | Pin |
| - | - |
| Hotend | 10 | 
| Fan hotend | 8 |
| Fans part | 9 |
| Temperature sensor | A13 |
| Extruder steps | 36 |
| Extruder direction | 34 |
| Extruder enable | 30 |

As can be seen in the documentation of the _RAMPS 1.4_ board, it provides interfaces for two extruders (E0/E1) and motors for all three axis (X/Y/Z). The used extruder output can be easily changed by using the different pins in the [Arduino code](https://github.com/ELISSA-IRAS/elissa3_print/blob/main/misc/Arduino/Arduino_Printing_Code_2/Arduino_Printing_Code_2.ino). Furthermore the hotend and different fans can be connected. A detailed documentation is provided in the _RAMPS 1.4_ wiki page. 
