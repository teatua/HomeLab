# HomeLab built on a small factor server running Debian 12 (Bookworm) and containerized applications

## Description 

In this project, we will explore the ways of building a HomeLab with minimal hardware requirements. In this case, I am using an intel NUC i3 with 4 core, 8 threds running at 2.1GHz, with 8GB Ram and only 120 GB storage ! Small factor PC's of this kind can be found for cheap, avoiding ongoing and unexpected bills from cloud providers. Whilst being powerful enough to run several containerized applications, and gain full sovereignty over your LAB environment.

**System minimal requirements:**

* 4 core CPU
* 8GB RAM
* 120GB storage
* Ethernet Port 
* Wake on Lan (WOL) compatibility

**Accessory requirements:**

* Your personal computer / laptop
* Your personal Smart Phone
* Monitor
* Mouse
* Keyboard
* Bootable USB drive
* 1 free LAN Ethernet port on your router, with an ethernet cable


## Table of Content

1. Installing the Operating System (OS)
2. Configuring Wake on Lan (WOL) using your personal Smart Phone
3. Configuring remote access via Secure Shell (SSH)]

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
3. Once in the BIOS, find and set the USB drive to be first in boot priority. Enable Wake on Lan and save / exit.

Your server should now launch the Debian 12 installation menu, you can choose a non graphical interface. For security purposes, it would be recommended to use a strong and unique password for both your root user, and session user. 

## Configuring remote access via Secure Shell (SSH)

From your server's terminal, login as root with your set credential:
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

__Let's SSH__

* For Windows Users, you may need to enable ssh following the [Microsoft Guidelines](https://learn.microsoft.com/en-us/windows-server/administration/openssh/openssh_install_firstuse?tabs=gui)
* For Mac users, it should already be up and ready to go
* For Linux users, you may need to repeat the openssh server install following your package manager guidelines.

(replace user and ip address)
```
ssh user@ip address
```
Now that you have successfuly SSH'd into your server, type in ```exit``` to come back to your personal computer terminal.

To secure the SSH connection, we will create an SSH key with the following command
```
ssh-keygen -t ed25519
```
_-t stands for type. This allows you to choose between different key algorithms supported by SSH. the ed25519 algorithm is one of the most secure up to date, as of 2023_

We will now transfer this key onto our server
```
ssh-copy-id user@ip address
```
Log back in, notice you will not be asked for a user password.
```
ssh user@ip address
```
We will now disable root and password login, for this we will change the configuration file of sshd.config, located at /etc/ssh/sshd.config
```
sudo nano /etc/ssh/sshd.config
```
* Locate "PermitRootLogin" with ```Ctrl + w``` and set to "no". For this to apply, makes sure to remove any comment sign __#__ at the begining of the line.
* Locate "PasswordAuthentication" and set to "no"
* As we will not be using this feature, it will be safer to also locate "UsePAM" and set to "no"

Exit and save ```Ctrl + x``` -> yes

## Disabling sleep

You may want to stop your machine from going to sleep and becoming unaccessible, use the following command:
'''
sudo systemctl mask sleep.target suspend.target hibernate.target hybrid-sleep.target
'''
To re-enable sleep (optional):
'''
sudo systemctl unmask sleep.target suspend.target hibernate.target hybrid-sleep.target
'''











