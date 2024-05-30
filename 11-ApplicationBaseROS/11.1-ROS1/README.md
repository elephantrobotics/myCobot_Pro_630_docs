# ROS

ROS是用于机器人的开源的元操作系统。它提供了操作系统应有的服务，包括硬件抽象、低级设备控制、常用功能的实现、进程之间的消息传递以及包管理。它也提供用于获取、编译、编写、和跨计算机运行代码所需的工具和库函数。

ROS 运行时的“graph”是一种基于ROS通信基础结构的松耦合点对点进程网络。ROS实现了几种不同的通信方式，包括基于同步RPC样式通信的服务（services）机制，基于异步流媒体数据的话题（topics）机制以及用于数据存储的参数服务器。

ROS并不是一个实时的框架，但ROS可以嵌入实时程序。Willow Garage的PR2机器人使用了一种叫做 pr2_etherCAT 的系统来实时发送或接收 ROS 消息。ROS还可以与Orocos 实时工具包无缝集成。

**ROS 图标** ：

![ROS图标](../../resources/11-ApplicationBaseROS/Ros-icon.png)

## 1 ros 的设计目标和特点

很多人都在问“ROS与其它机器人软件平台有什么不同？”这是一个很难解答的问题。因为ROS不是一个集成了大多数功能或特征的框架。事实上，ROS 的主要目标是为机器人研究和开发提供代码复用的支持。ROS是一个分布式的进程（也就是节点）框架，这些进程被封装在易于被分享和发布的程序包和功能包集中。ROS也支持一种类似于代码储存库的联合系统，这个系统也可以实现工程的协作及发布。这个设计可以使一个工程的开发和实现从文件系统到用户接口完全独立决策（不受ROS限制）。同时，所有的工程都可以被ROS的基础工具整合在一起。

为了支持共享和协作这一主要目标，ROS 框架还有其他几个特点：

* 精简：ROS尽可能设计的精简，以便为ROS编写的代码可以与其他机器人软件框架一起使用。由此得出的必然结论是ROS可以轻松集成在其它机器人软件平台：ROS已经可以与OpenRAVE，Orocos和Player集成。
* ROS不敏感库：ROS的首选开发模型都是用不依赖ROS的干净的库函数编写而成。
* 语言独立：ROS框架可以简单地使用任何的现代编程语言实现。ros已经实现了Python版本，C++版本和 Lisp版本。同时也拥有Java 和 Lua版本的实验库。
* 松耦合:ROS中功能模块封装于独立的功能包或元功能包，便于分享，功能包内的模块以节点为单位运行，以ROS标准的IO作为接口，开发者不需要关注模块内部实现，只要了解接口规则就能实现复用,实现了模块间点对点的松耦合连接
* 方便测试：ROS内建一个了叫做rostest的单元/集成测试框架，可以轻松安装或卸载测试模块。
* 可扩展：ROS可以适用于大型运行时系统和大型开发进程。
* 免费且开源：开发者众多，功能包多


## 2 为什么使用ROS

通过ROS，我们能够在虚拟环境中实现对机械臂的仿真控制。

我们将通过 **rviz** 平台实现对机械臂的可视化，并使用多种方式对我们的机械臂进行操作；通过 **moveit** 平台进行机械臂行动路径的规划和执行，达到自由控制机械臂的效果。

我们将在接下来的章节中学习如何通过ros中的平台对我们产品的控制进行控制。

# MoveIt

**MoveIt** 是目前针对机械臂移动操作的最先进的软件，已在 100 多个机器人上使用。它综合了运动规划、控制、3D 感知、运控学、控制和导航的最新成果，提供了开发先进机器人应用的易用平台，为工业、商业和研发等领域的机器人新产品的设计和集成体用评估提供了一个集成化软件平台。

**MoveIt 图标** :

![moveit图标](../../resources/11-ApplicationBaseROS/moveit-icon.png)

## 1 简介

MoveIt 是ROS中的一个集成开发平台，由多种用于操纵机械臂的功能包组成，包括：运动规划、操作、控制、逆运动学、3D感知和碰撞检测等。

下图所示为 Moveit 提供的主要节点 **move_group** 的高层结构，它像一个组合器：把所有单独的组件集成在一起，提供一系列的 actions 和 services 供用户使用。

<img src =../../resources/11-ApplicationBaseROS/moveit-3.png
width ="500"  align = "center">

## 2 用户界面

用户可以通过三种方式访问move_group提供的操作和服务：

* 在C++ ： 使用move_group_interface包可以方便实用move_group。
* 在 Python ： 使用moveit_commander包。
* 通过 GUI ： 使用 Motion——commander 的 Rviz（ROS可视化工具）。

move_group可以使用ROS参数服务器进行配置，从中还可以获取机器人的URDF和SRDF。

## 3 配置

move_group是一个 ROS 节点。它使用ROS参数服务器来获取三种信息：

1. URDF - move_group在ROS参数服务器上查找robot_description参数，以获取机器人的URDF。

2. SRDF - move_group在 ROS 参数服务器上查找robot_description_semantic参数，以获取机器人的 SRDF。SRDF 通常由用户使用 MoveIt 设置助理创建。

3. MoveIt 配置 - move_group将在 ROS 参数服务器上查找特定于 MoveIt 的其他配置，包括关节限制、运动学、运动规划、感知和其他信息。这些组件的配置文件由MoveIt设置助手自动生成，并存储在机器人的相应MoveIt配置包的配置目录中。配置助手的使用请参考：[MoveIt Setup Assistant](https://moveit.picknik.ai/main/doc/examples/setup_assistant/setup_assistant_tutorial.html)

---

[← 上一页](../../6-SDKDevelopment/python/PyhtonAPI.md) | [下一页 →](11.1.1-EnvironmentBuilding.md)
