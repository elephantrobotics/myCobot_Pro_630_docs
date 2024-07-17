# 柔性抓取器专业版

> **兼容型号:** myCobot 320, myCobot Pro 630

## 产品图片

<img src="../../../resources/1-ProductIntroduction/1.4/1.4.1-Gripper/4-FlexibleGripper/柔性夹爪1.jpg" alt="img-1" width="800" height="auto" /> <br>

**规格说明：**

| 名称 name              | myCobotPro 柔性夹爪                      |
| ---------------------- | ---------------------------------------- |
| 材料                   | 金属                                     |
| 夹持范围 clamp size    | 36-136 毫米                              |
| 最大夹持力 clamp force | 垂直 600 克 包裹 1080 克                 |
| 驱动方式 drive         | 气动                                     |
| 传动方式 transmission  | 形变                                     |
| 尺寸 size              | 170x128x195mm                            |
| 重量 weight            | 365 克                                   |
| 固定方式 fixed         | 螺丝固定                                 |
| 使用环境要求           | 常温常压                                 |
| 控制接口 control       | IO 控制                                  |
| 适用设备               |myCobot 320、myCobot Pro 600、myCobot Pro 630 |
<!-- | 重复精度 precision     | 0.5 毫米                                 |
| 使用寿命 lifetime      | 1 年                                     | -->
**柔性夹爪:** 夹取物体使用

**简介**

- 传统工业吸盘需要吸取物料的平整表面，在越来越多的工况中，吸取表面容易损伤面板或元器件，柔触夹爪捏边抓取，轻松无痕无损搬运面板，确保产品表面无瑕疵，提升良品率。
- 柔触夹爪的模块化设计，自重轻，可以按照面板尺寸自由排列组合。
- 传统气缸的夹持力普遍较大，且力度难以控制，夹持面板的边缘容易夹伤夹翘，柔性夹爪的单指夹持力精准可控，不会夹伤脆弱工件。

**工作原理**

- 柔性夹爪是研究人员模仿海星腕足的形态，研发出的一种创新型仿生柔性夹具。软爪的“手指”是由高分子硅胶柔性材料制作而成，通过充气实现弯曲形变，能够像海星一样，自适应地包覆住目标物体，可完成对异形、易损物品的柔性、无损抓取 。

**适用物体**

- 合理大小内的任意形状物体


**安装使用**

- 需要配合空压机使用：
  ![alt text](../../../resources/1-ProductIntroduction/1.4/1.4.1-Gripper/4-FlexibleGripper/a1.png)

  1. 将黑色插头插入排插；

  2. 将搭配的红色软管插入机器上的接口：  
     ![alt text](../../../resources/1-ProductIntroduction/1.4/1.4.1-Gripper/4-FlexibleGripper/a2.png)
  3. 红色按钮为开关，往外拔即打开，按回去则关闭机器：
     ![alt text](../../../resources/1-ProductIntroduction/1.4/1.4.1-Gripper/4-FlexibleGripper/a3.png)

- 夹爪安装：

 

  1. 将空压机红色软管的另一端接上气动控制器的接口：
     ![alt text](../../../resources/1-ProductIntroduction/1.4/1.4.1-Gripper/4-FlexibleGripper/a4.png)
  2. 用柔性夹爪配套的蓝色软管分别接上夹爪和气动控制器的接口：
     ![alt text](../../../resources/1-ProductIntroduction/1.4/1.4.1-Gripper/4-FlexibleGripper/a5.png)
     ![alt text](../../../resources/1-ProductIntroduction/1.4/1.4.1-Gripper/4-FlexibleGripper/a6.png)
  3. 用配套螺丝将柔性夹爪固定在机械臂末端：
     ![alt text](../../../resources/1-ProductIntroduction/1.4/1.4.1-Gripper/4-FlexibleGripper/a7.png)

- 电气连接：

  1. 配发两根连接线，一根用于供电，一根用于控制。

  - 在机械臂底座端，用于供电的线，红色接 24V 接口，黑色接 GND 接口。对于用于控制的线，红色接 OUT1，黑色接 OUT2：
    ![alt text](../../../resources/1-ProductIntroduction/1.4/1.4.1-Gripper/4-FlexibleGripper/a8.png)
  - 气动控制器端，供电线红色接气动控制器 24V，黑色接气动控制器的 GND。控制线红色接 IN1，黑色接 IN2：
    ![alt text](../../../resources/1-ProductIntroduction/1.4/1.4.1-Gripper/4-FlexibleGripper/a9.png)
    > 注意接在“正压”一侧，若供电成功显示屏会亮起。
    > 可以手动测试连接是否正常，将空压机打开，按下气动控制器的按钮，向左（正压）按下则夹爪收缩，向右（负压）则夹爪打开。使用 IO 控制时，确保将上述三档拨动开关设置在中间位置。

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

     elephant_client.set_digital_out(0,0)#复位IO
     time.sleep(2) 
     elephant_client.set_digital_out(1,0)#复位IO
     time.sleep(2)
    
     elephant_client.set_digital_out(0,1)#闭合
     time.sleep(2)
     elephant_client.set_digital_out(1,0)#复位IO
     time.sleep(2)

     elephant_client.set_digital_out(0,0)#复位IO
     time.sleep(2)    
     elephant_client.set_digital_out(1,1)#张开
     time.sleep(2)

     elephant_client.set_digital_out(0,0)#复位IO
     time.sleep(2)
    
     elephant_client.set_digital_out(1,0)#复位IO
     time.sleep(2)
     
 ```


[← 上一页](./3-PneumaticGripper.md) | [下一页 →](../1.4.2-PumpCup/1-ModuleSuctionCup.md)
