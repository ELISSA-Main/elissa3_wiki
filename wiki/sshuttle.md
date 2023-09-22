# Remote work on the Hamilcar On-Board Computer

To update the software, configure parameters or fix bugs it is essential to work on the on-board computer of the Hamilcar freeflyers. Some tricks to make this easier are shown on this page.

---
Table of Content:
- [Remote work on the Hamilcar On-Board Computer](#remote-work-on-the-hamilcar-on-board-computer)
  - [Enable an Internet Connection](#enable-an-internet-connection)
    - [Installation of sshuttle](#installation-of-sshuttle)
    - [Installation without Internet on the Remote](#installation-without-internet-on-the-remote)
    - [Execute sshuttle](#execute-sshuttle)
    - [Usage](#usage)

---
Other usefull pages: [Hamilcar Freeflyers](hamilcar), [Hamilcar OBS](install_hamilcar_obs), [Network IDs](https://github.com/ELISSA-IRAS/elissa_wiki/blob/master/testbed/network.md)

---

## Enable an Internet Connection

One way to use the Hamilcar freeflyers with the internet is the connection of a screen and working in the desktop environment with a wifi connection. A simpler solution is possible with the use of [sshuttle](https://github.com/sshuttle/sshuttle). It is already installed on the following systems:

- [x] Red Five
- [ ] Hamilcar
- [ ] Hannibal
- [x] Pegasus

### Installation of sshuttle

The experience showed that the best way to install _sshuttle_ is the usage of pip. Use the following command:

```bash
pip3 install sshuttle
```

The other [available options](https://sshuttle.readthedocs.io/en/stable/installation.html) did not run on the Raspberry Pi of Red Five. 

### Installation without Internet on the Remote

If no internet connection is available on the remote machine, the follwing steps must be done for an installation:

1. Download the [sshuttle repository](https://github.com/sshuttle/sshuttle) as a zip file
2. Copy this zip file to the remote via ssh:

```bash
scp /home/<sansa-username>/Downloads <remote-username>@<remote-ip>:/path/to/remote/file
```
3. [Install](https://stackoverflow.com/questions/15031694/installing-python-packages-from-local-file-system-folder-to-virtualenv-with-pip) the pip-package using the file:

```bash
pip install sshuttle --no-index --find-links file:///path/to/remote/file
```
4. Restart the system.

### Execute sshuttle

To use _sshuttle_ to connect the freeflyer to the internet, a command must be executed from the freeflyer. This can happen via an ssh-connection from the _Sansa_ computer (or any other computer in the _elissa_ network). Connect to the freeflyer via:

```bash
ssh <ff-username>@<ff-ip-adress>
```
The following command must be executed to foreward the internet traffic via the _Sansa_ computer:

```bash
sshuttle --dns --verbose --remote <sansa-username>@<sansa-ip-adress> --exclude <sansa-ip-adress> 0/0
```
If the command is not found after installation, it may be necessary to provide the path to the installation when executing with python. The given command differs from the default one provided in the [documentation](https://sshuttle.readthedocs.io/en/stable/usage.html), as this did not work on Red Five. The solution was found following [this thread](https://github.com/sshuttle/sshuttle/issues/150). 

### Usage

Another terminal must be opend to use the enabled internet connection. Now commands like `git pull` can be executed while still being connected to the _elissa_ network and without the need to connect a screen.

