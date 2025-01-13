# **API接口说明**

## **1 概述**

大象机器人允许用户使用Socket远程控制机器人。 我们使用TCP协议在客户端和机器人之间进行通信，用户可以通过TCP发送格式化字符串来获取或设置机器人的某些属性/状态，每个API的格式介绍如下。

## **2 Socket字符串格式规范**

### **2.1 获取机器人当前角度**

Socket字符串格式：`get_angles()`

- **功能：** 获取所有关节角度
- **返回值：** `list`一个浮点值的列表,代表所有关节的角度
- **示例：** 调用成功，将收到 **get_angles:[0.174058, 0.520382, -0.07874, 0.092855, 0.0, 0.030356]**，如果发生错误，将返回InvalidAngles()函数（格式为**[-1.0, -2.0, -3.0, -4.0, -1.0, -1.0]**）

### **2.2 设置机器人的角度**

Socket字符串格式：`set_angles(joint1_angle, joint2_angle, joint3_angle, joint4_angle, joint5_angle, joint6_angle,speed) `

- **功能：**  发送所有角度给机械臂所有关节
- **参数说明：**
  - `joint1_angle`:关节1角度，范围-180.00 ~ 180.00
  - `joint2_angle`:关节2角度，范围-270.00 ~ 90.00
  - `joint3_angle`:关节3角度，范围-150.00 ~ 150.00
  - `joint4_angle`:关节4角度，范围-260.00 ~ 80.00
  - `joint5_angle`:关节5角度，范围-168.00 ~ 168.00
  - `joint6_angle`:关节6角度，范围-174.00 ~ 174.00
  - `speed`: 表示机械臂运动的速度，取值范围是0 ~ 2000
- **示例：** **set_angles(10.0,11.0,12.2,12.3,11.1,16.0,500) **，如果成功调用，将会收到：**set_angles:[ok]** ，如果发送数据错误，将会收到：**set_angles:error_message**

### **2.3 设置一个关节的角度**

Socket字符串格式：`set_angle(joint,angle, speed)`

- **功能：**  发送指定的单个关节运动至指定的角度
- **参数说明：**
  - `joint`: J1 / J2 / J3 / J4 / J5 / J6
  - `angle`: 具体每个关节角度范围请参考set_angles()函数的参数说明
  - `speed`: 表示机械臂运动的速度，取值范围是0 ~ 2000
- **示例：** **set_angle(J1,50.5,500)**，如果成功调用，将会收到：**set_angle：[ok]**，如果发生错误，将会收到：**set_angle:error_message**

### **2.4 获取机器人的当前坐标**

Socket字符串格式：`get_coords()`

- **功能：** 获取当前坐标和姿态
- **返回值：** `list`包含坐标和姿态的列表，长度为 6，依次为 `[x, y, z, rx, ry, rz]`
- **示例：** 如果成功调用，将会收到：**get_coords :[0.174058, 0.520382, -0.07874, 0.092855, 0.0, 0.030356]**，如果发生错误，将返回InvalidCoords()函数（格式为**[-1.0, -2.0, -3.0, -4.0, -1.0, -1.0]**）

### **2.5 设置机器人的坐标**

Socket字符串格式：`set_coords(axis_x_coord, axis_y_coord, axis_z_coord, axis_rx_coord, axis_ry_coord, axis_rz_coord,speed)`

- **功能：** 发送整体坐标和姿态,让机械臂头部从原来点移动到指定点
- **参数说明：**
  - `axis_x_coord`: x坐标
  - `axis_y_coord`: y坐标
  - `axis_z_coord`: z坐标
  - `axis_rx_coord`: rx坐标
  - `axis_ry_coord`: ry坐标
  - `axis_rz_coord`: rz坐标
  - `speed`: 表示机械臂运动的速度，范围是0 ~ 2000

