# Phoenix API使用案例

**注意事项**：Phoenix API只能运行在机械臂的主控上，不能运行在客户的电脑上，而且如果要使用Phoenix API，需要手动将Roboflow关闭，否则会报错

## 1 机器人使能控制
```Python
from pymycobot.mycobotpro630 import *
import time
p = Phoenix()
#检查机器人是否使能，如果没有，则给机器人使能
while p.state_check()==False:
    p.start_robot()#机器人上电且使能
    time.sleep(0.02)
time.sleep(2)
p._state_off()#机器人关闭使能
p._power_off()#机器人下电

```
## 2 机器人关节角度获取和控制
```Python
from pymycobot.mycobotpro630 import *
import time
p = Phoenix()
#检查机器人是否使能，如果没有，则给机器人使能
while p.state_check()==False:
    p.start_robot()
    time.sleep(0.02)

#获取机器人关节角度
print("angles=",p.get_angles())

#等待机器人运动指令执行后，再执行后续指令
def wait_done():
    while p.is_in_commanded_position()==False:
        time.sleep(0.1)
        

p.set_angles([0,-90,0,-90,0,0],20)#关节运动到指定关节角度
wait_done()#等待运动指令完成
p.set_angles([00,-90,0,0,0,0],20)#关节运动到指定关节角度
wait_done()#等待运动指令完成

```

## 3 机器人坐标位姿获取和控制
```Python
from pymycobot.mycobotpro630 import *
import time
p = Phoenix()
#检查机器人是否使能，如果没有，则给机器人使能
while p.state_check()==False:
    p.start_robot()
    time.sleep(0.02)

#获取机器人坐标位姿
print("coords=",p.get_coords())

#等待机器人运动指令执行后，再执行后续指令
def wait_done():
    while p.is_in_commanded_position()==False:
        time.sleep(0.1)

p.set_angles([0,-90,90,-91,-90,0],20)#关节运动至初始姿态
wait_done()#等待运动指令完成
p.set_coords([369.002, 46.685, 321.705, 175.578, 0.01, 83.526],20)#坐标运动至指定位姿
wait_done()#等待运动指令完成
p.set_coords([369.002, 46.685, 421.705, 175.578, 0.01, 83.526],20)#坐标运动至指定位姿
wait_done()#等待运动指令完成   
```

## 4 机器人IO获取和控制
```Python
from pymycobot.mycobotpro630 import *
import time
p = Phoenix()
#检查机器人是否使能，如果没有，则给机器人使能
while p.state_check()==False:
    p.start_robot()
    time.sleep(0.02)

#DI.PIN_0 ~ DI.PIN_5对应机器人IN1~IN6输入,若是返回1代表有输入，返回0代表无输入
print("IN1=",p.get_digital_in(DI.PIN_0))

#DO.PIN_0 ~ DO.PIN_5对应机器人OUT1~OUT6输出
p.set_digital_out(DO.PIN_0,1)#OUT1打开输出 
time.sleep(2) 
p.set_digital_out(DO.PIN_0,0)#OUT1关闭输出

```

## 5 自适应夹爪控制
```Python
from pymycobot.mycobotpro630 import *
from pymycobot import ElephantRobot
ElephantRobot.set_gripper_state()
import time
p = Phoenix()
#检查机器人是否使能，如果没有，则给机器人使能
while p.state_check()==False:
    p.start_robot()
    time.sleep(0.02)

p.tool_set_gripper_mode(0)#设置夹爪为透传模式
p.tool_set_gripper_value(0,100)#设置夹爪完全关闭
time.sleep(1)
p.tool_set_gripper_value(100,100)#设置夹爪完全关闭
time.sleep(1)

```