# Installation

This page offers a tutorial on a ROS setup as required for the operation and development of the ELISSA environment.
---

Table of Content:
- [Installation](#installation)
  - [Installing ROS](#installing-ros)
  - [Setting up a catkin Workspace](#setting-up-a-catkin-workspace)
  - [Adding ELISSA repositories](#adding-elissa-repositories)
  - [Network Configuration](#network-configuration)
  - [Setting up VSCode](#setting-up-vscode)
  - [Installing additional ROS Packages](#installing-additional-ros-packages)

---

## Installing ROS

**DISCLAIMER** Beware that the ROS installation is more complicated for newer versions of Ubuntu and may cause packages to break. It is therefore strongly recommended to use Ubuntu 20.04. **Using a newer version of Ubuntu will likely cause many, many issues!!!**

### Standard Installation on Ubuntu 20.04

This is the standard ROS installation with bash setup included. 

Currrent ROS version : NOETIC

1. The suggested operating system for ROS is Linux (more specifically the Ubuntu or Debian distributions) so make sure to have it installed in your machine. There are experimental versions avaiable for Windows and Arch Linux. Refer to the ROS documentation for further information on experimental versions. 

> Beware that the ROS installation is more complicated for newer versions of Ubuntu. It is recommended to use Ubuntu 20.04. If you want to use a newer version see the guide below.

2. Configure your Ubuntu repositories to allow "restricted," "universe," and "multiverse."
Do this by going into your "Software & Updates" application under the Ubuntu Software Tab and checking all required boxes. 

<br> <img src="wiki/graphics/Software Sources.png" alt="Software Sources" width="800">

3. Update your Sources List to accept software from packages.ros.org by entering the following command:

```shell
sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
```

4. Set up your keys by entering the following commands:

```shell
sudo apt install curl # if you haven't already installed curl
curl -s https://raw.githubusercontent.com/ros/rosdistro/master/ros.asc | sudo apt-key add -
```

5. Update your system before the installation

```shell
sudo apt update
```

6. Now start the full ROS installation with the following command. See [the ROS installation Guide](http://wiki.ros.org/noetic/Installation/Ubuntu) for more detailled information on different installation commands. The here provided command installs the full ROS desktop package.

```shell
sudo apt install ros-noetic-desktop-full
```

7. Now all thats left is to format your bash terminal to operate in the ROS environment. The following command formats the bash terminal once.

```shell
source /opt/ros/noetic/setup.bash
```

If you want to automatically source this script every time a new terminal is launched use the following commands once. 

```shell
echo "source /opt/ros/noetic/setup.bash" >> ~/.bashrc
source ~/.bashrc
```
8. Check whether your installation was successfull by running
```shell
roscore
```

ROS is now succesfully installed on your workstation. You can see the following tutorials on how to set up a catkin workstation and how to clone the ELISSA repos to finallize your setup.

### ROS Installation on Ubuntu 22.04

This guide is based on [this repository](https://github.com/lesaf92/ros_noetic_ubuntu22/blob/main/README.md?plain=1).

1. Install utils
```shell
sudo apt-get install htop python3-pip net-tools curl python3-pil python3-pil.imagetk
```
2. Install mamba
```shell
curl -L -O "https://github.com/conda-forge/miniforge/releases/latest/download/Mambaforge-$(uname)-$(uname -m).sh"
bash Mambaforge-$(uname)-$(uname -m).sh
```
3. Install and configure robostack
```shell
mamba create -n ros_env python=3.9 -c conda-forge
mamba activate ros_env
conda config --env --add channels robostack-staging
# remove the defaults channel just in case, this might return an error if it is not in the list which is ok
conda config --env --remove channels defaults
mamba install ros-noetic-desktop-full
mamba install catkin_tools
mamba install rosdep
rosdep init
rosdep update
```
4. Put at the end of your `bashrc` file
```shell
conda deactivate
conda activate ros_env
```

5. Reopen your terminal to enforce the before defined shell rules. Now check whether the installation was successful by running

```shell
roscore
```
--- 

## Setting up a catkin Workspace

To create a catkin workspace that holds all code and helps to build the project use the following commands.
```shell
mkdir -p ~/catkin_ws/src
cd ~/catkin_ws/src
catkin_init_workspace
cd ~/catkin_ws
catkin_make
echo "source ~/catkin_ws/devel/setup.bash" >> ~/.bashrc
source ~/.bashrc
```

## Adding ELISSA repositories

To be able to launch all scenarios in the ELISSA environment a multitude of ROS packages are required. These can be found in the ELISSA Git and should be cloned into the catkin_ws.
Clone all required repositories into the src folder.
The required Repositories are:
- elissa3
- elissa3_drap
- elissa3_estop
- elissa3_fad
- elissa3_gazebo
- elissa3_gnc
- elissa3_gui
- elissa3_hamilcar
- elissa3_hamilcar_OBS
- elissa3_hannibal
- elissa3_mvm
- elissa3_print

## Network Configuration

tbd

## Setting up VS Code

tbd

## Adding additional ROS Packages

tbd
