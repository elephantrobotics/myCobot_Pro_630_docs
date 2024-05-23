# SDK Development Guide

- [1 Developed and used based on python API](./6.1-Python/6.1.2-ApplicationBasePython.md)
The python API is an interface for interactive control of external devices by the Elephant collaborative robot. It provides functions such as coordinate control, angle control, io control, trajectory recording, and gripper control.

<div align=center><img src="../resources/6-SDKDevelopment/pythonlogo.jpg"></div>


- [2 Development and use based on ROS](../11-ApplicationBaseROS/11.1-ROS1/README.md)
   ROS is open source and is a post-operating system, or secondary operating system, for robot control. Through ROS, we can realize simulation control of the robotic arm in a virtual environment. We will use the rviz platform to visualize the robotic arm and use a variety of methods to operate our robotic arm; we will use the moveit platform to plan and execute the robotic arm's action path to achieve the effect of freely controlling the robotic arm. The system that comes with myCobot_Pro_630 does not support ROS, but we can use ROS by using the Socket connection of the Ubuntu system in the virtual machine on the PC. After users install the ROS development environment on the PC, they can view the use cases and use of moveit. .

   <div align=center><img src="../resources/2-serialproduct/myCobot Pro 600/Chinese/ros.jpg"></div>

---
[← Previous page](../5-BasicApplication/5.2-ApplicationUse.md) | [Next page → ](./python/PyhtonAPI.md)