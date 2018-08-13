# Overview
This project is for controlling one or more Bitcraze Crazyflies in ROS using python.
With this software, you can write your own autonomous navigation programs by
retrieving the vehicle telemetry (such as sensor data) and transmitting movement commands.
Writing navigation programs with this software is simple and flexible.
Users are free to interact with the Crazyflies either through ROS topics and actions, or through a wrapper of the official Bitcraze python API.
This allows users familiar with ROS to quickly integrate their crazyflies with part of a larger robotic system,
while also providing an appropriate starting point beginners.

This project uses a client server architecture. In this model, the user's
program (a ROS node) interacts with a client API that handles communication with the back-end server.
The server (a separate ROS node) maintains a radio connection to each Crazyflie in the environment, and implements
the control and data logging functions using crazyflie-lib-python.

# Dependencies
To use this project, you will need
- Ubuntu (tested on 16.04)  
- Python (tested on 2.7)
- a ROS distribution (tested on Kinetic Kame)
- ROS dependencies for building packages
- Bitcraze crazyflie-lib-python

To install ROS and the dependences for building packages, please follow the [official instructions](http://wiki.ros.org/ROS/Installation).

To install crazyflie-lib-python, follow the instructions in the [readme](https://github.com/bitcraze/crazyflie-lib-python#development) under development. Note that you do not have to fork the repository - if you would prefer, just clone it from [https://github.com/bitcraze/crazyflie-lib-python.git]

# Installation
To install this project, open a terminal and create a catkin workspace

`mkdir catkin_ws/src; cd catkin_ws/src; catkin_init_workspace`

Then clone this repository

`git clone https://github.com/jgsuw/rospy-crazyflie.git`

Now change directory back to `catkin_ws` and build the package, then install

`cd ..`
`catkin_make rospy_crazyflie; catkin_install rospy_crazyflie`

Lastly, source the devel and install directories into your environment

`source devel/setup.bash; source install/setup.bash`

# Getting Started
## Starting a server
Before you can run a client program, you first need to start the server. If the project is built properly, you can launch the server like so
`roslaunch rospy_crazyflie default.launch`
The default launch file starts a server node with the name crazyflie_server. Refer to this server name in your client program.
## Run an example
Now that the server is running, you can try executing the takeoff and landing example script like so
`roscd rospy_crazyflie/examples`
`python takeoff_landing.py`
This example will tell the crazyflie to takeoff to a height of .5 meters, and will hover until the user hits enter in the console.
Please note that without a [FlowDeck](https://www.bitcraze.io/flow-deck/) the crazyflie will drift over time, or without a [Z-ranger deck](https://www.bitcraze.io/z-ranger-deck/) the crazyflie will not be able to hold altitude.