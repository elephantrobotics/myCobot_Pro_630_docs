# **气动夹爪**

> **兼容型号：** myCobot 320、myCobot Pro 630、myCobot Pro 600

## 产品图片

<img src="../../../resources/1-ProductIntroduction/1.4/1.4.1-Gripper/3-PneumaticGripper/气动夹爪1.jpg" alt="img-2" width="800" height="auto" /> <br>

## 规格

| **名称**     | **mycobot 气动夹爪**                                |
| :----------- | :----------------------------------------------------- |
| 模型         | myCobotPro_Gripper_Air_10                              |
| 材料         | 金属 + 7500 尼龙                                       |
| 夹取范围     | 0-8mm                                                  |
| 夹紧力       | 外径 34N 内径 45N                                      |
| 驱动模式     | 气动                                                   |
| 传输方式     | 活塞缸                                                 |
| 尺寸         | 67.3×38×23.6mm                                         |
| 重量         | 180g                                                   |
| 固定方法     | 螺丝固定                                               |
| 使用环境要求 | 常温常压                                               |
| 控制接口     | 输入/输出控制                                          |
| 适用设备     |  myCobot 320 系列、 myCobot Pro 630、 myCobot Pro 600 |
<!-- | 重复性精度   | ±0.01mm                                                |
| 使用寿命     | 一年                                                   | -->
## 用于抓取物体

**引言**

- 气动夹爪又称气动手指或气动夹钳，是一种利用压缩空气作为动力抓取或抓取工件的执行器。它体积小、重量轻、外形紧凑，能够实现单向和双向抓取、自动对中、高重复精度和自动控制磁性开关。

- 气动夹爪套件包括夹爪法兰、气泵、φ8 气管、φ6 气管、φ8-6 快速接头、电磁阀和电缆。其主要功能是代替人力抓取工作，可有效提高生产效率和工作安全性。需要外接吸气泵。

**工作原理**

- 单活塞：轴驱动曲柄，气爪由活塞驱动开合。两个爪片上分别布置有相应的曲柄槽。为减小摩擦阻力，爪片与机身之间采用钢珠滑轨结构连接。

- 双活塞：由两个活塞控制，每个活塞通过一个滚轮和一个双曲柄与一个气动指连接，形成一个特殊的驱动单元。需要注意的是，气动指始终向中心轴向移动，每个气动指不能独立移动。

- 平行钳形气缸：如果气动指朝相反方向移动，则先前被压缩的活塞处于排气状态，而另一个活塞处于压缩状态。

**适用对象**

- 体积小于夹紧行程

- 重量小于最大夹紧重量

- 自定义指尖可扩展更多用法

**安装使用**

- 需要配合空压机使用：
  ![alt text](../../../resources/1-ProductIntroduction/1.4/1.4.1-Gripper/3-PneumaticGripper/a1.png)

  1. 将黑色插头插入排插；

  2. 将搭配的红色软管插入机器上的接口：  
     ![alt text](../../../resources/1-ProductIntroduction/1.4/1.4.1-Gripper/3-PneumaticGripper/a2.png)
  3. 红色按钮为开关，往外拔即打开，按回去则关闭机器：
     ![alt text](../../../resources/1-ProductIntroduction/1.4/1.4.1-Gripper/3-PneumaticGripper/a3.png)

- 夹爪安装：

  
  1. 将空压机红色软管的另一端接上电磁阀的接口：
     ![alt text](../../../resources/1-ProductIntroduction/1.4/1.4.1-Gripper/3-PneumaticGripper/a4.png)
  2. 将电磁阀另一端再拧开一个接口供启动夹爪控制开合使用：
     ![alt text](../../../resources/1-ProductIntroduction/1.4/1.4.1-Gripper/3-PneumaticGripper/a5.png)
     ![alt text](../../../resources/1-ProductIntroduction/1.4/1.4.1-Gripper/3-PneumaticGripper/a6.png)
  3. 用配套的两根透明软管，一端接在电磁阀的两个接口：
     ![alt text](../../../resources/1-ProductIntroduction/1.4/1.4.1-Gripper/3-PneumaticGripper/a7.png)
  4. 透明软管另一端接在夹爪的两个接口上：
     ![alt text](../../../resources/1-ProductIntroduction/1.4/1.4.1-Gripper/3-PneumaticGripper/a8.png)
  5. 用配套螺丝将夹爪固定在机械臂末端：
     ![alt text](../../../resources/1-ProductIntroduction/1.4/1.4.1-Gripper/3-PneumaticGripper/a9.png)

- 电气连接：

  1. 连接线黑色接机械臂底座 GND，红色接 OUT1~OUT6 任意一个，根据选择的接口更改后续程序的引脚号，这里使用 OUT1：
     ![alt text](../../../resources/1-ProductIntroduction/1.4/1.4.1-Gripper/3-PneumaticGripper/a10.png)

## 3 通过 python 控制

**使用前需要先启动机器人系统**
![](../../../resources/1-ProductIntroduction/1.4/poweron/poweron.png)
![](../../../resources/1-ProductIntroduction/1.4/poweron/poweron2.png)

确认机械臂的IP地址：终端输入 ifconfig 获取
![](../../../resources/1-ProductIntroduction/1.4/poweron/ip.png)


```python
from pymycobot import ElephantRobot
import time

# 将ip更改成P600树莓派的实时ip

elephant_client = ElephantRobot("192.168.10.158", 5001)

# 启动机器人必要指令
elephant_client.start_client()
time.sleep(1)

elephant_client.set_digital_out(0,1)
time.sleep(2)

elephant_client.set_digital_out(0,0)
time.sleep(2)




```


<!-- ## 购买链接

- [淘宝](https://shop504055678.taobao.com)
- [shopify](https://shop.elephantrobotics.com/)

## 如何使用

1 安装夹具: <br>

<img src="../../../resources/1-ProductIntroduction/1.4/1.4.1-Gripper/3-PneumaticGripper/气动夹爪2.jpg" alt="img-2" width="400" height="auto" /> <br>

<img src="../../../resources/1-ProductIntroduction/1.4/1.4.1-Gripper/3-PneumaticGripper/气动夹爪3.jpg" alt="img-2" width="400" height="auto" /> <br> -->

[← 上一页](./2-ElectricGripper.md) | [下一页 →](./4-FlexibleGripper.md)