- **示例：** **set_coords(10.0,11.0,12.2,12.3,11.1,16.0,500)**，如果成功调用，将会收到：**set_coords:[ok]**，如果发生错误，将会收到：**set_coords:error_message**

### **2.6 设置一个轴的坐标**

Socket字符串格式：`set_coord(axis,coordinate ,speed)` 

- **功能：** 发送单个坐标值给机械臂进行移动
- **参数说明：**
  - `axis`: x / y / z / rx / ry / rz
  - `coordinate`: 输入您想要到达的坐标值
  - `speed`: 表示机械臂运动的速度，范围是0-2000
- **示例：** **set_coord(x,50.5,500) **，如果成功调用，将会收到：**set_coords:[ok]**。如果发生错误，将会收到：**set_coords:error_message**

### **2.7 获取数字输出引脚的信号**

Socket字符串格式：`get_digital_out(pin_number)` 

- **功能：** 获取输出引脚信号
- **参数说明：**
  - `pin_number`: 0 ~ 5 对应底座电气接口 OUT 1 ~ 6 ; 16 ~ 17 对应机械臂末端电气接口 OUT 1 ~ 2 （可查阅Pro600使用手册对照确认）
- **示例：** **get_digital_out(1)** ,如果成功调用，将会收到：**get_digital_out:0** 或 **get_digital_out:1**  ，如果发生错误，将会收到：**get_digital_out:error_message**

### **2.8 设置数字输出引脚的信号**

Socket字符串格式：set_digital_out(pin_number,signal)

- **功能：** 设置输出引脚信号
- **参数说明：**
  - `pin_number`: 0 ~ 5 对应底座电气接口 OUT 1 ~ 6 ; 16 ~ 17 对应机械臂末端电气接口 OUT 1 ~ 2 （可查阅Pro600使用手册对照确认）
  - `signal` : 1 - 高电平，0 - 低电平
- **示例：** **set_digital_out(1,1)** 如果成功调用，将会收到：**set_digital_out:[ok]**，如果发生错误，将会收到：**set_digital_out:error_message**

### **2.9 获取引脚中的数字信号**

Socket字符串格式：`get_digital_in(pin_number)` 
- **功能：** 获取输入引脚信号
- **参数说明：**
  - `pin_number`: 0 ~ 5 对应底座电气接口 IN 1 ~ 6 ; 16 对应机械臂末端电气接口 IN 1  （可查阅Pro600使用手册对照确认）
- **示例：** **get_digital_in(1)** , 如果成功调用，将会收到：**get_digital_in:0** 或 **get_digital_in:1**  ，如果发生错误，将会收到：**get_digital_in:error_message**

### **2.10 向一个方向连续改变一个轴的坐标**

Socket字符串格式：`jog_coord(axis,direction,speed)`

- **功能：** 控制机器人按照指定的坐标轴方向持续移动
- **参数说明：**
  - `axis`: 代表不同的方向，可用参数有 x / y / z / rx / ry / rz 
  - `direction`: 主要控制机器臂移动的方向, -1 - 负方向 ，0 - 停止，1 - 正方向
  - `speed`: 速度 0 ~ 2000
- **示例：** **jog_coord(x,1, 500) ** ，如果成功调用，将会收到：**jog_coord:[ok]**，如果发生错误，将会收到：**jog_coord:error_message**

### **2.11 向一个方向连续改变一个关节的角度**

Socket字符串格式：`jog_angle(joint,direction,speed)` 

- **功能：** 控制机器人按照指定的角度持续移动
- **参数说明：**
  - `joint`: 代表机械臂的关节，可用参数有 J1 / J2 / J3 / J4 / J5 / J6
  - `direction`: 主要控制机器臂移动的方向，-1 - 负方向 ，0 - 停止，1 - 正方向
  - `speed`: 速度 0 ~ 2000
- **示例：** **jog_angle(J1, 1, 500)** ，如果成功调用，将会收到：**jog_angle:[ok]**,  如果发生错误，将会收到：**jog_angle:error_message**

