# **基于Python API开发**
&ensp;&ensp;大象提供了Python API来远程控制机器人，我们使用TCP协议来在客户端和机器人之间进行通信，因此在使用我们的API之前，您需要按照文档操作以下内容。

## **1 环境搭建**
### 1.1 安装Python

> **注意：**安装之前，请先确认您的电脑是64位还是32位。右键点击`我的电脑`，选择`属性`。如下图显示是64位的操作系统，所以选择64位的Python安装包。
>
> <img src="../../resources/7-ApplicationBasePython/电脑位数1.jpg" style="zoom: 67%;" />
>
> <img src="../../resources/7-ApplicationBasePython/电脑位数2.jpg" style="zoom: 67%;" />



* **Python官方下载地址： https://www.python.org/downloads/**

* **点击`Downloads`选项，开始下载Python，点击`Add Python 3.10 to PATH`,点击`Install Now`，开始安装Python**

<img src="../../resources/7-ApplicationBasePython/pythondownload1.jpg" style="zoom: 33%;" />

<img src="../../resources/7-ApplicationBasePython/pythondownload2.jpg" style="zoom: 50%;" />

<img src="../../resources/7-ApplicationBasePython/pythondownload3.jpg" style="zoom: 50%;" />



* **出现“Setup was successful”提示，说明安装完成**

<img src="../../resources/7-ApplicationBasePython/pythondownload4.jpg" style="zoom: 50%;" />



### 1.2 运行Python
安装成功后，打开命令提示符窗口（Win+R，输入cmd回车），敲入`python`后，会出现两种情况。

**情况一：**

<img src="../../resources/7-ApplicationBasePython/运行python1.jpg" style="zoom: 50%;" />

出现图片中的提示表示Python安装成功。

出现提示符`>>>` 就表示我们已经在Python交互式环境中了，可以输入任何Python代码，回车后会立刻得到执行结果。

**情况二：** 

假如输入错误（比如输入pythonn），则会出现错误提示：

<img src="../../resources/7-ApplicationBasePython/运行python2.jpg" style="zoom: 50%;" />

>  **注意：**出现错误的信息一般都是没有配置环境变量导致的，可以参考**1.3 配置环境变量**修改环境变量。



### 1.3 配置环境变量
由于Windows会根据一个Path的环境变量设定的路径去查找python.exe，如果没找到，就会报错。因此，如果安装时漏掉了勾选`Add Python 3.10 to PATH`，则需要手动把python.exe所在的路径添加到Path中，或者重新安装一遍Python，记得勾选上`Add Python 3.10 to PATH`选项即可。

以下是手动添加python.exe所在的路径步骤。

* 右键我的电脑–>选择属性–>选择高级系统设置–>选择右下角的环境变量：

<img src="../../resources/7-ApplicationBasePython/环境变量.jpg" style="zoom: 50%;" />



* 环境变量主要有包括用户变量和系统变量，需要设置的环境变量就在这两个变量中。如下图所示：

<img src="../../resources/7-ApplicationBasePython/系统变量+用户变量.jpg" style="zoom: 50%;" />



* 用户变量是将自己的下载的程序可以在cmd命令中使用。把程序的绝对路径写到用户变量中即可使用，如下图所示：

<img src="../../resources/7-ApplicationBasePython/绝对路径.jpg" style="zoom: 50%;" />



<img src="../../resources/7-ApplicationBasePython/添加path.jpg" style="zoom: 50%;" />



* 以上步骤完成后，打开命令提示符窗口（Win+R，再输入cmd，回车），敲入Python，出现下图中的提示表示成功：

<img src="../../resources/7-ApplicationBasePython/路径添加成功.jpg" style="zoom: 50%;" />

### 1.4 pymycobot安装
* pymycobot安装。打开一个控制台终端(快捷键Win+R,输入cmd进入终端)，输入以下命令后按键盘回车键进行安装：

```python
pip install pymycobot --upgrade --user
```

