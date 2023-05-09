# System Overview

The main part of the ELISSA system is the air bearing table. It provides a planar surface and air cushion for the freeflyer to move with reduced friction. The system is developed to recreate an on-orbit environment with low residual acceleration, low illumination and a motion capture system as a GPS equivalent. The system can be used in an simulation environment or the laboratory environment. The first can be used for the general ELISSA scope and some packages, but not all features are included in the simulation. 

In this chapter, the different aspects of the system are described. For tutorials on how to use the system look in the [user guides](user_guides) section. The following chapter describes these elements:

- [System Overview](#system-overview)
  - [Lab Environment](#lab-environment)
  - [Freeflyer Classes](#freeflyer-classes)
    - [Hannibal Class](#hannibal-class)
    - [Hamilcar Class](#hamilcar-class)
  - [Simulation Environment](#simulation-environment)
  - [Experiment Types](#experiment-types)
  - [Package Structure](#package-structure)

## Lab Environment

The laboratory environment of the ELISSA system consists of the four subsystems:

* Aeromechanical subsystem
* Motion tracking subsystem
* Freeflyer subsystem
* Mission control subsystem

The laboratory room with the air bearing table is shown in the image below. The table constructed of different panels. The dimensions of the table and these panels is shown in the table below. An air cushion is created between the freeflyer and the table using the two blowers in the basement. Each blower supplies air to one half of the table (split at x=3,5 m). This allows the operator to use only one halve of the table. This reduces the necessary energy to run the table and is recommended, if it is not required to use the complete testbed. The blowers and the table are the aeromechanical subsystem.

| | length (x) | width (y) |
| - | :-: | :-: |
| Table | 7 m | 4 m |
Small panel | 1,75 m | 0,8 m |
Large panel | 2,33 m | 0,8 m |

![The lab environment](graphics/elissa_tisch.jpg)

In the image above are two freeflyers shown. These are the satellite mockups operating on the table. They are described in detail in the next section. The position of the freeflyers is tracked using the motion tracking system. Multiple cameras are placed in the room overlooking the complete tested. These cameras detect the markers, which are placed on the freeflyers. In the tracking software, the corresponding markers are assigned to a freeflyer to get its position.

This is happening in the fourth subsystem, the mission control subsystem. The control room is visible in the picture above behind the glass window. At least two computers are used to run the software necessary for the laboratory operations. *Windows* is running on the first computer to run the following programs:

- *INVERTER* to control the blowers
- *Motive* to use the motion tracking system

An introuction on how to use the software is given in the [Tutorial](user_guides/run_laboratory.md) section of the wiki. The other computer is runnung *Ubuntu 20.04* to provide the [ROS](overview/ros.md) infrastructure. Most of the necessary code to control the freeflyers and run mission specific code is executed on this machine. 

## Freeflyer Classes

The freeflyers are the satellite mockups operating on the ELISSA table. As real satellites, the freeflyers need different subsystems to function. The general systems are very similar between the different flyers. The all have a:

- Propulsion module
- Service module

Furthermore each freeflyer can use mission specific payloads. The concrete details of each module differ depending on the freeflyer class. At the moment two freeflyer classes are used on the ELISSA testbed:

- *Hannibal* class freeflyers
- *Hamilcar* class freeflyers

A complete list of all freeflyers is given in the table below. A detailed description of each freeflyer class is provided in the next section.

| Name | Class | Status | Description |
| - | - | - | - |
| Hannibal | Hannibal | Operational | First freeflyer of the hannibal class, mainly used for printing and docking experiments |
| Pegasus | Hannibal | Operational | Second freeflyer of the hannibal class, mainly used for IMU development |
| Hamilcar | Hammilcar | Not oeprational | Freeflyer of the hamilcar classed, redesigned in 2021 |
| Red Five | Hammilcar | Not oeprational | Freeflyer of the hamilcar classed, redesigned in 2021 |

### Hannibal Class

The Hannibal freeflyer is the second freeflyer used within the ELISSA testbed. It consists of several modules that can easily be stacked upon each other. The figure below shows Hannibal in the printing configuration, consisting of a propulsion module (bottom), the service module (middle) and the printing module (top).  

![The Hannibal freeflyer](graphics/hannibal.jpg)

> A redesign of the Hannibal class freeflyers was conducted to reduce the weight and optimize the freeflyers. This new design is used for Pegasus and it is planned to changed Hannibal as well, when it is not needed. 



### Hamilcar Class

## Simulation Environment

tbd

## Experiment Types

tbd

## Package Structure

tbd