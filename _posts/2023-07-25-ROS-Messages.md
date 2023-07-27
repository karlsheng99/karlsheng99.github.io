---
layout: post
title: "ROS Messages"
description: "ROS Messages"
date: 2023-07-25
feature_image: 
tags: [ROS, Raspberry Pi, Linux]
---

A study note for ROS Messages.

<!--more-->

# ROS Messages

### Create customized messages

1. Create a msg folder in the package
2. Create the message file with file extension “.msg”
3. Edit the message file by adding the elements
    
    e.g.
    
    ```bash
    int32 id
    string name
    float32 temperature
    float32 humidity
    ```
    
4. Update dependencies in CMakeLists.txt
    
    ```diff
    find_package(catkin REQUIRED COMPONENTS
        roscpp
        rospy
        std_msgs
    +	message_generation
    )
    ```
    
    ```diff
    add_message_files(
        FILES
    +	message_name.msg
    )
    ```
    
    ```bash
    generate_messages(
    	DEPENDENCIES
    	std_msgs
    )
    ```
    
    ```diff
    catkin_package(
    	INCLUDE_DIRS include
    	LIBRARIES ros_basics_tutorials
    +	CATKIN_DEPENDS roscpp rospy std_msgs message_runtime
    	DEPENDS system_lib
    )
    ```
    
5. Update Dependencies in package.xml
    
    ```xml
    <buildtool_depend>catkin</buildtool_depend>
    
    <build_depend>roscpp</build_depend>
    <build_depend>rospy</build_depend>
    <build_depend>std_msgs</build_depend>
    <build_depend>message_generation</build_depend>
    
    <build_export_depend>roscpp</build_export_depend>
    <build_export_depend>rospy</build_export_depend>
    <build_export_depend>std_msgs</build_export_depend>
    
    <exec_depend>roscpp</exec_depend>
    <exec_depend>rospy</exec_depend>
    <exec_depend>std_msgs</exec_depend>
    <exec_depend>message_runtime</exec_depend>
    ```
    
6. Compile programs and build executables
    
    ```bash
    catkin_make
    ```
    
7. Show the message
    
    ```bash
    rosmsg show package_name/message_name
    ```