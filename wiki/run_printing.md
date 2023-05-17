# Run Printing Experiments

## Start a Printing Operations

Before starting the printing operation:
- Generated a truss **tbd**
- Prepared ELISSA laboratory for operation (see [here](begin_operation))
- Placed the freeflyer next to the printing table
Launch the printing package:
```bash
roslaunch elissa3_print hannibal_print_single.launch ...
```
Move the robot arm above the table:
```bash
rostopic pub /MecademicRobot_command std_msgs/String "MoveJoints(0,30,0,0,-30,90)"
```
Move the robot arm closer to the table top:
...
Run the printing node to forward the commands:
```bash
...
```
## Abort / Stop a Printing Operation

Set the hotend temperature to zero: 
```bash
rostopic pub /arduino/hotend_temp "data: 0"
```
Set the extruber distance to zero to stop the motor:
```bash
rostopic pub /arduino/extruder_distance "data: 0"
```
Wait for the hotend temperature to be below 40°C before proceeding. Monitor the temperature with:
```bash
rostopic echo /arduino/actual_temp
```
Before shutting the active `roslaunch` and `rosrun` commands, deactivate the fans with:
```bash
rostopic pub /arduino/fan_hotend "data: false"
rostopic pub /arduino/fan_part "data: false"
```