<img src="../../resources/7-ApplicationBasePython/pymycobot安装.jpg" style="zoom: 67%;" />


## 2 **开启TCP服务器功能**


### **2.1登录RoboFlow操作系统**

&ensp;&ensp;机器人上电开机后，使用VNC Viewer进入树莓派，登录RoboFlow操作系统
<div align=center><img src="../../resources/2-serialproduct/myCobot Pro 600/Chinese/p0.png"></div>

### **2.2启动机器人**
&ensp;&ensp;进入配置中心，点击启动机器人按钮
<div align=center><img src="../../resources/2-serialproduct/myCobot Pro 600/Chinese/p1.png"></div>
<br>
<div align=center><img src="../../resources/2-serialproduct/myCobot Pro 600/Chinese/p2.png"></div>
<br>
<div align=center><img src="../../resources/2-serialproduct/myCobot Pro 600/Chinese/p3.png"></div>

### **2.3检查TCP服务器是否开启**
&ensp;&ensp;返回主菜单，点击编写程序后，再点击空白程序，进入程序编辑界面后，点击配置按钮，点击网络/串口选项,检查TCP服务器是否开启，通常情况下，**TCP服务器是默认开启的**，若未开启，则需手动开启

<div align=center><img src="../../resources/2-serialproduct/myCobot Pro 600/Chinese/p4.png"></div>
<br>
<div align=center><img src="../../resources/2-serialproduct/myCobot Pro 600/Chinese/p5.png"></div>
<br>
<div align=center><img src="../../resources/2-serialproduct/myCobot Pro 600/Chinese/p6.png"></div>
<br>
<div align=center><img src="../../resources/2-serialproduct/myCobot Pro 600/Chinese/p7.png"></div>

## 3 **Python API接口说明**
### 3.1 ElephantRobot类实列化
```
"从pymycobot库导入ElephantRobot类"
from pymycobot import ElephantRobot

"连接机器人服务器"
elephant_client = ElephantRobot("192.168.137.182", 5001)

"开始TCP通信"
elephant_client.start_client()
```
**使用Python API必须先将ElephantRobot类实例后才可调用mycobot pro600的功能函数**
- **必填参数**：
&ensp;&ensp;  **参数1**：机器人实际IP地址
&ensp;&ensp;  **参数2**：机器人端口（**API函数端口固定为5001**）
### 3.2功能函数介绍
**def start_client()**:
- **功能**：开启TCP连接（**若要使用Python API控制机器人，必须调用此API**）
- **参数**：无
  
**def stop_client()**:
- **功能**：关闭TCP连接
- **参数**：无

**def send_command(command)**:
- **功能**：发送指令给服务器
- **参数**：指令(字符串类型)

**def string_to_coords(data)**:
- **功能**：字符串类型数据转列表类型数据
- **参数**：字符串类型数据

**def string_to_double(data)**:
- **功能**：字符串类型数据转双精度浮点型数据
- **参数**：字符串类型数据

**def string_to_int(data)**:
- **功能**：字符串类型数据转整型数据
- **参数**：字符串类型数据
  
**def invalid_coords()**:
- **功能**：给服务器返回一个无效的笛卡尔坐标
- **参数**：无

**def get_angles()**:
- **功能**：向服务器请求当前各个关节角度信息
- **参数**：无

**def get_coords()**:
- **功能**：向服务器请求当前笛卡尔位姿信息
- **参数**：无
  
**def get_speed()**:
- **功能**：向服务器请求机器人运动速率
- **参数**：无

**def power_on()**:
- **功能**：机器人上电
- **参数**：无

**def power_off()**:
- **功能**：机器人下电
- **参数**：无

**def check_running()**:
- **功能**：检查机器人是否在运行
- **参数**：无

**def state_check()**:
- **功能**：获取机器人状态
- **参数**：无

**def read_next_error(data)**:
- **功能**：机器人错误检测
- **参数**：无
  
