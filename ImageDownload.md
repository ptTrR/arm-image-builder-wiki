---
title: prebuilt Images
description: 
published: 1
date: 2021-01-06T05:02:46.945Z
tags: 
editor: undefined
dateCreated: 2020-12-29T20:13:34.502Z
---

# Downloading prebuilt Images

**Official and verified images can be downloaded from the Releases section of the github.**
https://github.com/pyavitz/rpi-img-builder/releases

**Other images may also be found at the following location.**
https://files.arm-image-builder.xyz
**Important: Not every image is verified and nor may work**

# Usage after flashing

## Debian / Devuan

### /boot/rename_to_credentials.txt

```sh
Rename file to credentials.txt and input your wifi information.

SSID=" "			# Service set identifier
PASSKEY=" "			# Wifi password
COUNTRYCODE=" "			# Your country code

# set static ip
MANUAL=n			# Set to y to enable a static ip
IPADDR=" "			# Static ip address
NETMASK=" "			# Your Netmask
GATEWAY=" "			# Your Gateway
NAMESERVERS=" "			# Your preferred dns

For headless use: ssh user@ipaddress

Note:
You can also mount the ROOTFS partition and edit the following
files, whilst leaving rename_to_credentials.txt untouched.

/etc/opt/interfaces.manual
/etc/opt/wpa_supplicant.manual
```

## Ubuntu

### /boot/rename_to_credentials.txt

```sh
Rename file to credentials.txt and input your wifi information.

NAME=" "			# Name of the connection
SSID=" "			# Service set identifier
PASSKEY=" "			# Wifi password
COUNTRYCODE=" "			# Your country code

MANUAL=n			# Set to y to enable a static ip
IPADDR=" "			# Static ip address
GATEWAY=" "			# Your Gateway
DNS=""				# Your preferred dns

For headless use: ssh user@ipaddress
```
# Usage on the device

## Using deb-eeprom

```sh
Raspberry Pi 4B EEPROM Helper Script
Usage: deb-eeprom -opt

   -v       Edit version variable
   -U       Upgrade eeprom package
   -w       Setup and install usb boot
   -u       Update script

Note:
Upon install please run 'deb-eeprom -u' before using this script.
```

## Using fetch
```sh
Fetch, Linux kernel installer for the Raspberry Pi Image Builder
Usage: fetch -opt

   -1       Linux 5.4.y LTS
   -2       Linux Stable Branch
   -3       Linux Mainline Branch
   -u       Update Fetch
   -s       Not working? Setup Fetch

fetch -h will list available options and kernel revisions
```
## Simple wifi helper (Debian / Devuan)
```sh
swh -h

   -s       Scan for SSID's
   -u       Bring up interface
   -d       Bring down interface
   -r       Restart interface
   -W       Edit wpa supplicant
   -I       Edit interfaces
```
## CPU frequency scaling
```sh
Usage: governor -opt

   -c       Conservative
   -o       Ondemand
   -p       Performance

   -r       Run
   -u       Update

A service runs 'governor -r' during boot.
```

---