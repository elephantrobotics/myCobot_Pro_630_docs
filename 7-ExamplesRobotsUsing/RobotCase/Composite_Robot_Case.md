# 复合机器人案例

Ranger Mini V3.0:

![](../../resources/7-ExamplesRobotsUsing/RobotCase/ranger_mini_v2.png)


## 设备环境

Ranger mini V3.0、myCobot Pro 630、Jetson Orin nano开发板、Realsense D435i相机、2D N10P雷达

## Ranger mini 3.0电气接口说明

![](../../resources/7-ExamplesRobotsUsing/RobotCase/infter.png)

RANGER MINI 3.0 底盘尾部配置有一个航空扩展接口，航空扩展接口配置了一组电源以及一组CAN通讯接口。便于使用者给扩展设备提供电源（负载电流不能超过15A，电压范围46~50V），以及通讯使用。其具体引脚定义如下图所示。需要注意的是，这里的扩展电源受内部控制，当电池电压低于安全电压会主动切断供电，所以用户需要注意，在达到临界电压前RANGER MINI 3.0 底盘平台会通过前灯闪烁通知，用户在使用过程中注意充电。

![](../../resources/7-ExamplesRobotsUsing/RobotCase/infter2.png)

|  **引脚编号**  |  **引脚类型**  |  **功能及定义**  |  **备注**  |
| :----------- | :--------- |:----------- | :---------    |
|1	|电源	|VCC	|电源正，电压范围46~50V, 负载电流不能超过15A|
|2	|电源	|GND	|电源负|
|3	|CAN	|CAN_H	|CAN总线高|
|4	|CAN	|CAN_L	|CAN总线低|

## 小车遥控功能说明

使⽤遥控器可以轻松控制RANGER MINI V3.0通⽤机器⼈底盘移动，其定义及其功能如下：

![](../../resources/7-ExamplesRobotsUsing/RobotCase/infter3.png)

### 按键功能定义 

SWB为控制模式选择拨杆，拨至最上方为指令控制模式，拨至中间或下方为遥控控制模式；SWA为灯光控制开关，拨到下方为关闭灯光（需SWB先进入遥控模式）；SWC拨到下方为驻车模式，此时四轮四转向呈X形锁止；

**SWD为底盘运动模式设置开关**：SWD拨到上为①前后阿克曼和②自旋模式  ①左摇杆控制速度，右摇杆控制转角；②左摇杆不动，右摇杆左右方向控制自旋；

**SWD拨到下为斜移模式：** 左摇杆控制速度，右摇杆控制转角（最大角度90°即为横移）；

**电压/电流驱动模式切换：**
需要先把 SWC 拨到下方进入驻车状态，然后SWB拨到最下，SWC再拨到最上退出驻车状态就可以切换完成

**零点校准：**
首先将 SWA 拨杆打到最下面;SWB 打到最上面;SWD 打到最下面;
左摇杆四个方位代表指定对应四个位置的转向电机（例如：右上指右上角转向电机，左上指的是左上角转向电机），右摇杆左右方向调节转角，左滚轮可两个方向位置累加调节SWC为调节灵敏度:DOWN→粗调MID→中间挡 UP→微调，Key1设定当前位置为零点。

**任何情况下按下KEY1 = 强制清除底盘所有错误 注意！！仅在确保安全的特殊情况下可使用**

**POWER**为电源按钮，同时按住即可开机 。

### 遥控控制基本操作流程

启动之前需要**确保 RANGERMINI 的轮子和底盘平行朝着正前方**，正常启动RANGERMINI 3.0 移动机器人底盘后（尾部有电源开关按钮，按下打开电源启动小车），启动遥控器，将SWB切换为遥控控制模式，即可通过遥控器控制RANGERMINI平台运动。

**注意：使用遥控器摇杆进行操作时，需缓慢轻推摇杆，避免速度过快。当小车顶部有载重时，速度过快容易出现重心不稳，影响运动控制的平稳性。**

## 小车CAN总线连接

- 将顶部航空插头或者尾部插头CAN线引出，将CAN线中的CAN_H和CAN_L分别与CAN_TO_USB适配器相连；
- 打开移动机器人底盘旋钮开关，检查来两侧的急停开关是否释放； 
- 将CAN_TO_USB连接至笔记本的usb口。连接示意如图所示。

![](../../resources/7-ExamplesRobotsUsing/RobotCase/can.png)

## 安装依赖包

```bash
sudo apt-get update
sudo apt-get install build-essential git cmake libasio-dev libpcap-dev libboost-all-dev
sudo apt install ros-noetic-joint-state-publisher-gui -y
sudo apt install ros-noetic-ros-controllers -y
sudo apt install ros-noetic-gmapping -y
sudo apt install ros-noetic-map-server -y
sudo apt install ros-noetic-navigation -y
```

## 下载程序代码

```bash
cd ~/catkin_ws/src
git clone -b ranger_mini3.0 https://github.com/elephantrobotics/mc_embodied_kit_ros.git
cd ..
catkin_make
soure devel/setup.bash

```