### **2.12 启动系统**

**提示：用此命令前，需先使用power_on()，使机械臂上电，否则无法启动系统**

Socket字符串格式：`state_on()`

- **功能：** 启动系统
- **示例：** **state_on()**，如果成功调用，将会收到：**state_on:[ok]** ，如果发生错误，将会收到：**state_on:error_message**

### **2.13 关闭系统**

Socket字符串格式：`state_off()`

- **功能：** 关闭系统，但是机械臂仍然处于上电状态
- **示例：** **state_off()**，如果成功调用，将会收到：**state_off:[ok]**，如果发生错误，将会收到：**state_off:error_message**

### **2.14 停止任务**

Socket字符串格式：`task_stop()`

- **功能：** 停止运行程序
- **示例：** **task_stop()** ，如果成功调用，将会收到：task_stop:[ok]，如果发生错误，将会收到：**task_stop:error_message**

### **2.15 设置进给速率**

Socket字符串格式：`set_feed_rate(speed)`

- **功能：** 设置速度
- **参数说明：**
  - `speed`: 速度 0 ~ 100
- **示例：** **set_feed_rate(50.0)**，如果成功调用，将会收到：**set_feed_rate: 0**，返回其他值则为调用失败。

### **2.16 让机器人短暂休眠**

Socket字符串格式：`wait(seconds)` 

- **功能：** 设置系统等待时间
- **参数说明：**
  - `seconds`: 等待时长
- **示例：** **wait(10.5) **，如果成功调用，将会收到：**wait:[ok]**，如果发生错误，将会收到：**wait:error_message**。这个功能将使机器人在给定的几秒钟内“休眠”，不执行任何收到的指令。

### **2.17 翻转Z轴的值**

Socket字符串格式：`set_upside_down(up_dn)`

- **功能：**  翻转Z轴的值
- **参数说明：**
  - `up_dn`: 1 - 翻转，0 - 不翻转
- **示例：** **set_upside_down(1)**，如果成功调用，将会收到：**set_upside_down:[ok]**，如果发生错误，将会收到：**set_upside_down:error_message**

### **2.18 机器人上电**

Socket字符串格式：`power_on()`

- **功能：**  机器人上电
- **示例：** **power_on()**，如果成功调用，将会收到：**power_on:[ok]**，如果发生错误，将会收到：**power_on:error_message**

### **2.19 机器人断电**

Socket字符串格式：`power_off()`


- **功能：**  机器人断电
- **示例：** **power_off()**，如果成功调用，将会收到：**power_off:[ok]**，如果发生错误，将会收到：**power_off:error_message**

### **2.21 获取机器人运行速度**

Socket字符串格式：`get_speed()` 

- **功能：**  获取运行速度，速度参数单位是mm/s
- **示例：** **get_speed() **，如果成功调用，将会收到：**get_speed: speed**，如果发生错误，将会收到：**get_speed:error_message**

### **2.22 检查机器人状态**

Socket字符串格式：`state_check()`

- **功能：** 获取机器人状态
- **示例：** **state_check()** ，如果机器人处于正常状态，将会收到**state_check:1**，如果机器人处于非正常状态，将会收到**state_check:0**，如果发生错误，将会收到：**state_check:error_message**

### **2.23 检查机器人是否在运行**

Socket字符串格式：`check_running()`

- **功能：** 检查机器人是否在运行
- **示例：** **check_running()**，如果机器人正在运行，将会收到**check_running:1**，如果机器人未运行，将会收到**check_running:0**，如果发生错误，将会收到：**check_running:error_message**

### **2.24 设置机器人的扭矩限制**

Socket字符串格式：`set_torque_limit(axis,torque)`

- **功能：** 设置机器人的扭矩限制
- **参数说明：**
  - `axis`: x / y / z / rx / ry / rz 
  - `torque`: 范围为0 ~ 2 ，扭矩单位为N
