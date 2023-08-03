---
layout: post
title: "ROS Network Configuration and Utilities"
description: "ROS Network Configuration and Utilities"
date: 2023-08-01
feature_image: 
tags: [ROS, Raspberry Pi, Linux]
---

A study note for ROS Network Configuration and Utilities.

<!--more-->

# Network Configuration and Utilities

### User Workstation

edit .bashrc file

```bash
# Workstation Configuration
# The ip address for the local workstation
export ROS_IP=workstation_ip_address
export ROS_HOSTNAME=workstation_ip_address
export ROS_MASTER_URI=http://master_node_ip_address:11311

echo "ROS_HOSTNAME: "$ROS_HOSTNAME
echo "ROS_IP: "$ROS_IP
echo "ROS_MASTER_URI: "$ROS_MASTER_URI
```

### Robot Machine

edit .bashrc file

```bash
# Robot Machine Configuration
# The localhost ip address = ip address for the master node
export ROS_MASTER_URI=http://localhost:11311
# The ip address for the master node
export ROS_HOSTNAME=robot_machine_ip_address
export ROS_IP=robot_machine_ip_address

echo "ROS_HOSTNAME: "$ROS_HOSTNAME
echo "ROS_IP: "$ROS_IP
echo "ROS_MASTER_URI: "$ROS_MASTER_URI
```

### Launch File

- XML document which specifies
    - which nodes to execute
    - their parameters
    - what other launch files to include
- `roslaunch` launches multiple ROS nodes at the same time
- has a .launch extension

Launch file: file_name.launch

```bash
<launch>
    <node name="node_name" pkg="package_name" type="executable_file" />
    <node name="node_name" pkg="package_name" type="executable_file" output="screen"/>
</launch>
```

```bash
<launch>
		<include file="$(find package_name)/src/launch_file" />

		<param name="param_name" value="val" />
		# rospy.get_param("param_name")

    <node name="node_name" pkg="package_name" type="executable_file" />
</launch>
```

```bash
roslaunch package_name launch_file
```