# Install the On-Board Software on the Hamilcar Freeflyers

A guide to the installation of the OBS for the Hamilcar freeflyers (and the force measurement on-board Hannibal) is presented here. 

---
Table of Content:
- [Install the On-Board Software on the Hamilcar Freeflyers](#install-the-on-board-software-on-the-hamilcar-freeflyers)
  - [Creating the SD Card](#creating-the-sd-card)
  - [Updating the On-Board Software](#updating-the-on-board-software)
    - [SSHuttle Installation](#sshuttle-installation)
    - [Change the MAC Adress](#change-the-mac-adress)
    - [Update the ROS Files](#update-the-ros-files)
    - [Enable GPIO Access](#enable-gpio-access)

---
Other usefull pages: [Hamilcar Freeflyers](hamilcar), [SSHuttle](sshuttle)

--- 

## Creating the SD Card

As the Freeflyers are utilizing Raspberry Pis as on-board computers, the [OS](https://linuxmint.com/edition.php?id=293) must be loaded to a SD card. To decrease the effort with the installation of the [ROS](https://www.ros.org/) environment, an already existing iso image can be used. The image of the Red Five OBS can be found on the Sansa Computer Desktop.

The image can be loaded on the SD card using the [WindDiskImager](https://www.heise.de/download/product/win32-disk-imager-92033) running on Windows. The same should be possible using the [Raspberry Pi Imager](https://www.raspberrypi.com/software/) on Linux, but was not successfull on the last attempts.

## Updating the On-Board Software

### SSHuttle Installation

To simplify the next steps, [SSHuttle](sshuttle) should be installed first. If not internet is available on the Raspberry Pi, the follow the detailed description provided on the sshutle page.

### Change the MAC Adress

Next, the MAC adress must be changed. As the ip adress is updated automatically, the MAC adress is bound to the image file of Red Five. To avoid issues if both systems are online at the same time, the adress must be replaced by a random adress. The next steps follow [this guide](https://www.elektronik-kompendium.de/sites/raspberry-pi/2102231.htm). First, connect to the internet (via sshuttle if necessary) to install the following package:

```bash
sudo apt-get install macchanger
```

Disable the network (maybe disconnect from sshuttle), set a random MAC adress and enable the network again.

```bash
sudo ip link set eth0 down
sudo macchanger -r eth0
sudo ip link set eth0 up
```

### Update the ROS Files

To ensure a clean integration in the existing ROS network, the follwoing files must be updated to the new ip adress of the OBC:

| File | Change |
| - | - |
| .bashrc | ROS_IP |
| | ROS_HOSTNAME |
 env.sh | ROS_HOSTNAME |

 ### Enable GPIO Access

 For the force measuremenet and other features, an access to the GPIO pins is necessary. Be sure, that the current user is part of the *gpio* group (or [create the group](https://superuser.com/questions/624745/ubuntu-server-create-group-create-user-user-specific-access)):

 ```bash
sudo adduser ubuntu gpio
 ```

Check the current permissions of the */dev/gpiomem* file:

```bash
ls -l /dev/gpiomem
```

If the *gpio* group has no access, you must allow the group to access the mem and give read and write control:

```bash
sudo chown root.gpio /dev/gpiomem
sudo chmod g+rw /dev/gpiomem
```

As the */dev* folder is created with the boot process, you must give these permissions after every launch. To provide these permissions permanantly, you must create a *udev* rule:

```bash
nano /etc/udev/rules.d/gpio.rules
```

Add the follwoing rule:

```
KERNEL=="gpiomem", GROUP="gpio", MODE="0660"
```

If any problems occur, follow [one](https://raspberrypi.stackexchange.com/questions/40105/access-gpio-pins-without-root-no-access-to-dev-mem-try-running-as-root9) [of](https://raspberrypi.stackexchange.com/questions/59371/set-permissions-and-group-for-dev-gpiomem-permanently?noredirect=1&lq=1) [these](https://raspberrypi.stackexchange.com/questions/40105/access-gpio-pins-without-root-no-access-to-dev-mem-try-running-as-root) [guides](https://raspberrypi.stackexchange.com/questions/5289/permissions-on-dev-entries). 
