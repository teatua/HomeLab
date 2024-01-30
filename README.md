# HomeLab build on a small factor server running Debian 12 (Bookworm)

## Description 

In this project, we will explore the ways of building a HomeLab with minimal hardware requirements. In this case, I am using an intel NUC i3 with 4 core, 8 threds running at 2.1GHz, with 8GB Ram and only 120 GB storage ! Small factor PC's of this kind can be cheap yet powerful enough to gain full sovereignty over your LAB ;)

**System minimal requirements:**

* 4 core CPU
* 8GB RAM
* 120GB storage
* Ethernet Port 
* Wake on Lan (WOL) compatibility

**Accessory requirements:**

* Your personal computer / laptop
* Monitor
* Mouse
* Keyboard
* Bootable USB drive
* 1 free LAN Ethernet port on your router, with an ethernet cable


## Table of Content

1. [Installing the Operating System (OS)](##Installing-the-Operating-System-(OS))

## Installing the Operating System (OS)

You will require:

* Debian 12 (bookworm) Optical Disc Image [(ISO)](https://www.debian.org/download)
* Bootable USB (8GB minimum)
* [Balena Etcher](https://etcher.balena.io/)

Loading your Image to the bootable USB: 

1. Open BalenaEtcher and select "Flash from file" -> Locate and select your Debian12.iso download 
2. Select target and locate your bootable USB drive
3. Hit Flash ! Once completed, you can safely remove the USB drive.

Booting the Server from a USB Key

Make sure to have your server connected to a monitor with keyboard and mouse.

1. Insert the USB drive
2. Check your server's motherboard manual on how to boot in BIOS, something alike pressing Delete on system wake.
3. Once in the BIOS, find and set the USB drive to be first in boot priority. Enable Wake on Lan and save and exit.

Your server should now launch the Debian 12 installation menu, you can choose a non graphical interface. For security purposes, it would be recommended to use a strong and unique password for both your root user, and session user. 

## Configuring remote access via Secure Shell (SSH)

From the terminal, login as root with your set credential:
```
sudo su
```
Install Open SSH Server
```
apt install openssh-server
```
Verify the service is active and enabled
```
systemctl status ssh
```
To activate the service 
```
systemctl start ssh
```
To enable the service at system start
```
systemctl enable ssh
```

You will need to find the IP address of your server to be able to remotely access it, for this simply type ```ip a``` in the terminal and locate your 192.168.0.* address.

Your router might be Dynamically assigning an IP address to your device through a DHCP server. For ease of use, you will need to set a static IP.

On your personal device, login to your router via 192.168.0.1 / 192.168.0.10 or following your router's manual -> Locate DHCP Server and address reservation, you will there be able to assign a static IP to your Server.