**def write_coords(coords,speed)**:
- **功能**：发送整体坐标和姿态,让机械臂头部从原来点移动到指定点
- **参数**：机器人笛卡尔位姿（列表类型），机械臂运动的速度

**def write_coord(axis, value, speed)**:
- **功能**：发送单个坐标值给机械臂进行移动
- **参数**：机器人笛卡尔位置[0代表x,1代表y,2代表z,3代表rx,4代表ry,5代表rz]，要到达的坐标值，机械臂运动的速度

**def write_angles(angles,speed)**:
- **功能**：发送所有角度给机械臂所有关节
- **参数**：关节角度(列表类型)，机械臂运动的速度
  
**def write_angle(joint, value, speed)**:
- **功能**：发送指定的单个关节运动至指定的角度
- **参数**：指定关节[0代表j1,1代表j2,2代表j3,3代表j4,4代表j5,5代表j6],关节角度,机械臂运动的速度

**def set_speed(percentage)**:
- **功能**：设置速度
- **参数**：目标速度

**def set_carte_torque_limit(axis_str, value)**:
- **功能**：设置机器人的扭矩限制
- **参数**：x/y/z/rx /ry/rz,扭矩
  
**def set_payload(payload)**:
- **功能**：设置机器人的有效负载
- **参数**：范围 0.0 ~ 2.0

**def state_on()**:
- **功能**：启动系统
- **参数**：无

**def state_off()**:
- **功能**：关闭系统
- **参数**：无

**def task_stop()**:
- **功能**：任务暂停
- **参数**：无

**def jog_angle(joint_str, direction, speed)**:
- **功能**： 控制机器人按照指定的角度持续移动
- **参数**：机械臂的关节[J1/J2/J3/J4/J5/J6]，主要控制机器臂移动的方向[-1=负方向 ，0=停止，1=正方向]，机器人运动的速度

**def jog_coord(axis_str, direction, speed)**:
- **功能**： 控制机器人按照指定的坐标轴方向持续移动
- **参数**：笛卡尔的方向[x/y/z/rx/ry/rz],主要控制机器臂移动的方向[-1=负方向 ，0=停止，1=正方向],机器人运动的速度
  
**def get_digital_in(pin_number)**:
- **功能**：获取输入引脚信号
- **参数**：引脚序号

**def get_digital_out(pin_number)**:
- **功能**：获取输出引脚信号
- **参数**：引脚序号

**def set_digital_out(pin_number, pin_signal)**:
- **功能**：设置输出引脚信号
- **参数**：引脚序号，引脚状态[0=低电平，1=高电平]
  
**def get_acceleration()**:
- **功能**：获取机器人的加速度
- **参数**：无

**def set_acceleration(acceleration)**:
- **功能**：设置机器人的加速度
- **参数**：加速度

**def command_wait_done()**:
- **功能**：等待到上一个运动命令完成为止(**此API函数必须添加到所有运动API函数后面**)
- **参数**：无

**def wait(seconds)**:
- **功能**：等待时长(以秒为单位)
- **参数**：无
  
**def assign_variable(var_name, var_value)**:
- **功能**：给定义好的变量赋值
- **参数**：变量名（字符串类型）,目标值

**def get_variable(var_name)**:
- **功能**：获取一个变量的值
- **参数**：变量名（字符串类型）

<!-- ## 4 **Python API使用案例**
### 4.1 **关节控制**
&ensp;&ensp;使用VNC Viewer进入RoboFlow系统后，在快速移动界面下，可通过关节控制，控制机器人到达目标位置后，记录操作面板上显示的机器人6个关节的角度
<div align=center><img src="../../resources/2-serialproduct/myCobot Pro 600/Chinese/p9.png"></div>