- **示例：** **set_torque_limit(x,10.0)** ，如果成功调用，将会收到：**set_torque_limit:[ok]**，如果发生错误，将会收到：**set_torque_limit:error_message**

### **2.25 打开一个g_code格式的文件**

Socket字符串格式：`program_open(file_path_name)`

- **功能：** 打开一个g_code格式的文件
- **参数说明：** 
  - `file_path_name`: 要打开文件的绝对路径
- **示例：** **program_open(/usr/a.txt) **，如果成功调用，将会收到：**program_open:0**，如果发生错误，将会收到：**program_open:error_message**

### **2.26 从给定的g_code格式文件行中运行指定行**

Socket字符串格式：`program_run(line_number)`

- **功能：** 从给定的g_code格式文件行中运行指定行
- **参数说明：** 
  - `line_number`: 要运行的代码的行数
- **示例：** **program_run(0)**，如果成功调用，将会收到：**program_run:0**，如果发生错误，将会收到：**program_run:error_message**

### **2.27 获取机器人错误信息**

Socket字符串格式：`read_next_error()`

- **功能：** 机器人错误检测
- **示例：** **read_next_error()**，如果成功调用，将会收到：**read_next_error:error_message**

### **2.28 设置机器人的有效载荷**

Socket字符串格式：`set_payload(payload)`

- **功能：** 设置机器人的有效负载
- **参数说明：**
  - `payload`: 范围 0.0 ~ 2.0，单位为kg
- **示例：** **set_payload(1.0)**，如果成功调用，将会收到：**set_payload:[ok]**，如果发生错误，将会收到：**set_payload:error_message**

### **2.29 设置机器人的加速度**

Socket字符串格式：`set_acceleration(acc)` 

- **功能：** 设置机器人的加速度
- **参数说明：**
  - `acc` : 加速度，必须为整数，单位为mm/s
- **示例：** **set_acceleration(50)**，如果成功调用，将会收到：**set_acceleration:[ok]**，如果发生错误，将会收到：**set_acceleration:error_message**

### **2.30 获取机器人的加速度**

Socket字符串格式：`get_acceleration()` 

- **功能：** 获取机器人的加速度
- **示例：** **get_acceleration()**，如果成功调用，将会收到：**get_acceleration: acc(实际加速度)**

### **2.31 等待命令完成**

Socket字符串格式：`wait_command_done()` 

- **功能：** 等待到上一个命令完成为止
- **示例：** **wait_command_done()**，如果成功调用，将会收到：**set_payload:0**，如果发生错误，将会收到：**set_payload:error_message**

### **2.32 暂停程序**

Socket字符串格式：`pause_program()` 

- **功能：** 暂停正在运行的程序
- **示例：** **pause_program() **，如果成功调用，将会收到：**pause_program:[ok]**，如果发生错误，将会收到：**pause_program:error_message**

### **2.33 恢复程序**

Socket字符串格式：`resume_program()`

- **功能：** 恢复被 暂停的程序
- **示例：** **resume_program()**，如果成功调用，将会收到：**resume_program:[ok]**，如果发生错误，将会收到：**resume_program:error_message**

### **2.34 变量赋值**

Socket字符串格式：`assign_variable("variable_name",value)`
- **功能：** 给定义好的变量赋值
- **示例：** **assign_variable("A",10)** ，**assign_variable("A",10.20202)** 或**assign_variable("B",”ABC”)** 或 **assign_variable("C",True)**，**assign_variable("C",False)**

变量名需要使用双引号（""）进行引用；值是字符串，使用双引号（“”）引用，值是整数型或者浮点型时，不需要用序号，直接写数职即可，值为布尔型时，用True/False，直接写0/1，变量会被改为整数型

返回字符串被格式化为键值对，键是函数名，值是接收自机器人的值，如果成功调用，将会收到：**assign_variable:[ok]**。如果发生错误，将会收到：**assign_variable:[wrong request format]**。

