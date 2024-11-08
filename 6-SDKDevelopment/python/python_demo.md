# **Python API使用案例**
使用python API前，需先确认机器人的IP地址：在机器人终端输入 ifconfig 获取
![](../../resources/1-ProductIntroduction/1.4/poweron/ip.png)

## 1 机器人使能控制


###  1.1 机器人打开使能
```python
from pymycobot import ElephantRobot
import time
if __name__=='__main__':
  
    "将ip更改成P600树莓派的实时ip"
    elephant_client = ElephantRobot("192.168.10.158", 5001)

    "启动机器人必要指令"
    elephant_client.start_client()

    "先关闭机器人使能"   
    elephant_client.state_off()
    time.sleep(3)

    "给机器人上电"   
    elephant_client.power_on()
    time.sleep(3)

    "给机器人使能"   
    elephant_client.state_on()
    time.sleep(3)
```

### 1.2 机器人关闭使能
```python
from pymycobot import ElephantRobot
import time
if __name__=='__main__':
  
    "将ip更改成P600树莓派的实时ip"
    elephant_client = ElephantRobot("192.168.10.158", 5001)

    "启动机器人必要指令"
    elephant_client.start_client()

    "关闭机器人使能"   
    elephant_client.state_off()
    time.sleep(3)

```
### 1.3 机器人仅上电
```python
from pymycobot import ElephantRobot
import time
if __name__=='__main__':
  
    "将ip更改成P600树莓派的实时ip"
    elephant_client = ElephantRobot("192.168.10.158", 5001)

    "启动机器人必要指令"
    elephant_client.start_client()

    "机器人上电"   
    elephant_client.power_on()
    time.sleep(3)

```

### 1.4 机器人仅下电
```python
from pymycobot import ElephantRobot
import time
if __name__=='__main__':
  
    "将ip更改成P600树莓派的实时ip"
    elephant_client = ElephantRobot("192.168.10.158", 5001)

    "启动机器人必要指令"
    elephant_client.start_client()

    "机器人下电"   
    elephant_client.power_off()
    time.sleep(3)

```

## 2 关节控制
&ensp;&ensp;使用VNC Viewer进入RoboFlow系统后，在快速移动界面下，可通过关节控制，控制机器人到达目标位置后，记录操作面板上显示的机器人6个关节的角度
<div align=center><img src="../../resources/2-serialproduct/myCobot Pro 600/Chinese/p9.png"></div>



### 2.1 单关节控制
```python
from pymycobot import ElephantRobot

if __name__=='__main__':
    "将ip更改成P600树莓派的实时ip"
    elephant_client = ElephantRobot("192.168.10.158", 5001)

    "启动机器人必要指令"
    elephant_client.start_client()

    "填入要控制的单个关节的角度，第1个参数0为第一轴，以此类推；第2个参数表示关节角度；第三个参数表示运动速度"
    elephant_client.write_angle(0,94.828,1000)

    "等待机器人运动到目标位置再执行后续指令"
    elephant_client.command_wait_done()     

```


### 2.2 多关节控制
```python
from pymycobot import ElephantRobot

if __name__=='__main__':
    "将ip更改成P600树莓派的实时ip"
    elephant_client = ElephantRobot("192.168.10.158", 5001)

    "启动机器人必要指令"
    elephant_client.start_client()

    "在列表内填入记录下的6个关节角度，最后一个参数为运动速度,需更改为自己设定的关节角度"
    elephant_client.write_angles([94.828,-143.513,135.283,-82.969,-87.257,-44.033],1000)

    "等待机器人运动到目标位置再执行后续指令"
    elephant_client.command_wait_done()     

```

### 2.3 关节角度获取
```python
from pymycobot import ElephantRobot

if __name__=='__main__':
    "将ip更改成P600树莓派的实时ip"
    elephant_client = ElephantRobot("192.168.10.158", 5001)

    "启动机器人必要指令"
    elephant_client.start_client()

    "打印机器人当前6个关节角度信息"   
    print(elephant_client.get_angles())

     

```

### 2.4 机器人关节回到零位
```python
from pymycobot import ElephantRobot

if __name__=='__main__':
    "将ip更改成P600树莓派的实时ip"
    elephant_client = ElephantRobot("192.168.10.158", 5001)

    "启动机器人必要指令"
    elephant_client.start_client()

    "在列表内填入6个关节零位角度，最后一个参数为运动速度"
    elephant_client.write_angles([0,-90,0,-90,0,0],1000)

    "等待机器人运动到目标位置再执行后续指令"
    elephant_client.command_wait_done()     

```

