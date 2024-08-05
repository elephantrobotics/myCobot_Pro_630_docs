# **Python API使用案例**



## 1 机器人使能控制
确认机器人的IP地址：在机器人终端输入 ifconfig 获取
![](../../resources/1-ProductIntroduction/1.4/poweron/ip.png)

###  1.1 机器人打开使能
```python
from pymycobot import ElephantRobot
import time
if __name__=='__main__':
  
    "连接机器人服务器"
    elephant_client = ElephantRobot("192.168.10.158", 5001)

    "开启TCP通信"
    elephant_client.start_client()

    "先关闭机器人使能"   
    elephant_client.state_off()
    time.sleep(3)

    "给机器人上电"   
    elephant_client.power_on()
    time.sleep(3)

    "给机器人上电"   
    elephant_client.power_on()
    time.sleep(3)
```

### 1.2 机器人关闭使能
```python
from pymycobot import ElephantRobot
import time
if __name__=='__main__':
  
    "连接机器人服务器"
    elephant_client = ElephantRobot("192.168.10.158", 5001)

    "开启TCP通信"
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
  
    "连接机器人服务器"
    elephant_client = ElephantRobot("192.168.10.158", 5001)

    "开启TCP通信"
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
  
    "连接机器人服务器"
    elephant_client = ElephantRobot("192.168.10.158", 5001)

    "开启TCP通信"
    elephant_client.start_client()

    "机器人下电"   
    elephant_client.power_off()
    time.sleep(3)

```

## 2 关节控制
&ensp;&ensp;使用VNC Viewer进入RoboFlow系统后，在快速移动界面下，可通过关节控制，控制机器人到达目标位置后，记录操作面板上显示的机器人6个关节的角度
<div align=center><img src="../../resources/2-serialproduct/myCobot Pro 600/Chinese/p9.png"></div>

确认机器人的IP地址：在机器人终端输入 ifconfig 获取
![](../../resources/1-ProductIntroduction/1.4/poweron/ip.png)

### 2.1 单关节控制
```python
from pymycobot import ElephantRobot

if __name__=='__main__':
    "连接机器人服务器"
    elephant_client = ElephantRobot("192.168.10.158", 5001)

    "开启TCP通信"
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
    "连接机器人服务器"
    elephant_client = ElephantRobot("192.168.10.158", 5001)

    "开启TCP通信"
    elephant_client.start_client()

    "在列表内填入记录下的6个关节角度，最后一个参数为运动速度"
    elephant_client.write_angles([94.828,-143.513,135.283,-82.969,-87.257,-44.033],1000)

    "等待机器人运动到目标位置再执行后续指令"
    elephant_client.command_wait_done()     

```

### 2.3 关节角度获取
```python
from pymycobot import ElephantRobot

if __name__=='__main__':
    "连接机器人服务器"
    elephant_client = ElephantRobot("192.168.10.158", 5001)

    "开启TCP通信"
    elephant_client.start_client()

    "打印机器人当前6个关节角度信息"   
    print(elephant_client.get_angles())

     

```

### 2.4 机器人回零
```python
from pymycobot import ElephantRobot

if __name__=='__main__':
    "连接机器人服务器"
    elephant_client = ElephantRobot("192.168.10.158", 5001)

    "开启TCP通信"
    elephant_client.start_client()

    "在列表内填入6个关节零位角度，最后一个参数为运动速度"
    elephant_client.write_angles([0,-90,0,-90,0,0],1000)

    "等待机器人运动到目标位置再执行后续指令"
    elephant_client.command_wait_done()     

```

