# Run Printing Experiments

## Start a Printing Operations

Before starting the printing operation:
- Generated a truss **tbd**
- Prepared ELISSA laboratory for operation (see [here](begin_operation))
- Placed the freeflyer next to the printing table
Launch the printing package:
```bash
roslaunch elissa3_print hannibal_print_single.launch lab_mode:="true" pid_ctl:="true" smc_ctl:="false" robot:="true" printhead:="true" eso:="false"
```
Optional arguments:
- force (boolean): Use the force sensors in the chaser docking module
- printhead (boolean): Enable the heating of the printhead (if disabled, see commands below)
Move the robot arm above the table:
```bash
rostopic pub /MecademicRobot_command std_msgs/String "MoveJoints(0,30,0,0,-30,90)"
```
Move the robot arm closer to the table top:
```bash
rostopic pub /MecademicRobot_command std_msgs/String "MoveLinRelWRF(0,0,-2.5,0,0,0)" 
```
The third value is the distance in the z-direction and can be used to move the robot arm closer to the table.
...
Run the printing node to forward the commands:
```bash
rosrun elissa3_print print_trajectory.py __ns:=hannibal _sat_name:="hannibal"
```
Open the teleop client:
```bash
rosrun elissa3_print teleop_cli_print.py
```
The following commands are necessary to start the printing operation:
- T: Get to the printing menu
- C: Load a csv file (enter the path, i.e. _cd /home/elissa/catkin_ws/src/elissa3_print/misc/Trajectories/Compensation_data.csv_)
- S: To start the setup (printhead is heated)
- R: Run the trajectory and start the print
Monitor the hotend heat with the following command in another terminal:
```bash
rostopic echo /arduino/actual_temp
```
## Abort / Stop a Printing Operation

Set the hotend temperature to zero: 
```bash
rostopic pub /arduino/hot_end_temp std_msgs/Float32 "data: 0"
```
Set the extruber distance to zero to stop the motor:
```bash
rostopic pub /arduino/extrude_distance std_msgs/Float32 "data: 0"
```
Wait for the hotend temperature to be below 40°C before proceeding. Monitor the temperature with:
```bash
rostopic echo /arduino/actual_temp
```
Before shutting the active `roslaunch` and `rosrun` commands, deactivate the fans with:
```bash
rostopic pub /arduino/fan_hotend std_msgs/Bool "data: false"
rostopic pub /arduino/fan_part std_msgs/Bool "data: false"

## Appendix

[Link to the motor controller board](https://reprap.org/wiki/RAMPS_1.4)
```
