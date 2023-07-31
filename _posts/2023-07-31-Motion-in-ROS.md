---
layout: post
title: "Motion in ROS"
description: "Motion in ROS"
date: 2023-07-31
feature_image: 
tags: [ROS, Raspberry Pi, Linux]
---

A study note for Motion in ROS.

<!--more-->

# Motion in ROS

### Basic Motion Types:

- Move in a straight line
    - Linear: x: speed
- Rotate in place
    - Angular: z: speed
- Go to goal (PID control)
    - Linear: x: func(distance)
    - Angular: z: func(angle)
- Spiral
    - Linear: x: func(time)
    - Angular: z: constant
    

![Untitled](/images/2023-07-31/Untitled.png)

![Untitled](/images/2023-07-31/Untitled%201.png)

### Launch File

Allows to start multiple nodes at the same time

Launch file: file_name.launch

```bash
<launch>
    <node name="node_name" pkg="package_name" type="executable_file" />
    <node name="node_name" pkg="package_name" type="executable_file" output="screen"/>
</launch>
```

```bash
roslaunch package_name launch_file
```