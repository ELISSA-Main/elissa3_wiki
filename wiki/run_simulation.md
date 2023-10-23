# Run the Simulation

tbd

## Single Freeflyer

tbd

## Multiple Freeflyer

tbd

## Docking Scenario

The launch file for a docking scenario experiment is setup for simulation by default.
Open a terminal session and run:

```shell
roslaunch elissa3 docking.launch
```
This will automatically start the launch cascade. An RViz visualization will pop up with the Chaser and the Target spawned and their specified spawn points.
The **Final Approach and Docking Operations Gui** will also be launched automatically. The docking scenario is fully controlled through this GUI.
For details on the launch default refer to the docking.launch file.
Final Approach and Docking (FAD) specific parameters, such as approach velocities and final seperations after maneuver phases, can be set using the *fad_params.yaml* file.
This file is located in *elissa3_fad/params/*.

<!-- TODO Add image of GUI and simulation -->
<!-- TODO add some of the defaults -->


## Printing Scenario

tbd

## Mission and Vehicle Management
