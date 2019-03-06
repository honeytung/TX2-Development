# TX2 Development
This repository contains some of my troubleshooting notes for Jetson TX2 Development Kit.

## Table of Contents
* [Install Jetpack on Linux VM](#install-jetpack-on-linux-vm)
* [Maximum Performance](#maximum-performance)

## Install Jetpack on Linux VM

Although unsupported, it is possible to install Jetpack on a Linux VM. I used Parallels Desktop running Linux 18.04 and Jetpack Ver. 3.3. The entire process can be followed in this [link](https://docs.nvidia.com/jetpack-l4t/2_1/index.html#developertools/mobile/jetpack/jetpack_l4t/2.0/jetpack_l4t_install.htm). Follow the entire process (full installation) until you reach the installer reports an error unable to obtain IP address of your TX2. Your TX2 in this stage should have the OS installed and can be booted without all the libraries. After that error, quit the installer and follow the following instructions:

1. Relauch the installer, this time do a custom install instead of full install.
2. In the list, go to "Flash OS Image to Target" and select the action to become "no action" (prevent from reinstalling the OS again)
3. Proceed on installing the files, the installer will need you to input the IP address of your TX2. You can check your IP address in Linux settings -> Network. Input your IP address and your username and password and the installer should proceed normally.

The process is confirmed working on host PC (MacBook Pro) running 18.04 using Parallels Desktop and Jetpack 3.3. (Note: error may show up during the installation process that is concern with missing dependencies, you can use `apt-get` to solve these problems)

## Maximum Performance

By default the high performance Denver2 cores are switched off for power saving. You can enable the cores using the following commands (need sudo privilige):

`echo 1 > /sys/devices/system/cpu/cpu1/online`

`echo 1 > /sys/devices/system/cpu/cpu2/online`

You can check core status using:

`~/tegrastats`

Finally, you can set maximum clock frequencies using the following command (need sudo privilige):

`sudo ./jetson_clocks.sh`
