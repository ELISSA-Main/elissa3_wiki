# Control system for Hannibal and Meca500 with simulation-based tuning
This tutorial explains how the control algorithm of the hannibal freeflyer is implemented, to stay in the pose while the robot arm is moving. The first part relates to the software development neccessary to have package/module to establish the computational simulation environment to perform controller's parameters tuning.
## Objective
During the robot arm's operation, reaction forces from the robot arm movements cause the freeflyer to move undesirably. Therefore, the simulation-tuned controller for the freeflyer is designed to manage the reaction forces occurred from the operations and keep the freeflyer in the specified position.   

## Package
`elissa3_nncs` package consists of the development of Gazebo simulation environment where the meca500 r3 robot arm is attached to the hannibal freeflyer.
<img width="740" height="745" alt="image" src="https://github.com/user-attachments/assets/16ff48d5-42f6-4d49-aa18-60f14785f45d" />
## Gazebo Simulation Environment

We use gazebo to simulate the lab environment (ELISSA), in which we can virtually interact with the robots and observe the data such as the position of the freeflyer, joint angles of the robot arm, etc. 
The following figure shows the overall workflow of the simulation environment. 
<img width="1531" height="446" alt="image" src="https://github.com/user-attachments/assets/1e593306-6979-487a-b7cc-aa7149c54805" />


In the simulation environment, we can give commands to the robot arm via `moveit` module, which takes desired end-effector position alongside current arm joint angles and output the command of the corresponding trajectory. After that, hardware interface module `meca_hw_interface` takes the trajectory and publish commands of joint angles in string format as:
```'MoveJoints(angle1, angle2, angle3, angle4, angle5, angle6)'``` where all angles are defined in degree. This string is also to be used with the meca500. Then, the real robot arm PID controller takes these inputs and control joints to the calculated positions, whereas in the simulated robot arm PID controller, we need to firstly implement the string parser `meca500_movejoints_parser.py` such that the `libgazebo_ros_control` can read the joint angles.  

The following figure shows the high-level workflow of the lab environment.
<img width="1380" height="485" alt="image" src="https://github.com/user-attachments/assets/13eb300f-5cbd-4106-959e-eb3d5446f643" />

Remarks:
1. The real PID values of the robot arm is unknown and must be **identified** (gray box) to accurately tune the controller of the freeflyer in the simulation environment (For now, this is PID).
2. The individual link's inertias of the meca 500 is estimated and may not be accurated (elissa3_ws/src/elissa3_ram/elissa3_ram_legacy/urdf/meca_500_r3_with_inertia.urdf.xacro).
3. Using full detailed model of the freeflyer cause substantially drop in FPS. Set flag `ff_simple` to `true` to use the simplified model of the freeflyer in the robot simulation.
4. Red boxes represent the part which we need to take care of in the next step such as implementing and tuning the controller and its parameters.
## Launching the simulation
Run the following command in the terminal.
```shell
roslaunch elissa3_nncs hannibal_meca_plan.launch sim_mode:=true
```
## Launching the module with the real robot arm
```shell
roslaunch elissa3_nncs hannibal_meca_plan.launch lab_mode:=true
```
