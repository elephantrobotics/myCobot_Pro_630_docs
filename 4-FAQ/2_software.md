# 软件问题

**Q：如何查看机械臂的IP地址、连接VNC？**
WIFI连接:                         
连接wifi后，将鼠标放置到wifi图标上

![](../resources/3-UserNotes/FAQ/img/sofware_1.png)

或者点击右上角图标（如图所示）后2所指向的位置查看

![](../resources/3-UserNotes/FAQ/img/sofware_2.png)

**Q: 有p600将笛卡尔坐标系换算成六自由度的角度坐标的公式吗**

- A： 没有，但是可以用send_coords移动到目标位置，然后读当前关节角度

**Q:使用程序控制机械臂时，无法读取机械臂角度或坐标，执行第一个运动指令后无法继续控制机械臂运动怎么办？**

- A: 可能是由于编写程序控制机械臂时没有添加延时或等待完成指令。使用python控制时可添加command_wait_done()，使机械臂完成上一步运动再往下执行

![](../resources/3-UserNotes/FAQ/img/sofware_3.png)

使用RoboFlow时，可以添加延时确保机械臂完成运动后再执行下一步命令：

![](../resources/3-UserNotes/FAQ/img/sofware_4.png)

**机械臂运动后，command_wait_done()返回-1是为什么？**

- A: 是由于机械臂运动的时间过长，若运行时间超过1分钟，command_wait_done()则会返回-1

**解决方法**：替换RoboFlow版本为：630的roboflow最新版本和更新教程：

A：关闭roboflow，然后使用U盘将文件复制到树莓派上，并按照视频进行操作
视频：
https://drive.google.com/file/d/1KD1VxhzFYXEFF-3paO-ntMfGQMvjjLc2/view?usp=sharing
文件：
https://drive.google.com/file/d/1lV2fTM-rNeZbccjJInpbKVhSzSXJGf4c/view?usp=sharing

**启动机械臂报错是为什么？**

![](../resources/3-UserNotes/FAQ/img/sofware_5.png)

![](../resources/3-UserNotes/FAQ/img/sofware_6.png)

若出现以上报错：
1. 检查急停是否处于释放状态，若没有，需要将急停旋钮往顺时针拧，使其弹起。
2. 若急停处于释放状态，检查急停与机械臂的连接是否松动，可将连接按紧。

![](../resources/3-UserNotes/FAQ/img/sofware_7.png)

若出现以上报错：
检查系统提示的关节是否到达限位，需要断电将关节调整至零位。
如果是456关节超限，请按下急停开关，将456关节移动回到正常姿态后再启动机器人
如果是123关节超限，可按照下面的步骤将超限的关节姿态调整回来:

① 在roboflow中进入配置中心，在初始化栏点击仅上电
② 点击开始编程，进入配置栏，选择安全配置，依次打开 1，2，3 关节的刹车（如仅某一关节超限，打开对应的超限关节即可，不必123刹车全打开）。
③ 打开刹车后关节是可手动移动的，请手动调整关节到正常姿态，调整结束之后再关闭刹车
④ 在roboflow重启机器人即可，后续注意关节姿态不要超限

![](../resources/3-UserNotes/FAQ/img/sofware_8.png)

![](../resources/3-UserNotes/FAQ/img/sofware_9.png)

![](../resources/3-UserNotes/FAQ/img/sofware_10.png)


若出现以上报错：
关闭Roboflow，打开命令行输入elerob -l

![](../resources/3-UserNotes/FAQ/img/sofware_11.png)

再次启动RoboFlow可解决问题

**Q:600两个关节同时运动后的时候，出现运动速度很快的情况，怎么处理？**

A:关于你提到的这个关节1在0和0.0001的情况下，J4运动速度不一致问题请参考下面的解释
首先这个现象是正常的
你设定的这两组角度值中，J1的变化非常小，而J4的运动范围相对较大，当这组指令下发的时候，机械臂内部电机有一个同步执行机制，这意味着两个点位之间，J1前后运动的时间和J4关节前后运动的时间相同，由于J1的关节角度变化过小，运行时间自然也相对较短，这就导致了同步执行的情况下，J4关节需要在同样相对较短的运动时间内完成角度相对较大变化，这就导致了J4的速度较快的结果
为了如果你想将机器的运行速度调节到比较慢的状态，那么我们建议你在仅需要控制一个关节的情况下，使用控制单个关节的API: write_angle
如果你想控制多个关节同时运动的，请注意使用write_angles尽量让不同关节之间的角度差值缩小一点，像J1的0变化到0.00001，差值为0，而J4关节的-150到，-100差值为40，这个相差实在太大了，如果你将J1的变化更改成0到100，这个运动速度基本是正常的，不会太快，你可以测试看看