#### 4.1.1 **多关节控制**
```
from pymycobot import ElephantRobot

if __name__=='__main__':
    "连接机器人服务器"
    elephant_client = ElephantRobot("192.168.137.182", 5001)

    "开启TCP通信"
    elephant_client.start_client()

    "在列表内填入记录下的6个关节角度，最后一个参数为运动速度"
    elephant_client.write_angles([94.828,-143.513,135.283,-82.969,-87.257,-44.033],1000)

    "等待机器人运动到目标位置再执行后续指令"
    elephant_client.command_wait_done()     

```
#### 4.1.2 **单关节控制**
```
from pymycobot import ElephantRobot

if __name__=='__main__':
    "连接机器人服务器"
    elephant_client = ElephantRobot("192.168.137.182", 5001)

    "开启TCP通信"
    elephant_client.start_client()

    "填入要控制的单个关节的角度，第1个参数0为第一轴，以此类推；第2个参数表示关节角度；第三个参数表示运动速度"
    elephant_client.write_angle(0,94.828,1000)

    "等待机器人运动到目标位置再执行后续指令"
    elephant_client.command_wait_done()     

```
#### 4.1.3 **关节角度获取**
```
from pymycobot import ElephantRobot

if __name__=='__main__':
    "连接机器人服务器"
    elephant_client = ElephantRobot("192.168.137.182", 5001)

    "开启TCP通信"
    elephant_client.start_client()

    "打印机器人当前6个关节角度信息"   
    elephant_client.get_angles()

    "等待机器人运动到目标位置再执行后续指令"
    elephant_client.command_wait_done()     

```

### 4.2 **坐标控制**
&ensp;&ensp;主要用于实现智能规划路线让机械臂从一个位置到另一个指定位置。分为[x,y,z,rx,ry,rz]，其中[x,y,z]表示的是机械臂头部在空间中的位置（该坐标系为直角坐标系），[rx,ry,rz]表示的是机械臂头部在该点的姿态(该坐标系为欧拉坐标)<br/>
&ensp;&ensp;使用VNC Viewer进入RoboFlow系统后，在快速移动界面下，可通过笛卡尔坐标控制，控制机器人到达目标位置后，记录操作面板上显示的机器人6个坐标值
<div align=center><img src="../../resources/2-serialproduct/myCobot Pro 600/Chinese/p10.png"></div>

#### 4.2.1 **多参数坐标控制**
```
from pymycobot import ElephantRobot

if __name__=='__main__':
    "连接机器人服务器"
    elephant_client = ElephantRobot("192.168.137.182", 5001)

    "开启TCP通信"
    elephant_client.start_client()

    "在列表内填入记录下的6个坐标值，最后一个参数为运动速度"
    elephant_client.write_coords([-130.824,256.262,321.533,176.891,-0.774,-128.700], 3000)

    "等待机器人运动到目标位置再执行后续指令"
    elephant_client.command_wait_done()     

```
#### 4.2.2 **单参数坐标控制**
```
from pymycobot import ElephantRobot

if __name__=='__main__':
    "连接机器人服务器"
    elephant_client = ElephantRobot("192.168.137.182", 5001)

    "开启TCP通信"
    elephant_client.start_client()

    "填入参数，第1个参数的2代表Z轴方向，以此类推；第2个参数表示关坐标值；第三个参数表示运动速度"
    elephant_client.write_coord(2,94.828,3000)

    "等待机器人运动到目标位置再执行后续指令"
    elephant_client.command_wait_done()     

```
#### 4.2.3 **笛卡尔空间坐标获取**
```
from pymycobot import ElephantRobot

if __name__=='__main__':
    "连接机器人服务器"
    elephant_client = ElephantRobot("192.168.137.182", 5001)

    "开启TCP通信"
    elephant_client.start_client()

    "打印输出机器人当前笛卡尔空间坐标信息"
    elephant_client.get_coords()

    "等待机器人运动到目标位置再执行后续指令"
    elephant_client.command_wait_done()     

```
### 4.3 **IO控制**

