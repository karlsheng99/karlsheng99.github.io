---
layout: post
title: "ROS Environment Configuration, Computation Graph, and Basic Commands"
description: "ROS Environment Configuration, Computation Graph, and Basic Commands"
date: 2023-07-21
feature_image: 
tags: [ROS, Raspberry Pi, Linux]
---

A study note for ROS environment configuration, computation graph and basic commands.

<!--more-->

# ROS Environment Configuration, Computation Graph, and Basic Commands

### Create Workspace

```bash
mkdir -p ~/catkin_ws/src
cd ~/catkin_ws
catkin_make
```

### Create a ROS package

```bash
cd ~/catkin_ws/src
catkin_create_pkg package_name std_msgs rospy roscpp # specify the dependencies
cd ..
catkin_make
```

### ROS Computation Graph

![section 6-1.jpg](/images/2023-07-21/section_6-1.jpg)

![section 6-2.jpg](/images/2023-07-21/section_6-2.jpg)

### Publish a message on a topic from a command line

![Untitled](/images/2023-07-21/Untitled.png)

### Visualize ROS computation graph using rqt_graph

```bash
rosrun rqt_graph rqt_graph
```

![Untitled](/images/2023-07-21/Untitled%201.png)