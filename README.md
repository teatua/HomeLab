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




