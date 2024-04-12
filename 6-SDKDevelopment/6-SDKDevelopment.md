# SDK 开发指南

- [ 1 基于 python API 开发使用](./6.1-Python/6.1.2-ApplicationBasePython.md)
python API是大象协作型机器人给外部设备做交互控制的接口，提供了有坐标控制、角度控制、io控制、轨迹录制、夹爪控制等功能

<div align=center><img src="../resources/6-SDKDevelopment/pythonlogo.jpg"></div>


- [2 基于 ROS 开发使用](../11-ApplicationBaseROS/11.1-ROS1/README.md)
  ROS 是开源的，是用于机器人控制的一种后操作系统，或者说次级操作系统。通过ROS，我们能够在虚拟环境中实现对机械臂的仿真控制。我们将通过 rviz 平台实现对机械臂的可视化，并使用多种方式对我们的机械臂进行操作；通过moveit 平台进行机械臂行动路径的规划和执行，达到自由控制机械臂的效果。myCobot_Pro_630自带的系统是不支持ROS的，但我们可以通过在PC端使用虚拟机中的Ubuntu系统的Socket连接使用ROS，用户在PC端安装ROS开发环境后，即可查看使用案例和moveit的使用。

  <div align=center><img src="../resources/2-serialproduct/myCobot Pro 600/Chinese/ros.jpg"></div>

---
[← 上一页](../5-BasicApplication/5.2-ApplicationUse.md) | [下一页 → ](./6.1-Python/6.1.2-ApplicationBasePython.md)