---
layout: post
title: "ROS Introduction"
description: "An Introduction to ROS"
date: 2023-07-18
feature_image: 
tags: [ROS, Raspberry Pi, Linux]
---

A study note for the introduction to ROS.

<!--more-->

# ROS Introduction

![Untitled](/images/2023-07-18/Untitled.png)

![Untitled](/images/2023-07-18/Untitled%201.png)

### Publisher/Subscriber

![Untitled](/images/2023-07-18/Untitled%202.png)

### Services

![Untitled](/images/2023-07-18/Untitled%203.png)

### ActionLib

![Untitled](/images/2023-07-18/Untitled%204.png)

### Path Planning

- Global Path Planner
- Local Path Planner

## ROS Limitations

- Single robot (cannot communicate between robots)
- Not real-time (UDP/TCP; no priority)
- Need reliable network (nodes need to communicate; each node consume a bandwidth)