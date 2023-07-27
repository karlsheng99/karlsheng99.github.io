---
layout: post
title: "ROS Services"
description: "ROS Services"
date: 2023-07-26
feature_image: 
tags: [ROS, Raspberry Pi, Linux]
---

A study note for ROS Services.

<!--more-->

# ROS Services

### ROS service

Server / Client

- A client sends a request, the server sends back a response

When to use?

- Request the robot to perform a specific action

### List of Available Services

```bash
rosservice list
```

### Service Information

e.g.

```bash
rossrv info turtlesim/Spawn
```

turtlesim/: package

Spawn: the type of the request/response message

```bash
rosservice call /spawn 7 7 0 turtle2
```

/spawn: service request

![Untitled](/images/2023-07-26/Untitled.png)

## Assignment 3

1. Open the Turtlesim simulator
    
    ```bash
    rosrun turtlesim turtlesim_node
    ```
    
2. Display the list of services
    
    ```bash
    rosservice list
    ```
    
    /clear
    /kill
    /reset
    /rosout/get_loggers
    /rosout/set_logger_level
    /spawn
    /turtle1/set_pen
    /turtle1/teleport_absolute
    /turtle1/teleport_relative
    /turtlesim/get_loggers
    /turtlesim/set_logger_level
    
3. What is the command the information of the service /reset
    
    ```bash
    rosservice info /reset
    ```
    
4. Write the result of the execution of the command for the service /reset
    
    Node: /turtlesim
    URI: rosrpc://ubuntu:43387
    Type: std_srvs/Empty
    Args:
    
5. What is the command the information of the service /kill
    
    ```bash
    rosservice info /kill
    ```
    
6. Write the result of the execution of the command for the service /kill
    
    Node: /turtlesim
    URI: rosrpc://ubuntu:43387
    Type: turtlesim/Kill
    Args: name
    
7. spaw one additional turtle called tsim1. Write the command.
    
    ```bash
    rosservice call /spawn 3 3 2 tsim1
    ```
    
    ![Untitled](/images/2023-07-26/Untitled%201.png)
    
8. one additional turtle called tsim2. Write the command.
    
    ```bash
    rosservice call /spawn 7 7 5 tsim2
    ```
    
    ![Untitled](/images/2023-07-26/Untitled%202.png)
    
9. use the service kill to kill tsim1. Write the command.
    
    ```bash
    rosservice call /kill tsim1
    ```
    
    ![Untitled](/images/2023-07-26/Untitled%203.png)
    
10. use the service reset to reset all the simulation. Write the command.
    
    ```bash
    rosservice call /reset
    ```
    
    ![Untitled](/images/2023-07-26/Untitled%204.png)

---    
### Create a Client/Server ROS Service Application

1. Define the service message (service file)
    1. Create a srv folder in the package
    2. Create the service file with file extension “.srv”
    3. Edit the service file by adding the elements
        
        service definition e.g.
        
        ```bash
        # request message parameters
        int64 a
        int64 b
        ---
        # response message parameters
        int64 sum
        ```
        
    4. Update Dependencies in package.xml
        
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
        
    5. Update Dependencies in CMakeList.txt
        
        ```diff
        find_package(catkin REQUIRED COMPONENTS
            roscpp
            rospy
            std_msgs
        +	message_generation
        )
        ```
        
        ```diff
        add_service_files(
            FILES
        +	Add2Ints.srv
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
        
    6. Compile programs and build executables
        
        ```bash
        catkin_make
        ```
        
    7. Show the service 
        
        ```bash
        rossrv show package_name/service_name
        ```
        
2. Create ROS Server node
    1. Import the service request and response
    2. Create the service
        1. Initialize a server node with a server name
        2. Initialize a Service object with a service name, a service type, and a callback function
        3. spin()
    3. Create the callback function
        1. The callback function will be executed automatically every time a new request is received 
3. Create ROS Client node
    1. Import the service request and response
    2. Create the service client proxy
        1. Wait for the service before start communication
            1. Make sure that the client doesn’t send a request to a server that doesn’t exist
        2. Create a client(proxy) object with a service name and a service type
4. Execute the service
5. Consume the service by the client
    
## Assignment 4

1. What is the command used to create a ROS package called ros_service_assignment? Make sure to clarify the path where to create it.
    
    ```bash
    cd catkin_ws/src
    catkin_create_pkg hw4_service_rectangle_area std_msgs rospy roscpp
    ```
    
2. What is the name of the folder when to create the service file? Provide the absolute path to the file (from the root).
    
    ```
    /home/ubuntu/catkin_ws/src/hw4_service_rectangle_area/srv/RectangleAreaService.srv
    ```
    
3. What is the content of the service file RectangleAreaService.srv?
    
    ```
    float32 width
    float32 height
    ---
    float32 area
    ```
    
4. What are the changes you need to do in the CMakeLists.txt. Copy/paste the whole CMakeLists.txt.
    
    → Update Dependencies in CMakeList.txt
    
5. What are the changes you need to do the package.xml? Copy/paste the whole package.xml.
    
    → Update Dependencies in package.xml
    
6. What is the command to build the new service and generate executable files?
    
    ```bash
    catkin_make
    ```
    
7. How to make sure that service files are now created?
    
    ```bash
    rossrv show RectangleAreaService
    ```
    
    ```
    [hw4_service_rectangle_area/RectangleAreaService]:
    float32 width
    float32 height
    ---
    float32 area
    ```
    
8. Write the server application (C++ or Python)
9. Write the client application (C++ or Python)
10. What are the commands to test that the application works fine.
    
    ```bash
    roscore
    ```
    
    ```bash
    rosrun rosrun hw4_service_rectangle_area server.py
    ```
    
    ![Untitled](/images/2023-07-26/Untitled%205.png)
    
    ```bash
    rosrun hw4_service_rectangle_area client.py 3.3 4.8
    ```
    
    ![Untitled](/images/2023-07-26/Untitled%206.png)