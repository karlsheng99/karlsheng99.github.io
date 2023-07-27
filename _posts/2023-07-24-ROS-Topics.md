---
layout: post
title: "ROS Topics"
description: "ROS Topics"
date: 2023-07-24
feature_image: 
tags: [ROS, Raspberry Pi, Linux]
---

A study note for ROS Topics.

<!--more-->

# ROS Topics

### Write Publisher ROS Topics

1. Name for the topic to publish
2. Type of the messages that the topic will publish
3. Frequency of topic publication
4. Create a publisher object with parameters chosen
5. Keep publishing the topic message at the selected frequency

### Write Subscriber ROS Topics

1. Name for the topic to listen to
2. Type of the messages to be received
3. Define a callback function that will be automatically executed when a new message is received on the topic
4. Start listening for the topic messages
5. Spin to listen forever

### Make python file executable

Ensure using the correct interpreter (first line in the python file)

```python
#!/usr/bin/env python
```

Give the file execute permission

```bash
chmod +x file_name.py
```

## Assignment 2

1. Find the topic name of the pose (position and orientation) of turtlesim and its message type. Display the content of message of the pose.
    
    ```bash
    rostopic list
    ```
    
    /turtle1/pose
    
    ```bash
    rostopic info /turtle1/pose
    ```
    
    Type: turtlesim/Pose
    
    Publishers:
    
    - /turtlesim ([http://ubuntu:34483/](http://ubuntu:34483/))
    
    ```bash
    rosmsg show turtlesim/Pose
    ```
    
    float32 x
    float32 y
    float32 theta
    float32 linear_velocity
    float32 angular_velocity
    
2. Find the topic name of the velocity command of turtlesim and its message type. Display the content of message of the velocity command.
    
    ```bash
    rostopic list
    ```
    
    /turtle1/cmd_vel
    
    ```bash
    rostopic info /turtle1/cmd_vel
    ```
    
    Type: geometry_msgs/Twist
    
    Publishers: None
    
    Subscribers:
    
    - /turtlesim ([http://ubuntu:34483/](http://ubuntu:34483/))
    
    ```bash
    rosmsg show geometry_msgs/Twist
    ```
    
    geometry_msgs/Vector3 linear
    float64 x
    float64 y
    float64 z
    geometry_msgs/Vector3 angular
    float64 x
    float64 y
    float64 z
    
3. Write a simple ROS program called turtlesim_pose.py, which subscribes to the topic of the pose, and then prints the position of the robot in the callback function.
    
    ![Untitled](/images/2023-07-24/Untitled.png)
    
4. Complete the previous code to add a publisher to the velocity and make the robot move for a certain distance.
    
    ![Untitled](/images/2023-07-24/Untitled%201.png)