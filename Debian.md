---
title: Debian Image Builder
description: 
published: 1
date: 2021-01-03T03:52:38.533Z
tags: 
editor: undefined
dateCreated: 2020-12-21T09:11:13.668Z
---

<img src="https://socialify.git.ci/pyavitz/debian-image-builder/image?description=1&font=Rokkitt&forks=1&issues=1&logo=https%3A%2F%2Fwww.debian.org%2Flogos%2Fopenlogo-nd.svg&owner=1&pattern=Charlie%20Brown&pulls=1&stargazers=1&theme=Dark" alt="debian-image-builder" width="640" height="320" />

# Supported boards


- Allwinner:      # NanoPi NEO Plus2, Orange Pi R1, Pine A64+ and Tritium
- Amlogic:        # Le Potato, Odroid C4 and Odroid N2/Plus
- Broadcom:       # Raspberry Pi 4B
- Rockchip:       # NanoPC-T4, Renegade and Rock64

# Dependencies for Debian Buster AMD64/x86_64 cross compile

```sh
sudo apt install build-essential bison bc git dialog patch dosfstools zip unzip qemu parted \ 
                 debootstrap qemu-user-static rsync kmod cpio flex libssl-dev libncurses5-dev \
                 device-tree-compiler libfdt-dev python3-distutils python3-dev swig fakeroot \
                 lzop lz4 aria2 pv toilet figlet crossbuild-essential-arm64 gcc-arm-none-eabi \
                 distro-info-data lsb-release python python-dev
                 
Orange Pi R1 - sudo apt install -y crossbuild-essential-armhf
```

# Instructions

## Install dependencies

```sh
make ccompile   # Cross compile
make ncompile   # Native compile
```

## Menu interface

```sh
make config     # Create user data file
make menu       # Open menu interface
make dialogrc   # Set builder theme (optional)
```
## Config Menu

```sh
Name:					 # Whats your name?
Username:       # Your username
Password:       # Your password
Branding:       # Set ASCII text banner
Hostname:       # Set the system's host name
Debian:         # Supported: buster, bullseye, unstable and sid
U-Boot:         # Supported: v2020.10
Branch:         # Supported: 5.10.y (if patches fail let me know)
Mainline:       # 1 for any x.y-rc
Menuconfig:     # 1 to run uboot and kernel menuconfig
Crosscompile:   # 1 to cross compile | 0 to native compile
rtl88XXau:      # 1 to add Realtek 8812AU/14AU/21AU wireless support
rtl88XXbu:      # 1 to add Realtek 88X2BU wireless support
rtl88XXcu:      # 1 to add Realtek 8811CU/21CU wireless support
```
## User defconfig
```sh
nano userdata.txt
# place config in defconfig directory
custom_defconfig=1
MYCONFIG="nameofyour_defconfig"
```
## Compression
```sh
nano userdata.txt
# change from 0 to 1
auto=1        # compresses to img.xz
```
## Odroid N2/Plus eMMC
```sh
nano userdata.txt
# change from 0 to 1
emmc=1
```
## Miscellaneous

```sh
make cleanup    # Clean up image errors
make purge      # Remove sources directory
make purge-all  # Remove sources and output directory
```

# Usage

## Write to eMMC

```sh
Supported: Le Potato, Odroid C4, Odroid N2/Plus and NanoPi NEO Plus2
1. Attach eMMC module       # In some cases the module may need to be attached after boot
2. Boot from sdcard
3. Execute: sudo write2mmc
```

## Deb EEPROM ([usb_storage.quirks](https://github.com/pyavitz/rpi-img-builder/issues/17))

```
Raspberry Pi 4B EEPROM Helper Script
Usage: deb-eeprom -opt

   -v       Edit version variable
   -U       Upgrade eeprom package
   -w       Setup and install usb boot
   -u       Update script

Note:
Upon install please run 'deb-eeprom -u' before using this script.
```
## Simple wifi helper
```
swh -h

   -s       Scan for SSID's
   -u       Bring up interface
   -d       Bring down interface
   -r       Restart interface
   -W       Edit wpa supplicant
   -I       Edit interfaces
```
## CPU frequency scaling
```
governor -h

   -c       Conservative
   -o       Ondemand
   -p       Performance

   -r       Run
   -u       Update
   
A systemd service runs 'governor -r' during boot.
```