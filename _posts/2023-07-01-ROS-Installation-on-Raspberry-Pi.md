---
layout: post
title: "ROS Installation on Raspberry Pi"
description: "ROS on Raspberry Pi Installation Guide"
date: 2023-07-01
feature_image: images/2023-07-01/ROS-on-Raspberry-Pi.webp
tags: [ROS, Raspberry Pi, Linux]
---

An Installation Guide for Robot Operating System (ROS) Noetic on Raspberry Pi.

<!--more-->

# ROS Installation on Raspberry Pi

## Table of Contents
* [Install Ubuntu on Raspberry Pi](#install-ubuntu-on-raspberry-pi)
    * [Flash the SD Card](#1-flash-the-sd-card)
    * [Boot Ubuntu Server](#2-boot-ubuntu-server)
    * [Connect WiFi from command line](#3-connect-wifi-from-command-line)

* [ROS Noetic Installation on Ubuntu](#ros-noetic-installation-on-ubuntu)
    * [Setup sources.list](#1-setup-sourceslist)
    * [Setup Keys](#2-setup-keys)
    * [Installation](#3-installation)
    * [Setup Environment](#4-setup-environment)
    * [Dependencies for Building Packages](#5-dependencies-for-building-packages)

* [Verification](#verification)
    * [Start the ROS master in the first terminal](#1-start-the-ros-master-in-the-first-terminal)
    * [Start the turtlesim node in the second terminal](#2-start-the-turtlesim-node-in-the-second-terminal)
    * [Allow movement control by using arrow keys in the third terminal](#3-allow-movement-control-by-using-arrow-keys-in-the-third-terminal)

* [Access Raspberry Pi via SSH over the Internet (port forwarding)](#access-raspberry-pi-via-ssh-over-the-internet-port-forwarding)
    * [MobaXterm](#mobaxterm)

---

## Install Ubuntu on Raspberry Pi

### 1. Flash the SD Card

1. Insert the microSD card into a computer.
2. Install Raspberry Pi Imager.
    
    ![Untitled](/images/2023-07-01/1.png)
    
3. Choose OS: Select Other general-purpose OS → Ubuntu → Ubuntu Server 20.04.5 LTS (64-bit).
    
    ROS Noetic can only be installed on Ubuntu Focal (20.04).
    
    ![Untitled](/images/2023-07-01/2.png)
    
4. Choose Storage: Select the microSD card that has been inserted.
5. Click “Write” to flash the SD card

### 2. Boot Ubuntu Server

1. Insert the SD card into Raspberry Pi.
2. Plug in an HDMI screen and a USB keyboard, and power on Raspberry Pi.
3. Enter username and password.
    
    Default username: ubuntu
    
    Default password: ubuntu
    
4. Require to change the password after the first time login.

### 3. Connect WiFi from command line

1. Identify the name of your wireless network interface.
    
    ```bash
    ls /sys/class/net
    ```
    
    The wireless network interface name would be something like **`wlan0`** or **`wlp3s0`**.
    
2. Navigate to the `**/etc/netplan**` directory and locate the appropriate Netplan configuration files. The configuration file might have a name such as **`01-network-manager-all.yaml`** or **`50-cloud-init.yaml`**.
    
    ```bash
    ls /etc/netplan/
    ```
    
3. Edit the Netplan configuration file.
    
    ```bash
    sudoedit /etc/netplan/50-cloud-init.yaml
    ```
    
    Insert the **`wifis`** block with your SSID name and password into the configuration file.
    
    ```bash
    # This file is generated from information provided by the datasource.  Changes
    # to it will not persist across an instance reboot.  To disable cloud-init's
    # network configuration capabilities, write a file
    # /etc/cloud/cloud.cfg.d/99-disable-network-config.cfg with the following:
    # network: {config: disabled}
    network:
        ethernets:
            eth0:
                dhcp4: true
                optional: true
        version: 2
        wifis:
            wlan0:
                optional: true
                access-points:
                    "SSID-NAME-HERE":
                        password: "PASSWORD-HERE"
                dhcp4: true
    ```
    
    Make sure that the **`wifis`** block is aligned with the above **`ethernets`** or **`version`** block. Insert spaces instead of using Tab key.
    
4. Apply the changes and connect to your wireless interface.
    
    ```bash
    sudo netplan apply
    ```
    
5. If WiFi is connected successfully, you would be able to see your wireless adapter connected to the wireless network.
    
    ```bash
    ip a
    ```
    

## ROS Noetic Installation on Ubuntu

You can also follow the installation guide available on the [ROS official website](http://wiki.ros.org/noetic/Installation/Ubuntu).

### 1. Setup sources.list

Setup your computer to accept software from packages.ros.org.

```bash
sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
```

### 2. Setup Keys

```bash
sudo apt install curl # if you haven't already installed curl
curl -s https://raw.githubusercontent.com/ros/rosdistro/master/ros.asc | sudo apt-key add -
```

### 3. Installation

1. Make sure the package index is up-to-date
    
    ```bash
    sudo apt update
    ```
    
2. Pick ROS packages to be installed
    - **Desktop-Full Install:** Everything in **Desktop** plus 2D/3D simulators and 2D/3D perception packages
        
        ```bash
        sudo apt install ros-noetic-desktop-full
        ```
        
    - **Desktop Install:** Everything in **ROS-Base** plus tools like [rqt](http://wiki.ros.org/rqt) and [rviz](http://wiki.ros.org/rviz)
        
        ```bash
        sudo apt install ros-noetic-desktop
        ```
        
    - **ROS-Base:** ROS packaging, build, and communication libraries. No GUI tools.
        
        ```bash
        sudo apt install ros-noetic-ros-base
        ```
        

### 4. Setup Environment

You must source this script in every **bash** terminal you use ROS in.

```bash
source /opt/ros/noetic/setup.bash
```

It can be convenient to automatically source this script every time a new shell is launched. These commands will do that for you.

```bash
echo "source /opt/ros/noetic/setup.bash" >> ~/.bashrc
source ~/.bashrc
```

### 5. Dependencies for Building Packages

To create and manage your own ROS workspaces, there are various tools and requirements that are distributed separately.

To install this tool and other dependencies for building ROS packages, run:

```bash
sudo apt install python3-rosdep python3-rosinstall python3-rosinstall-generator python3-wstool build-essential
```

1. Initialize rosdep
    
    Before you can use many ROS tools, you will need to initialize rosdep. rosdep enables you to easily install system dependencies for source you want to compile and is required to run some core components in ROS.
    
    ```bash
    sudo rosdep init
    rosdep update
    ```
    

## Verification

Verify that ROS is installed successfully by running Turtlesim.

### 1. Start the ROS master in the first terminal

```bash
roscore
```

![Untitled](/images/2023-07-01/3.png)

### 2. Start the turtlesim node in the second terminal

```bash
rosrun turtlesim turtlesim_node
```

![Untitled](/images/2023-07-01/4.png)

### 3. Allow movement control by using arrow keys in the third terminal

```bash
rosrun turtlesim turtle_teleop_key
```

![Untitled](/images/2023-07-01/5.png)

## Access Raspberry Pi via SSH over the Internet (port forwarding)

This step will allow you to access your remote device via SSH, even if your local and remote devices are not connected to the same network. By forwarding your device to the internet, you can remotely control your Raspberry Pi from anywhere, whether you're at school or in the office while it stays at home.

1. Login to your router via the default gateway address.
2. Enter the credentials for your router on its login page.
3. Locate the port forwarding settings. Advanced → Port Forwarding
4. Add Port Forward.
    1. Select Raspberry Pi for the port forward.
    2. Pick port number 22 for SSH.
    3. Select TCP protocol.
5. Check to see if the port is open by going to [www.portchecktool.com](http://www.portchecktool.com/). 
    
    Enter the port number 22 and click *Check Your Port*.
    

Any incoming request to the router which has the external IP address over port 22 will be routed to the Raspberry Pi on the network.

### MobaXterm

Since ROS has visualization tools such as Rviz which has a graphic user interface, MobaXterm would be a good tool to control your remote device via SSH and display graphical applications using the embedded X server.

![Untitled](/images/2023-07-01/6.png)