## 3 坐标控制
&ensp;&ensp;主要用于实现智能规划路线让机械臂从一个位置到另一个指定位置。分为[x,y,z,rx,ry,rz]，其中[x,y,z]表示的是机械臂末端在空间中的位置（该坐标系为直角坐标系），[rx,ry,rz]表示的是机械臂末端在该点的姿态(该坐标系为欧拉坐标)
&ensp;&ensp;使用VNC Viewer进入RoboFlow系统后，在快速移动界面下，可通过笛卡尔坐标控制，控制机器人到达目标位置后，记录操作面板上显示的机器人6个坐标值
<div align=center><img src="../../resources/2-serialproduct/myCobot Pro 600/Chinese/p10.png"></div>

使用坐标控制需要先用关节运动将机械臂调整至下图姿态，避免奇异点导致机械臂无法执行动作
![](../../resources/14-IssueFAQ/move.png)

### 3.1 单参数坐标控制
```python
from pymycobot import ElephantRobot

if __name__=='__main__':
    "将ip更改成P600树莓派的实时ip"
    elephant_client = ElephantRobot("192.168.10.158", 5001)

    "启动机器人必要指令"
    elephant_client.start_client()

    "填入参数，第1个参数的2代表Z轴方向，以此类推；第2个参数表示关坐标值；第三个参数表示运动速度"
    elephant_client.write_coord(2,94.828,3000)

    "等待机器人运动到目标位置再执行后续指令"
    elephant_client.command_wait_done()     

```

### 3.2 多参数坐标控制

```python
from pymycobot import ElephantRobot

if __name__=='__main__':
    "将ip更改成P600树莓派的实时ip"
    elephant_client = ElephantRobot("192.168.10.158", 5001)

    "启动机器人必要指令"
    elephant_client.start_client()

    "在列表内填入记录下的6个坐标值，最后一个参数为运动速度,,需更改为自己设定的位姿"
    elephant_client.write_coords([-130.824,256.262,321.533,176.891,-0.774,-128.700], 3000)

    "等待机器人运动到目标位置再执行后续指令"
    elephant_client.command_wait_done()     

```

### 3.3 笛卡尔坐标获取
```python
from pymycobot import ElephantRobot

if __name__=='__main__':
    "将ip更改成P600树莓派的实时ip"
    elephant_client = ElephantRobot("192.168.10.158", 5001)

    "启动机器人必要指令"
    elephant_client.start_client()

    "打印输出机器人当前笛卡尔空间坐标信息"
    elephant_client.get_coords()

         

```
## 4**IO控制**

### 4.1 **设置IO引脚输出状态**
```python
from pymycobot import ElephantRobot

if __name__=='__main__':
    "将ip更改成P600树莓派的实时ip"
    elephant_client = ElephantRobot("192.168.10.158", 5001)

    "启动机器人必要指令"
    elephant_client.start_client()

    "引脚序号0 ~ 5对应底座电气接口OUT 1 ~ 6 ; 16 ~ 17 对应机械臂末端电气接口 OUT 1 ~ 2"
    "控制机器人OUT1输出为高电平"
    elephant_client.set_digital_out(0,1)

    "机器人延时3秒后再执行后面程序"
    elephant_client.wait(3)

    "控制机器人OUT1输出为低电平"
    elephant_client.set_digital_out(0,0)

    "机器人延时3秒后再执行后面程序"
    elephant_client.wait(3)    

```
### 4.2 **获取IO引脚输出状态**
```python
from pymycobot import ElephantRobot

if __name__=='__main__':
    "将ip更改成P600树莓派的实时ip"
    elephant_client = ElephantRobot("192.168.10.158", 5001)

    "启动机器人必要指令"
    elephant_client.start_client()
    
    "引脚序号0 ~ 5对应底座电气接口OUT 1 ~ 6 ; 16 ~ 17 对应机械臂末端电气接口 OUT 1 ~ 2"
    "获取机器人OUT1输出状态"
    elephant_client.get_digital_out(0)

    "机器人延时0.5秒后再执行后面程序"
    elephant_client.wait(0.5)  

```
### 4.3 **获取IO引脚输入状态**
```python
from pymycobot import ElephantRobot

if __name__=='__main__':
    "将ip更改成P600树莓派的实时ip"
    elephant_client = ElephantRobot("192.168.10.158", 5001)

    "启动机器人必要指令"
    elephant_client.start_client()
    
    "引脚序号0 ~ 5对应底座电气接口OUT 1 ~ 6 ; 16 ~ 17 对应机械臂末端电气接口 OUT 1 ~ 2"
    "获取机器人IN1输入状态,低电平有效,即GND与输入端导通时反馈1，其余状态反馈0"
    elephant_client.get_digital_in(0)

    "机器人延时0.5秒后再执行后面程序"
    elephant_client.wait(0.5)  

```

