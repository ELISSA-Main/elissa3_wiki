# End Operations

To finish the operations in the laboratory some major steps must be followed. This pages describes the necessary steps.

## Shut down Robot Arm

The following steps must only be followed if the printer was used.
- [ ] Use the following command to disable the heating element in the printer:
    - rostopic pub /arduino/hot_end_temp std_msgs/Float32 "data: 0"
- [ ] Disable the extruder:
    - rostopic pub /arduino/extrude_distance std_msgs/Float32 "data: 0"
- [ ] Monitor the hotend temperature
    - rostopic echo /arduino/actual_temp
- [ ] Wait until the temperature falls below 40°C
- [ ] Turn off both fans:
    - rostopic pub /arduino/fan_hotend std_msgs/Bool "data: false"
    - rostopic pub /arduino/fan_part std_msgs/Bool "data: false"
     
## Shut down Table and Freeflyers

- [ ] In Inverter click "An/Aus" to disable the blowers
- [ ] Close all command windows that have rosrun or roslaunch operations running
- [ ] Shut down the freeflyers
- [ ] Close the windows in the laboratory and the blower room
- [ ] Shut down the blowers in the basement
- [ ] Shut down LAN
- [ ] Don't forget to add your experiment to the protocoll int the control room
