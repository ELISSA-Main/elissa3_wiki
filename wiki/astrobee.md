# Astrobee

This page provides a short overview on the Astrobee ROS framework and information on installing the ROS Astrobee Flight Softwares (AFS).

Detailed information on Astrobee including setup and usage is available through their GitHub pages documentation: [NASA Astrobee Robot Software](https://nasa.github.io/astrobee/v/master/index.html)

---

Table of Content:
- [Astrobee](#astrobee)
  - [Installing AFS](#installing-afs)
    - [Preparations](#preparations)
    - [Clone and build AFS](#clone-and-build-afs)
  - [Adding ELISSA Repositories](#adding-elissa-repositories)
  - [Setup the Simulation Environment](#setup-the-simulation-environment)
    - [Activate the NAV cam](#activate-the-nav-cam)
    - [Replace the Astrobee FF model](#replace-the-astrobee-ff-model)
    - [Replace the ISS RViz configuration file](#replace-the-iss-rviz-configuration-file)
    - [Replace the PMC mesh](#replace-the-pmc-mesh)
    - [Change the PMC skin of Bumble](#change-the-pmc-skin-of-bumble)

---

## Installing AFS

**DISCLAIMER** This assumes that you have already setup Ubuntu 20.04., ROS Noetic and ELISSA on your machine.
In this case you will not have to reinstall ROS, simply follow these steps:

### Preparations

1. Create a new Ubuntu user account
2. Generate a new SSH key for your new account, detailed instructions can be found here: [Generate SSH Key](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)
3. Add the SSH key to your GitHub account, detailed instructions can be found here: [Add SSH Key to GitHub Acc](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account)

### Clone and build AFS 

Next, begin with the installation of the AFS. This is a condensed version of the more detailed guide provided by NASA.
For most of our use cases we will also not require the Astrobee Android submodule.
The Astrobee GitHub repository can be found here: [Astrobee repository](https://github.com/nasa/astrobee).
Detailed information on installation for non-NASA users can be found here: [Install for general users](https://nasa.github.io/astrobee/v/master/install-nonNASA.html)

1. Open a new terminal session and first make sure your system is up-to-date:
```shell
sudo apt-get install build-essential git
```
2.  Export the Astrobee install path:
```shell
export ASTROBEE_WS=$HOME/astrobee
```
3. Clone the AFS and add the media submodule:
```shell
git clone git@github.com:nasa/astrobee.git $ASTROBEE_WS/src
pushd $ASTROBEE_WS/src
git submodule update --init --depth 1 description/media
popd
``` 
4. Update your system, just in case:
```shell
sudo apt-get update
sudo apt-get upgrade
```
5. Install dependencies:
```shell
pushd $ASTROBEE_WS
cd src/scripts/setup
./add_ros_repository.sh
sudo apt-get update
cd debians
./build_install_debians.sh
cd ../
./install_desktop_packages.sh
sudo rosdep init
rosdep update
popd
```
Some errors might pop up informing you about packages that could not be found. This can be ignored as they are for NASA interal use only.
6. Prepare for building the AFS:
```shell
pushd $ASTROBEE_WS
./src/scripts/configure.sh -l -F -D
source ~/.bashrc
popd
```
7. Build the AFS:
```shell
pushd $ASTROBEE_WS
catkin build
popd
```
8. If your system is running out of memory try building with the **-j1** flag to prevent the build command running in multiple tasks in parallel:
```shell
pushd $ASTROBEE_WS
catkin build -j1
popd
```
9. Now all thats left is to format your bash terminal to operate in the ROS environment and setup automatic sourcing.
```shell
echo "source /opt/ros/noetic/setup.bash" >> ~/.bashrc
echo "source ~/astrobee/devel/setup.bash" >> ~/.bashrc
source ~/.bashrc
```

## Adding ELISSA Repositories

Since ELISSA and Astrobee are both ROS (Noetic) frameworks, code developed for ELISSA can be migrated and integrated into the Astrobee framework.
Note, however that this should not be done with repositories from main ELISSA organization, as the code will require some modifications for 
Astrobee integration. There is a dedicated ELISSA organization on GitHub concerned with ELISSA-Astrobee migration: [RFT-RAGGA](https://github.com/RFT-RAGGA)
Follow these simple steps:
1. Open a terminal session, change into the Astrobee src directory and add ELISSA repo as a submodule:
```shell
cd astrobee/src
git submodule add git@github.com:${ELISSA-ORGANIZATION}/${REPOSITORY}.git
```
2. Change back into astrobee and build:
```shell
cd ..
catkin build
```

## Setup the Simulation Environment

Using the Astrobee simulator for RAGGA/ELISSA related work requires some further setup.
This includes changing some default settings and replacing Astrobee files.

### Activate the NAV cam

1. Navigate to the simulation config directory:
```
astrobee/src/astrobee/simulation/config
```
2. Edit the **simulation.config** file, by changing the camera sampling rate to a value grater than 0.0, e.g. to:
```
nav_cam_rate = 5.0;
```
This will allow the simulator to generate images for the NAV cam, in this particular example the images will be generated at a rate of 5 Hz.
3. Change the NAV cam resolution. First navigate to the urdf directory:
```
astrobee/src/description/description/urdf
```
4. Edit the **sensor_nav_cam.urdf.xacro** file. Change the resolution values to:
```
`<width>1280</width>`
`<height>960</height>`
```
By default, the NAV cam resolution is reduced in the simulator for lower computational effort.

### Replace the Astrobee FF model

Replace default .urdf.xacro file for the Astrobee FF, this is done to include our Gecko-Docking mechanism in the 3D visualization model.

1. Navigate to:
```
astrobee/src/elissa3_astrobee/urdf
```
2. Copy the **model.urdf.xacro**
3. Navigate to:
```
astrobee/src/description/description/urdf
```
4. Paste and replace the existing **model.urdf.xacro**

### Replace the ISS RViz configuration file

Replace the default iss.rviz file to automatically have RViz configured for RAGGA research.

1. Navigate to:
```
astrobee/src/elissa3_astrobee/rviz
```
2. Copy the **iss.rviz** file
3. Navigate to:
```
astrobee/src/astrobee/resources/rviz
```
4. Paste and replace the existing **iss.rviz** file

### Replace the PMC mesh

By default the propulsion modules of the Astrobee will be colored gray.
In reality, they are black.
1. Navigate to:
```
astrobee/src/elissa3_astrobee/media/astrobee_freeflyer/meshes
```
2. Copy the **pmc.dae**
3. Navigate to 
```
astrobee/src/description/media/astrobee_freeflyer/meshes
```
4. Paste and replace the existing **pmc.dae** file

### Change the PMC skin of Bumble
Give Bumble another look, might be helpful later on.
1. Navigate to:
```
astrobee/src/elissa3_astrobee/media/astrobee_freeflyer/meshes
```
2. Copy the **pmc_skin_bumble.dae** 
3. Navigate to:
```
astrobee/src/description/media/astrobee_freeflyer/meshes
```
4. Paste and replace the existing **pmc_skin_bumble.dae** file
5. Navigate to:
```
astrobee/src/elissa3_astrobee/media/astrobee_freeflyer/media/materials/textures
```
6. Copy the **skin_bumble_high_vis.png**
7. Navigate to: 
```
astrobee/src/description/media/astrobee_freeflyer/media/materials/textures
```
8. Paste the **skin_bumble_high_vis.png** file