## 5 自适应夹爪控制

```python
from pymycobot import ElephantRobot
import time
if __name__=='__main__':
    "将ip更改成P600树莓派的实时ip"
    elephant_client = ElephantRobot("192.168.10.158", 5001)

    "启动机器人必要指令"
    elephant_client.start_client()
    time.sleep(1)

    "夹爪设置透传模式"
    elephant_client.set_gripper_mode(0)
    time.sleep(1)

    "夹爪完全张开"
    elephant_client.set_gripper_state(0,100)
    time.sleep(2)

    "夹爪完全闭合"
    elephant_client.set_gripper_state(1,100)
    time.sleep(2)

    "夹爪张开到指定行程，这里张开到夹爪行程的一半"
    elephant_client.set_gripper_value(50,100)
    time.sleep(2)
```
## 6 相对运动

```python
from pymycobot import ElephantRobot
import time
if __name__=='__main__':
    "将ip更改成P600树莓派的实时ip"
    elephant_client = ElephantRobot("192.168.10.158", 5001)
    
    "启动机器人必要指令"
    elephant_client.start_client()
    time.sleep(1)
    
    "机器人以当前坐标位置往Z方向正方向整体运动50mm"
    elephant_client.jog_relative("Z",50,1500,1)
    
    "等待机器人运动到目标位置再执行后续指令"
    elephant_client.command_wait_done() 
    
    "机器人以当前J6关节角度增加10度"
    elephant_client.jog_relative("J6",10,1500,0)
    
    "等待机器人运动到目标位置再执行后续指令"
    elephant_client.command_wait_done()  

```

## 7 机器人夹爪搬运木块案例
```python
from pymycobot import ElephantRobot
import time
if __name__=='__main__':
    "将ip更改成P600树莓派的实时ip"
    elephant_client = ElephantRobot("192.168.137.182", 5001)

    "启动机器人必要指令"
    elephant_client.start_client()  
    time.sleep(1) 

    "夹爪设置透传模式"
    elephant_client.set_gripper_mode(0)
    time.sleep(1) 

    "夹爪完全张开"
    elephant_client.set_gripper_state(1,100)
    time.sleep(1)

    for i in range (1):
        "机器人关节运动到安全点,需更改为自己设定的关节角度"
        elephant_client.write_angles([94.828,-143.513,135.283,-82.969,-87.257,-44.033],1000)
        "等待机器人运动到目标位置再执行后续指令"
        elephant_client.command_wait_done()
        
        "机器人笛卡尔运动到码垛抓取过渡点,需更改为自己设定的位姿"
        elephant_client.write_coords([-130.824,256.262,321.533,176.891,-0.774,-128.700], 3000)
        elephant_client.command_wait_done()

        "机器人以当前坐标位置往Z轴负方向整体运动100mm,到达木块抓取位置"
        elephant_client.jog_relative("Z",-100,1500,1)
        elephant_client.command_wait_done()
        
        "控制夹爪闭合到30mm"
        elephant_client.set_gripper_value(30,100)
        "控制机器人等待1秒后再动作"
        elephant_client.wait(1)

        "机器人以当前坐标位置往Z轴正方向整体运动100mm,到达木块抓取过渡点"
        elephant_client.jog_relative("Z",100,1500,1)
        elephant_client.command_wait_done()

        "机器人以当前坐标位置往Y轴正方向整体运动300mm,到达木块放置过渡点"
        elephant_client.jog_relative("Y",300,1500,1)
        elephant_client.command_wait_done()

        "机器人以当前坐标位置往Z轴负方向整体运动100mm,到达木块放置位置"
        elephant_client.jog_relative("Z",-100,1500,1)
        elephant_client.command_wait_done()
        
        "控制夹爪完全张开"
        elephant_client.set_gripper_value(100,100)
        "控制机器人等待1秒后再动作"
        elephant_client.wait(1)

        "机器人以当前坐标位置往Z轴正方向整体运动100mm,到达木块放置过渡点"
        elephant_client.jog_relative("Z",100,1500,1)
        elephant_client.command_wait_done()

        "机器人关节运动到安全点"
        elephant_client.write_angles([94.828,-143.513,135.283,-82.969,-87.257,-44.033],1000)
        elephant_client.command_wait_done()

```

---
[← 上一页](./python_demo.md) | [下一页 → ](../../11-ApplicationBaseROS/11.1-ROS1/README.md)
