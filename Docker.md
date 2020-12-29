---
title: Docker instructions
description: 
published: 1
date: 2020-12-29T04:30:26.294Z
tags: 
editor: markdown
dateCreated: 2020-12-21T09:11:20.474Z
---

<img src="https://socialify.git.ci/ptTrR/arm-img-builder-docker/image?description=1&descriptionEditable=Build%20customized%20arm%20images%20with%20docker&font=Bitter&forks=1&issues=1&logo=https%3A%2F%2Fwww.docker.com%2Fsites%2Fdefault%2Ffiles%2Fd8%2F2019-07%2Fvertical-logo-monochromatic.png&owner=1&pattern=Charlie%20Brown&pulls=1&stargazers=1&theme=Dark" alt="arm-img-builder-docker" width="640" height="320" />

# Docker arm image builder

For easily build your image we have created a docker image. The only thing you need to install is docker and docker-compose.
You have the possibility to build the docker image yourself or download the image from docker hub.
The prebuilt docker images are available for the following architectures:

* amd64
* arm64

Here you find the image on the docker-hub:

[pttrr/arm-img-builder](https://hub.docker.com/r/pttrr/arm-img-builder)

We will provide two different tags: 

> latest --> for cross compiling on amd64 or arm64
> native --> for native compiling on arm64

## Installing docker and docker-compose

Docker and docker-compose are for following operating systems available:

* Linux (all distros)
* Mac
* Windows

You will find how to install docker and docker-compose for your operating system here:

https://docs.docker.com/get-docker/

## Install docker at raspberry or other arm devices

The official instruction for installing docker-compose on arm devices isnt working sometimes. 

You can follow this guide for the installation:
https://dev.to/rohansawant/installing-docker-and-docker-compose-on-the-raspberry-pi-in-5-simple-steps-3mgl

## Torubleshooting at docker
If you got some problems at using for compiling the image you should install the following on your host system:

```
apt install qemu-user-static #debian/ubuntu

yay -S qemu-user-static #arch and other distros
```
## Usage

### Clone my repo

```
git clone https://github.com/ptTrR/arm-img-builder-docker
```
or create the docker-compose.yml:

```
version: '3.6'
services:

  arm-img-builder:
  #  build: .  #uncomment for building 
    image: pttrr/arm-img-builder:latest 
  #  image: pttrr/arm-img-builder:native #uncomment for native compiling
    privileged: true
    container_name: arm-img-builder
    tty: true
    restart: always
    volumes:
      - /sys/fs/cgroup:/sys/fs/cgroup:ro
      - /dev:/dev
      - ./:/images
```
### Change the image tag to your needs. 

**:latest is for cross compiling on your amd64 and arm64
:native is for native compiling on arm64**

### Pulling and start the container

```
docker-compose pull && docker-compose up -d
```
If your container is successfully started you have to exec into it:
```
docker exec -it arm-img-builder bash
```
### Docker-Helper

We also created a "docker-helper" which is aimed for guys which not using docker that often or never used it. 
Just check this link:
https://wiki.arm-image-builder.xyz/en/docker-helper

### Supported Builder

* [rpi-img-builder](https://github.com/pyavitz/rpi-img-builder) is located at /build/rpi-img-builder
* [debian-image-builder](https://github.com/pyavitz/debian-image-builder) is located at /build/debian-img-builder

### Usage inside the container

Just run in the /build dir following commands:

```
make pull 	# Pulling latest updates from the builder
make update # Updating scripts and the makefile
make setup 	# The builder makefiles will be converted for docker-usage
```
Then enter in your wanted builder directory and follow the commands which you will find here:

[raspberry-image-builder](https://wiki.arm-image-builder.xyz/en/Raspberry)
[debian-image-builder](https://wiki.arm-image-builder.xyz/en/Debian)

## Moving image to the host system
When your image built, you just have to move your to the /image directory, for example:
```
mv *.img.xz /images
```

Then you will find the image where you started the docker-compose. 

## Maintenance and Troubleshooting

### Cleanup

For clearing up your directory and built cache in the container you can use the following commands:

```
make cleanup
make purge
make purge-all
```
### Clearing the complete docker system

1. Stop your running container with `docker stop arm-img-builder` 
2. Then run `docker system prune -a --volumes`

## Support

For more information watch at our [Wiki](https://wiki.arm-image-builder.xyz/) or [GitHub](https://github.com/pyavitz).

Should you come across any bugs, feel free to either open an issue on GitHub or talk with us directly by joining our channel on Freenode; [`#debianarm-port`](irc://irc.freenode.net/#debianarm-port)