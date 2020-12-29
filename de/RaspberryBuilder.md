---
title: Raspberry Image Builder 
description: 
published: 1
date: 2020-12-29T20:00:21.557Z
tags: 
editor: markdown
dateCreated: 2020-12-29T19:59:58.340Z
---

# Supported Boards and distributions

## Raspberry Image Builder

* **Raspberry Pi 4B (bcm2711)** | *Debian, Devuan and Ubuntu*
* **Raspberry Pi 3/A/B/+ (bcm2710)** | *Debian, Devuan and Ubuntu*
* **Raspberry Pi 0/W/B/+ (bcm2708)** | *Debian and Devuan*

## Debian Image Builder

* **Allwinner:** *NanoPi NEO Plus2, Orange Pi R1, Pine A64+ and Tritium*
* **Amlogic:** *Le Potato, Odroid C4 and Odroid N2/Plus*
* **Broadcom:**	*Raspberry Pi 4B (Using U-Boot)*
* **Rockchip:** *NanoPC-T4, Renegade and Rock64*

# Basics

- Most things are done automatically, you only have to provide your wanted settings
- Easy Cross-building on your powerful host system, so that the time is reduced much at building
- Many improvements are done automatically by the builder, just take a watch at our patches, which are included
- Upgrading Kernel, firmware, and some other scripts, which are included, are easily done with a few commands
- There also prebuilt images, which are completely tested.

# Using Docker

We have created a Docker image which already installed all dependencies for native and cross-compiling and also native compiling. So that only a few dependencies are needed, also it is isolated from your system.

## Using the docker-helper

The usage of the "docker-helper" will help you easily to exec into the container and the magic is mostly done within some commands.

