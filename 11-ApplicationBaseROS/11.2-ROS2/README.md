# ROS2 介绍

ROS2的前身是ROS，ROS就是机器人操作系统（Robot Operating System）。 但ROS本身并不是一个操作系统，而是一个软件库和工具集。
Ros的出现解决了机器人各个部件的通信问题。 后来，越来越多的机器人算法被集成到ROS中。 ROS2继承了ROS，比ROS更强大更好用。

## 1 ROS2的设计目标和特点

ROS2肩负着改变智能机器人时代的历史使命。 在设计之初，就考虑到满足各种机器人应用的需求。

* **多机器人系统：** 未来机器人不再是独立的个体，机器人之间也需要交流和协作。 ROS2为多机器人系统的应用提供了标准的方法和通信机制。
  
* **跨平台：** 机器人应用场景不同，使用的控制平台也会有很大差异。 为了让所有的机器人都能运行ROS2，ROS2可以跨平台运行在Linux、Windows、MacOS、RTOS上。
  
* **实时：** 机器人运动控制和许多行为策略都要求机器人是实时的。 例如，机器人必须在 100 毫秒内可靠地检测到前方的行人，或在 1 毫秒内完成运动学和动力学计算。 ROS2 是像这样实时提供基本要求的。

* **产品化：** 大量的机器人已经进入我们的生活，未来还会越来越多，ROS2不仅可以用于机器人研发阶段，还可以直接安装在 产品并进入消费市场。 这也对ROS2的稳定性和鲁棒性提出了巨大的挑战。
  
* **项目管理：** 机器人开发是一项复杂的系统工程。 设计、开发、调试、测试、部署全过程的项目管理工具和机制也将在ROS2中得到体现，方便我们开发机器人。

## 2 发行版本

ROS2和Ubuntu对应的发行版本和维护周期。

| **ROS2 版本** | **发布日期** | **维护期限** | **Ubuntu 版本** |
| :--------: | :------------------: | :-------------: | :-------------: |
| [Dashing](http://docs.ros.org/en/dashing/index.html)     | 2019.5 | 2021.5 | Ubuntu 18.04 (Bionic Beaver)  |
| [Eloquent](http://docs.ros.org/en/eloquent/index.html)     | 2019.11| 2020.11 | Ubuntu 18.04 (Bionic Beaver)  |
| [Foxy](http://docs.ros.org/en/foxy/index.html)     | 2020.6 | 2023.5 | Ubuntu 20.04(Focal Fossa)  |
| [Galactic](http://docs.ros.org/en/galactic/index.html) | 2021.5 | 2022.11 |Ubuntu 20.04(Focal Fossa)  |
| [Humble](http://docs.ros.org/en/humble/index.html)   | 2022.5 | 2027.5 | Ubuntu 22.04(Jammy Jellyfish)  |

## 3 ROS和ROS2的比较

ROS2重新设计了系统架构。 两代ROS的架构变化如下：

<img src =../../resources/11-ApplicationBaseROS/ros-ros2.png
width ="500"  align = "center">

- **OS Layer：** OS层。在ROS2中，它可以构建在linux或其他系统上，甚至是没有操作系统的裸机。

- **Middleware Layer：** 中间件层。ROS1的通信系统基于TCPROS/UDPROS，而ROS2的通信系统基于DDS。 DDS是分布式实时系统中数据发布/订阅的标准解决方案。

- **Application Layer：** 应用层。ROS1依赖于ROS Master，而在ROS2中，节点之间使用了一种名为“Discovery”的发现机制来帮助彼此建立连接。

ROS设计了一套完整的通信机制（主题、服务、参数、动作）来简化机器人开发。 通过这种机制，可以连接机器人的各个部件。 这种机制设计了一个叫做Ros Master的节点，所有其他组件的通信都必须经过master节点。 一旦主节点挂掉，就会导致整个机器人系统的通信崩溃！ 所以不能利用Ros的不稳定性来做一些自动驾驶等高风险的机器人。 此外，还有以下缺点：

* 基于TCP的通信实时性差，系统开销大
* 对 python3 支持不友好
* 消息机制不兼容
* 无加密机制，安全性低

ROS2首先移除ROS中存在的master节点。 去掉主节点后，各个节点可以通过DDS节点相互发现，各个节点是平等的，可以实现一对一、一对多、多对多的通信。 使用DDS进行通信后，可靠性和稳定性得到了增强。

与只支持Linux系统的**ROS**相比，**ROS2**还支持windows、mac甚至RTOS平台。

---

[← 上一节](../11.1-ROS1/README.md) | [下一页 →](11.2.1-EnvironmentBuilding.md)