#### 4.3.1 **设置IO引脚输出状态**
```
from pymycobot import ElephantRobot

if __name__=='__main__':
    "连接机器人服务器"
    elephant_client = ElephantRobot("192.168.137.182", 5001)

    "开启TCP通信"
    elephant_client.start_client()

    "控制机器人OUT1输出为高电平"
    elephant_client.set_digital_out(0,1)

    "机器人延时3秒后再执行后面程序"
    elephant_client.wait(3)

    "控制机器人OUT1输出为低电平"
    elephant_client.set_digital_out(0,0)

    "机器人延时3秒后再执行后面程序"
    elephant_client.wait(3)    

```
#### 4.3.1 **获取IO引脚输出状态**
```
from pymycobot import ElephantRobot

if __name__=='__main__':
    "连接机器人服务器"
    elephant_client = ElephantRobot("192.168.137.182", 5001)

    "开启TCP通信"
    elephant_client.start_client()

    "获取机器人OUT1输出状态"
    elephant_client.get_digital_out(0)

    "机器人延时0.5秒后再执行后面程序"
    elephant_client.wait(0.5)  

```
#### 4.3.1 **获取IO引脚输入状态**
```
from pymycobot import ElephantRobot

if __name__=='__main__':
    "连接机器人服务器"
    elephant_client = ElephantRobot("192.168.137.182", 5001)

    "开启TCP通信"
    elephant_client.start_client()

    "获取机器人IN1输入状态"
    elephant_client.get_digital_in(0)

    "机器人延时0.5秒后再执行后面程序"
    elephant_client.wait(0.5)  

```
## 5 **Python API应用场景案例**
### 5.1 **搬运码垛**
```
from pymycobot import ElephantRobot

if __name__=='__main__':
    "连接机器人服务器"
    elephant_client = ElephantRobot("192.168.137.182", 5001)
    "开启TCP通信"
    elephant_client.start_client()     
    for i in range (1):
        "机器人关节运动到安全点"
        elephant_client.write_angles([94.828,-143.513,135.283,-82.969,-87.257,-44.033],1000)
        "等待机器人运动到目标位置再执行后续指令"
        elephant_client.command_wait_done()
        
        "机器人笛卡尔运动到码垛抓取过渡点"
        elephant_client.write_coords([-130.824,256.262,321.533,176.891,-0.774,-128.700], 3000)
        elephant_client.command_wait_done()

        "控制机器人朝Z轴方向笛卡尔运动到码垛抓取点"
        elephant_client.write_coord(2,241.533,3000)
        elephant_client.command_wait_done()
        
        "控制机器人OUT1输出为高电平"
        elephant_client.set_digital_out(0,1)
        "控制机器人等待1秒后再动作"
        elephant_client.wait(1)

        "控制机器人朝Z轴方向笛卡尔运动到码垛抓取过渡点"
        elephant_client.write_coord(2,321.533,3000)
        elephant_client.command_wait_done()

        "控制机器人运动到放置过渡点"
        elephant_client.write_coords([86.687,255.542,320.867,177.065,-1.333,-128.721], 3000)
        elephant_client.command_wait_done()

        "控制机器人朝Z轴方向笛卡尔运动到码垛放置点"
        elephant_client.write_coord(2,241.533,3000)
        elephant_client.command_wait_done()
        
        "控制机器人OUT1输出为低电平"
        elephant_client.set_digital_out(0,0)
        elephant_client.wait(1)

        "控制机器人朝Z轴方向笛卡尔运动到码垛放置过渡点"
        elephant_client.write_coord(2,321.533,3000)
        elephant_client.command_wait_done()

        "机器人关节运动到安全点"
        elephant_client.write_angles([94.828,-143.513,135.283,-82.969,-87.257,-44.033],1000)
        elephant_client.command_wait_done() -->

   
<!-- ``` -->

---
[← 上一页](../6-SDKDevelopment.md) | [下一页 → ](../../11-ApplicationBaseROS/11.1-ROS1/README.md)