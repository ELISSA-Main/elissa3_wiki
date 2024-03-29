# Run the Astrobee Simulation

This page focuses on running the Astrobee simulator in relation to ELISSA.
Detailed information on running the default Astrobee simulator is available at the NASA Astrobee GitHub pages documentation: [NASA Astrobee Robot Software](https://nasa.github.io/astrobee/v/master/index.html)

The simple basic launch command for non-NASA users is:
```shell
roslaunch astrobee sim.launch dds:=false robot:=sim_pub rviz:=true
```

Table of Content:
- [Run the Astrobee Simulation](#run-the-astrobee-simulation)
  - [Running Astrobee/ELISSA Simulations](#running-astrobeeelissa-simulations)

---

## Running Astrobee/ELISSA Simulations

Right now their is only the RAGGA related simulation related to Astrobee/ELISSA combined simulations.
The simulation is still **Work in Progress**

To run the simulator open a terminal session and enter:
```shell
roslaunch elissa3_astrobee sim_elissa.launch
```

By default the Final Approach Operations GUI will be launched. 
This GUI differs from the standard ELISSA version as it has been adapted for the Astrobee 6-DoF environment.
If your screen resolution is full 1080p or lower, the GUI will be to large to display correctly.
Adding the appropriate flags to the launch command, will launch a GUI with scrollbars to resolve this issue:
```shell
roslaunch elissa3_astrobee sim_elissa.launch fad_ops_gui:=false fad_ops_gui:=true
```