**Q：630的roboflow最新版本和更新教程：**

- A：关闭roboflow，然后使用U盘将文件复制到树莓派上，并按照视频进行操作
视频：
https://drive.google.com/file/d/1N_lDCe4H-Oyy0yGGVttszHlmmVVN-K94/view?usp=sharing
文件（2024.10.10）：
https://drive.google.com/file/d/1h6UIe9G9Mum_dutInfaqH_oVjJHSrqn6/view?usp=sharing


**Q：P600在按下急停之后，无法继续使用python进行控制，这个如何处理？**

- A：正常情况下在按下急停仍然可使用python进行控制，无法控制的原因为没有使用power_off()给P600彻底断电,在启动机器人前添加power_off()即可

**Q：600运行超限后机械臂报错无法继续移动的情况下如何处理？**

- A:如果是456关节超限，请按下急停开关，将456关节移动回到正常姿态后再启动机器人
如果是123关节超限，可按照下面的步骤将超限的关节姿态调整回来

①在roboflow中进入配置中心，在初始化栏点击仅上电

②点击开始编程，进入配置栏，选择安全配置，依次打开 1，2，3 关节的刹车（如仅某一关节超限，打开对应的超限关节即可，不必123刹车全打开）。

③打开刹车后关节是可手动移动的，请手动调整关节到正常姿态，调整结束之后再关闭刹车

④在roboflow重启机器人即可，后续注意关节姿态不要超限

![](../resources/3-UserNotes/FAQ/img/sofware_8.png)


**Q：630是否带碰撞检测功能，如果带，那么碰撞检测阈值是否可以调整？**

- A：我们的机器有碰撞检测设计，在收到较大碰撞时机器会自动停止运动，如果你希望可以检测到比较小的力也产生碰撞检测，你可以尝试调整下面的碰撞检测参数，建议单次调整幅度为0.01

![](../resources/3-UserNotes/FAQ/img/sofware_12.png)


**Q：630&600的坐标控制无法使用如何解决wait_command_done:-1？**

检查机械臂是否姿态为下图这种

![](../resources/3-UserNotes/FAQ/img/sofware_13.png)

然后使用get_angles和get_coords这两个api获取坐标和角度

![](../resources/3-UserNotes/FAQ/img/sofware_14.png)

在获取坐标和角度后修改write_angles和write_coords的角度和坐标

![](../resources/3-UserNotes/FAQ/img/sofware_15.png)


```python
from pymycobot import ElephantRobot
import time

# 这个代码没上电，你要确保你已经上电。
if __name__=='__main__':

#    "将ip更改成P600树莓派的实时ip"
    elephant_client = ElephantRobot("192.168.1.153", 5001,debug=True)

    elephant_client.start_client()

    print(elephant_client.get_angles())
    time.sleep(1)
    print(elephant_client.get_coords())
    time.sleep(1)

    elephant_client.write_angles([0.0, -144.884, 138.455, -89.648, -89.824, 0.0], 1000)
    elephant_client.command_wait_done()



    elephant_client.write_coords([80.014, 156.939, 316.656, 174.274, -0.0, 110.002], 3000)
    elephant_client.command_wait_done()

```

**Q：什么的是正向运动学和逆向运动学？**

- A：正向运动学（Forward Kinematics）是指已知机器人各个关节的角度（或位移），求解机器人末端执行器（如机械臂的手爪）在笛卡尔空间中的位置和姿态。get_coords()的API中实现了，但是具体的算法不公开。
逆运动学（Inverse Kinematics）与正向运动学相反，它是指已知机器人末端执行器在笛卡尔空间中的位置和姿态，求解机器人各个关节的角度（或位移）write_coords()、send_coords()
