# ROS

ROS is an open source meta-operating system for robots. It provides services that an operating system should have, including hardware abstraction, low-level device control, implementation of common functions, message passing between processes, and package management. It also provides the tools and library functions needed to obtain, compile, write, and run code across computers.

The ROS runtime "graph" is a loosely coupled peer-to-peer process network based on the ROS communication infrastructure. ROS implements several different communication methods, including a services mechanism based on synchronous RPC-style communication, a topic mechanism based on asynchronous streaming data, and a parameter server for data storage.

ROS is not a real-time framework, but ROS can be embedded in real-time programs. Willow Garage's PR2 robot uses a system called pr2_etherCAT to send or receive ROS messages in real time. ROS also integrates seamlessly with the Orocos real-time toolkit.

**ROS icon**:

![ROS icon](../../resources/11-ApplicationBaseROS/Ros-icon.png)

## 1 Design goals and features of ros

Many people are asking "What is the difference between ROS and other robot software platforms?" This is a difficult question to answer. Because ROS is not a framework that integrates most functions or features. In fact, the main goal of ROS is to provide support for code reuse for robotics research and development. ROS is a distributed process (node) framework that is encapsulated in a set of packages and function packages that are easy to share and publish. ROS also supports a federated system similar to a code repository, which can also enable project collaboration and release. This design allows the development and implementation of a project to be completely independent from the file system to the user interface (not restricted by ROS). At the same time, all projects can be integrated by ROS basic tools.

To support the main goal of sharing and collaboration, the ROS framework has several other features:

* Streamlined: ROS is designed to be as streamlined as possible so that code written for ROS can be used with other robot software frameworks. The inevitable conclusion from this is that ROS can be easily integrated with other robot software platforms: ROS can already be integrated with OpenRAVE, Orocos and Player.
* ROS-insensitive libraries: The preferred development model for ROS is all written with clean library functions that do not rely on ROS.
* Language independent: The ROS framework can be easily implemented using any modern programming language. ros has been implemented in Python version, C++ version and Lisp version. It also has Java and Lua versions of the experimental library.
* Loose coupling: Function modules in ROS are encapsulated in independent function packages or meta-function packages for easy sharing. The modules in the function package run in units of nodes, using ROS standard IO as the interface. Developers do not need to pay attention to the internal implementation of the module. As long as you understand the interface rules, you can achieve reuse and achieve point-to-point loose coupling between modules.
* Convenient testing: ROS has a built-in unit/integration testing framework called rostest, which can easily install or uninstall test modules.
* Scalable: ROS can be adapted to large runtime systems and large development processes.
* Free and open source: many developers and many feature packages


## 2 Why use ROS

Through ROS, we can realize simulation control of the robotic arm in a virtual environment.

We will use the **rviz** platform to visualize the robotic arm and use a variety of methods to operate our robotic arm; we will use the **moveit** platform to plan and execute the robotic arm's action path to achieve free control of the machine. arm effect.

We will learn in the next chapters how to control the control of our products through the platform in ros.

#MoveIt

**MoveIt** is currently the most advanced software for robotic arm movement operations and has been used on more than 100 robots. It integrates the latest achievements in motion planning, control, 3D perception, motion control, control and navigation, provides an easy-to-use platform for the development of advanced robot applications, and provides a comprehensive solution for the design and integration of new robot products in industrial, commercial and R&D fields. Provides an integrated software platform for evaluation.

**MoveIt Icon**:

![moveit icon](../../resources/11-ApplicationBaseROS/moveit-icon.png)

## 1 Introduction

MoveIt is an integrated development platform in ROS, consisting of a variety of function packages for manipulating robotic arms, including: motion planning, operation, control, inverse kinematics, 3D perception and collision detection, etc.

The figure below shows the high-level structure of the main node **move_group** provided by Moveit. It is like a combiner: integrating all individual components together to provide a series of actions and services for users to use.

<img src =../../resources/11-ApplicationBaseROS/moveit-3.png
width ="500" align ="center">

## 2 User interface

Users can access the operations and services provided by move_group in three ways:

* In C++: Use the move_group_interface package to conveniently implement move_group.
* In Python: Use moveit_commander package.
* Via GUI: Using Motion-commander's Rviz (ROS visualization tool).

move_group can be configured using the ROS parameter server, from which the robot's URDF and SRDF can also be obtained.

## 3 Configuration

move_group is a ROS node. It uses the ROS parameter server to obtain three kinds of information:

1. URDF - move_group looks up the robot_description parameter on the ROS parameter server to get the robot's URDF.

2. SRDF - move_group looks up the robot_description_semantic parameter on the ROS parameter server to get the robot's SRDF. SRDF is typically created by the user using the MoveIt Setup Assistant.

3. MoveIt configuration - move_group will look for additional configuration specific to MoveIt on the ROS parameter server, including joint constraints, kinematics, motion planning, perception and other information. Configuration files for these components are automatically generated by the MoveIt Setup Assistant and stored in the configuration directory of the robot's corresponding MoveIt configuration package. To use the configuration assistant, please refer to: [MoveIt Setup Assistant](https://moveit.picknik.ai/main/doc/examples/setup_assistant/setup_assistant_tutorial.html)

---

[← Previous page](../../6-SDKDevelopment/python/PyhtonAPI.md) | [Next page →](11.1.1-EnvironmentBuilding.md)