## 雷达串口映射

```bash
cd ~/catkin_ws/src/mc_embodied_kit_ros
sudo chmod +x wheeltec_udev.sh
sudo ./wheeltec_udev.sh
```

执行执行成功之后，重新拔插设备，输入下面命令验证：

```bash
ls -l /dev/wheeltec_lidar
```

若提示没有该设备名称，则查看 `/etc/udev/rules.d/`目录下是否有相对应的规则文件（`wheeltec_lidar*.rules`)

## 测试CAN通信

- 为确保CAN总线使能，每次打开电源、系统重启都需要运行此命令：

```bash
cd ~/catkin_ws && source devel/setup.bash
rosrun ranger_bringup setup_can2usb.bash
```

- 如果已经将can-to-usb连接到小车，并且小车已经开机、CAN总线已经使能、使用以下命令监控TRACER底盘的数据：

```bash
candump can0
```

若底盘数据正常，终端会一直输出如下数据：

![](../../resources/7-ExamplesRobotsUsing/RobotCase/can_data.png)

## 雷达建图导航

### 1 CAN总线使能

为确保CAN总线使能，每次打开电源、系统重启都需要运行此命令：

```bash
cd ~/catkin_ws && source devel/setup.bash
rosrun ranger_bringup setup_can2usb.bash
```

### 2 启动小车底层通信

启动小车底层节点和雷达通信，打开一个终端，运行以下命令：

```bash
cd ~/catkin_ws && source devel/setup.bash
roslaunch ranger_odometry ranger_active.launch
```

**注意：** 启动底盘节点前需确保CAN总线已经使能，系统重启或者重新拔插CAN总线，都需要执行使能指令： `rosrun ranger_bringup setup_can2usb.bash`

### 3 运行建图程序

打开一个终端，运行以下命令：

```bash
cd ~/catkin_ws && source devel/setup.bash
roslaunch ranger_navigation mapping.launch
```

### 3 开始建图

现在，底盘小车可以在手柄的遥控下移动了。同时，您可以在 Rviz 空间中观察到，随着小车的移动，我们的地图也在逐渐构建。

注意：为了获得更好的地图绘制效果，建议在操作手柄遥控器时缓慢推动摇杆并以低速行驶，因为较低的速度往往会产生更好的地图绘制效果。

### 4 保存构建地图

打开另一个新的终端控制台，在命令行中输入以下命令，保存 ranger 扫描的地图：

```bash
cd ~/catkin_ws/src/mc_embodied_kit_ros/ranger_navigation/map

rosrun map_server map_saver

```

执行成功后，将在当前路径(`~/catkin_ws/src/mc_embodied_kit_ros/ranger_navigation/map`)下生成两个默认地图参数文件，即map.pgm和map.yaml。

### 5 地图导航+PRO630运动

>> 注意：开始导航之前，建议将小车的初始位置放在绘制地图时小车所在的起点位置。

在此之前，我们已经成功创建了空间地图，并获得了一组地图文件，即位于 `~/catkin_ws/src/mc_embodied_kit_ros/ranger_navigation/map` 目录下的 map.pgm 和 map.yaml。

#### 5.1 启动小车底层通信

>> 注意：若已启动，请忽略此操作

启动小车底层节点和雷达通信，打开一个终端，运行以下命令：

```bash
cd ~/catkin_ws && source devel/setup.bash
roslaunch ranger_odometry ranger_active.launch
```

#### 5.2 启动导航程序

打开一个终端，输入以下命令运行：

```bash
cd ~/catkin_ws && source devel/setup.bash
roslaunch ranger_navigation navigation_active.launch
```

程序启动成功之后，可以在rviz界面进行导航操作，小车从A点移动到B点，myCobot Pro 630执行相关动作，效果demo如下：

<video id="my-video" class="video-js" controls preload="auto" width="100%"
poster="" data-setup='{"aspectRatio":"16:9"}'>
  <source src="../../resources/7-ExamplesRobotsUsing/RobotCase/ranger_miniV3.0_630.mp4" type='video/mp4' >
</video>

## Realsense 3D相机使用

### 依赖库安装

1. 注册服务器的公钥：

    ```bash
    sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-key F6E65AC044F831AC80A06380C8B3A55A6F3EFCDE || sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-key F6E65AC044F831AC80A06380C8B3A55A6F3EFCDE
    ```

2. 将服务器添加到存储库列表中：

    ```bash
    sudo add-apt-repository "deb https://librealsense.intel.com/Debian/apt-repo $(lsb_release -cs) main" -u
    ```

3. 安装SDK：

    ```bash
    sudo apt-get install librealsense2-utils librealsense2-dev
    ```

### 验证使用

打开控制台终端，输入以下命令：

```bash
realsense-viewer
```

更多使用详情请参考:[Jetson Installation Guide](https://github.com/IntelRealSense/librealsense/blob/master/doc/installation_jetson.md)