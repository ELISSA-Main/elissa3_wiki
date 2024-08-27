# Free-Flyer on-board network setup

This page walks you through the networking setup. 

---

## Table of Contents
- [Preparation](#preparation)
- [Setup Wi-Fi Hotspot](#setup-wi-fi-hotspot)
- [Prepare Portable Router](#prepare-portable-router)
- [Setup of Network Extension](#setup-of-network-extension)
- [Connecting to Inner Network Devices](#connecting-to-inner-network-devices)
  
---

## Preparation

We are currently using the following networking equipment:
- TP Link 5 Port LAN switch
- TP Link Portable AC750-WLAN-Router
- One PC with an Ethernet connection and a Wi-Fi module (Referred to as the HOST)
- Multiple LAN cables 

### Setup Wi-Fi Hotspot 

It sometimes may be necessary for you to create your own hotspot, which you will connect the portable router to. This may be the case if your network is strictly guarded via MAC-Address filtering. For this to work, you will need a computer (the HOST) already connected to a present ethernet network with a Wi-Fi antenna. 
We are currently using a Debian based OS but creating a hotspot should be possible on other operating systems.

Here's the guide for Debian/Ubuntu operating systems:
1. Open the app settings
2. Locate the section Wi-Fi
3. Locate the 3 vertical dots on the top of the setting bar.
4. Select "Turn on Wi-Fi Hotspot"
5. Choose a Password and SSID (Make sure to note this down for later). For Security Type, choose "WPA"
6. You should now be able to see your HOTSPOT on another device
7. Head to "/etc/NetworkManager/system-connections"
8. Locate the file "Hotspot.nmconnection"
9. Proceed to edit the file using "sudo nano Hotspot.nmconnection" or vim that's up to you
10. Edit the Ipv4 section to match below
11. Restart the Network Daemon using "sudo service network-manager restart"
```shell
[ipv4]
address1=192.168.0.1/24,192.168.0.1
dns-search=
method=shared
```

## Prepare Portable Router

This section will require another Wi-Fi capable device. 

1. Locate the "Mode Switch" on the side of the device and select the lowest option.
2. Locate the back of your router and if you can, note down or take a photo of the Information on the back.
3. Plug the router into an appropriate PSU 
4. There will be one or multiple SSID(s) as well as a password and a "default access"
5. Use your phone or other to connect to that Wi-Fi Network the password should work for both if multiple SSIDs are listed.
6. Open up a browser on your device and type in the "default access" as found on the back of your router. It should be "http://tplinkwifi.net"
7. If this is the initial installation, you should be met by a password setting prompt. Enter a password of your choosing.
8. You are now inside the control center. Locate the option "Quick Setup" default settings should be working well for you.
9. You will be prompted to connect to a network: Choose your HOTSPOT and enter the corresponding password 
10. Ensure that the operating mode is set to "client" (This may be done in quick setup or later via the option "operating mode" in the control panel)
11. In the "Network->Lan" section set the IP Address to static and the routers IP to "192.168.0.2"

## Setup of network extension

1. Use an appropriate PSU to connect to the network-switch
2. Connect your router to the Network-Switch via a LAN cable. Each ethernet port on the switch is numbered, choose the highest number and connect it.
3. Now you may connect your Raspberry Pi's or other on-board computers to the network-switch

All devices connected to the router will now be referred to as being in the "inner" Network.

## Connecting to inner network devices

Now that your inner Network is set up, it's time to find and connect to the devices inside of it. 
Assuming you're still using Ubuntu, this should be easy enough! 
You may do this on either the HOST or another device connected to the HOSTS Hotspot.

Run the command:
```shell
ifconfig
```
This should list all network interfaces. One of them being your Wi-Fi antenna you either used to create the Hotspot or used to connect to it. 

Now type in the command: 
```shell
sudo arp-scan -l --interface=(Add Interface here and remove brackets)
```

After a second, this should list all devices on the network connected to that interface. 

You can now connect to them via SSH or other protocols as normal! 
