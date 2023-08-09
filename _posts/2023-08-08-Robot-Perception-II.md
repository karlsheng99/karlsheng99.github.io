---
layout: post
title: "Robot Perception II"
description: "Robot Perception II"
date: 2023-08-08
feature_image: 
tags: [ROS, Laser Scanner, Raspberry Pi, Linux]
---

A study note for Robot Perception in ROS with Laser Scanner.

<!--more-->

# Perception II

### Laser Scanner

- Measure the distance to obstacles
- Uses laser beams
- Characteristics / parameteres:
    - Minimum angle: start angle
    - Maximum angle: end angle
    - Angle increment: angular distance between measurements
    - Time increment: time between measurements
    - Scan time: time between two scans
    - Minimum range: min observation range
    - Maximum range: max observation range
    - List of ranges: list of all measurements in a scan
    - List of intensities: list of all intensities in a scan
    

## Assignment 6

### The Move-Stop-Rotate Behavior for Obstacle Avoidance

We will first start with a very simple program to make the robot move around

1. First, make sure to install Turtlebot 3 Robot, as shown in the Section "Getting Started with Turtlebot3". It is recommended to use the latest version of ROS, which is ROS Noetic, although it should work on any version.
2. Start the Turtlebot3 Robot in the maze environment `roslaunch turtlebot3_gazebo turtlebot3_world.launch`
3. Start RIVIZ for Virualization `roslaunch turtlebot3_gazebo turtlebot3_gazebo_rviz.launch`
4. Observe the laser scanner in red dots in RVIZ. You can check the thickness of the laser scanner by changing the Size (m) attribute in rviz to 0.04 instead of 0.01. This will provide better visualization of the laser scanner topic.
5. Run the `teleop` node `roslaunch turtlebot3_teleop turtlebot3_teleop_key.launch`. Make the robot move and observe how the laser scanner layout is changing in `rviz`.
6. Now, develop a ROS program in Python AND in C++ to make the robot moves in a straight line, and stops when the closest obstacles become at a distance less than 0.6 meters. Use a laser bean around the center of [-5,+5] degrees.
7. Then, develop another function that makes the robot rotates until the straight obstacle distance in the same beam aperture becomes greater than 3 meters.
8. Make a loop to repeat these two functions and observe if the robot succeeds to move without hitting the obstacle forever or not.
9. Try the same program with the house environment `roslaunch turtlebot3_gazebo turtlebot3_house.launch`. What are your observations?

### A PID Controller

The motion behavior in the previous solution is not smooth as there are several motions interrupted by a stop.

The objective of this second assignment is to develop a Proportional controller that regulates the angular speed and the linear speed such as it moves smoothly without hitting obstacles.

- The linear velocity can be adjusted to be proportional to the distance (similar to what we did in Go-to-Goal Behavior)
- The angular velocity can be adjusted based on the distance to the obstacles on the left side and the distance to obstacles on the right side.
- If the distance to the left side obstacle is much closer than the right side obstacles, then make the robot rotates smoothly to the right.
- If the distance to the right side obstacle is much closer than the left side obstacles, then make the robot rotates smoothly to the left.
- Test the code on Turtlebot3 in the maze environment and house environment.
- Test it on a real robot if you have one (any kind of real robot).

[![Watch the video](https://youtu.be/H-VPotndE4I/maxresdefault.jpg)](https://youtu.be/H-VPotndE4I)


