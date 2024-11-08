# Phoenix API介绍

**注意事项**：Phoenix API只能运行在机械臂的主控上，不能运行在客户的电脑上，而且如果要使用Phoenix API，需要手动将Roboflow关闭，否则会报错

##  API接口介绍
## 1 状态管理
### start_power_on_only()

- **功能:** 机械臂仅上电,不使能,末端Atom灯亮
- **参数:** 无
- **返回:**`(bool)` 
    - `True`:  上电完成
    - `False`: 上电失败
    
### start_power_on_only()

- **功能:** 机械臂仅上电,不使能,末端Atom灯亮
- **参数:** 无
- **返回:**`(bool)` 
    - `True`:  上电完成
    - `False`: 上电失败

### is_power_on()

- **功能:** 检查机械臂是否上电
- **参数:** 无
- **返回:**`(bool)` 
    - `True`:  机械臂已上电
    - `False`: 机械臂未上电

### is_servo_enabled(joint)

- **功能:** 获取对应关节连接状态
- **参数:** 
    - `joint`: Joint.J1 ~ Joint.J6
- **返回:**`(bool)` 
    - `True`:  已连接
    - `False`: 未连接

### is_all_servos_enabled()

- **功能:** 获取所有关节连接状态
- **参数:** 
    - `joint`: Joint.J1 ~ Joint.J6
- **返回:**`(bool)` 
    - `True`:  所有关节已连接
    - `False`: 存在未连接的关节/所有关节未连接

### start_robot()

- **功能:** 机械臂上电且使能,末端Atom灯亮
- **参数:** 无
- **返回:**`(bool)` 
    - `True`:  启动完成
    - `False`: 启动失败


<!-- ### _state_on()

- **功能:** 机械臂使能
- **参数:** 无
- **返回:**`(bool)` 
    - `True`:  启动系统完成
    - `False`: 启动系统失败

### _state_off()

- **功能:** 机械臂掉使能
- **参数:** 无
- **返回:** 无 -->

### state_check()

- **功能:** 获取系统启动状态
- **参数:** 无
- **返回:**`(bool)` 
    - `True`:  系统已启动
    - `False`: 系统未启动

### check_running()

- **功能:** 获取系统启动状态
- **参数:** 无
- **返回:**`(bool)` 
    - `True`:  运动中
    - `False`: 静止


### set_free_move_mode(on=True)

- **功能:** 设置自由移动模式
- **参数:** 
   - `True`: 打开自由移动模式
   - `False`: 关闭自由移动模式
- **返回:**`(bool)` 
    - `True`:  打开/关闭自由移动模式成功
    - `False`: 打开/关闭自由移动模式失败

### is_software_free_move()

- **功能:** 判断自由移动模式是否打开
- **参数:** 无
- **返回:**`(bool)` 
    - `True`:  自由移动模式已打开
    - `False`: 自由移动模式未打开

### get_payload()

- **功能:** 读取机械臂负载
- **参数:** 无
- **返回:**`(float)` 负载
    
### is_program_paused()

- **功能:** 判断程序是否暂停
- **参数:** 无
- **返回:**`(bool)` 
    - `True`:  程序已暂停
    - `False`: 程序未暂停

### get_error()

- **功能:** 读取机械臂报错信息
- **参数:** 无
- **返回:**`(tuple)` 返回报错信息

### get_joint_min_pos_limit(joint)

- **功能:** 获取对应关节最小角度
- **参数:** 
    - `joint`: Joint.J1 ~ Joint.J6
- **返回:**`(float)` 对应最小关节角
    
### get_joint_max_pos_limit(joint)

- **功能:** 获取对应关节最大角度
- **参数:** 
    - `joint`: Joint.J1 ~ Joint.J6
- **返回:**`(float)` 对应最大关节角


### get_joint_max_pos_limit(joint)

- **功能:** 获取对应关节最大角度
- **参数:** 
    - `joint`: Joint.J1 ~ Joint.J6
- **返回:**`(float)` 对应最大关节角

### get_acceleration()

- **功能:** 获取机械臂加速度
- **参数:** 无
- **返回:**`(float)` 加速度

### set_task_mode(task_mode)

- **功能:** 设置机器人任务模式
- **参数:** 
    - `task_mode`: 有AUTO模式、MANUAL模式、MDI模式
- **返回:**`(bool)` 是否成功设置任务模式（返回值总为真）

### release_joint_brake(joint, release=True)

- **功能:** 设置关节刹车状态
- **参数:** 
    - `joint`: Joint.J1 ~ Joint.J6
    - `release (bool)`: True - 打开刹车 False - 关闭刹车
- **返回:** 无

### set_mdi_mode()

- **功能:** 设置工作模式为MDI
- **参数:** 无
- **返回:** 无
    

### is_mdi_mode()

- **功能:** 判断当前工作模式是否是MDI
- **参数:** 无
- **返回:**`(bool)` 
    - `True`:  MDI模式
    - `False`: 不是MDI模式

### is_manual_ok()

- **功能:** 确认机械臂属于STATE_ON状态且机械臂当前没有运行任何指令
- **参数:** 无
- **返回:**`(bool)` 
    - `True`: 机械臂属于STATE_ON状态且机械臂当前没有运行任何指令
    - `False`: 指令未运行/或者不处于无使能状态





### get_motion_line()

- **功能:** 获取当前正在执行的命令行序号
- **参数:** 无
- **返回:** 当前正在执行的命令行序号

### get_robot_status()

- **功能:** 获取机械臂状态
- **参数:** 无
- **返回:**`(bool)` 
    - `True`:  正常
    - `False`: 已关闭/报错/无法运动

### get_robot_temperature()

- **功能:** 获取机械臂CPU温度
- **参数:** 无
- **返回:** `(float)`: 系统温度

### get_joint_state(joint)

- **功能:** 获取对应关节状态
- **参数:** 
    - `joint`: Joint.J1 ~ Joint.J6
- **返回:** JointState
    - `ERROR`: 关节有错误
    - `OK`: 上电有使能
    - `ERROR`: POWERED_OFF

### get_joint_communication(joint)

- **功能:** 获取对应关节通讯状态
- **参数:** 
    - `joint`: Joint.J1 ~ Joint.J6
- **返回:**`(bool)` 
    - `True`:  通讯正常
    - `False`: 通讯失败

### set_power_limit(power_limit)

- **功能:** 设置机械臂功率限制
- **参数:** 
    - `power_limit (float)`: 功率限制
- **返回:** 无

### get_power_limit()

- **功能:** 获取机械臂功率限制
- **参数:** 无
- **返回:** 
    - `float`: 功率限制
   
### set_stopping_time(stopping_time)

- **功能:** 设置机械臂停止时间
- **参数:** 
    - `stopping_time (float):`停止时间
- **返回:** 无

### get_stopping_time()

- **功能:** 获取机械臂停止时间
- **参数:** 无
- **返回:** 
    - `float`: 停止时间

### set_stopping_distance(stopping_distance)

- **功能:** 设置机械臂当前停止距离
- **参数:** 
    - `stopping_distance (float):`停止距离
- **返回:** 无

### get_stopping_distance()

- **功能:** 获取机械臂当前停止距离
- **参数:** 无
- **返回:** 
    - `float`: 停止距离

### set_tool_speed(tool_speed)

- **功能:** 获取工具速度
- **参数:** 
    - `tool_speed (float):`工具速度
- **返回:** 无

### get_tool_speed()

- **功能:** 获取机械臂当前停止距离
- **参数:** 无
- **返回:** 
    - `float`: 工具速度

### set_tool_force(tool_force)

- **功能:** 设置工具力
- **参数:** 
    - `tool_force (float):`工具力
- **返回:** 无

### get_tool_force()

- **功能:** 获取工具力
- **参数:** 无
- **返回:** 
    - `float`: 工具力

### set_max_speed(speed)

- **功能:** 获取工具力
- **参数:** 
   - `speed:` 最大速度, 0 ~ 100
- **返回:** 无

### program_open(program_file_path)

- **功能:** 打开G-code文件，仅支持绝对路径
- **参数:** 
    - `program_file_path:`ngc文件的绝对路径
- **返回:** 无

### program_run(start_line)

- **功能:** 从给定行开始运行G-code文件
- **参数:** 
    - `start_line (int):`起始行(第一行为0)
- **返回:**`(bool)` 
    - `True`:  发送成功
    - `False`: 发送失败

### get_current_line()

- **功能:** 从给定行开始运行G-code文件
- **参数:** 无
- **返回:**`int:` 当前执行行
    - `-1`:  程序当前未执行/执行结束
    - `1，2，3....x`:  程序当前执行行

### program_pause()

- **功能:** 暂停程序运行
- **参数:** 无
- **返回:** 无

### program_resume()

- **功能:** 恢复程序运行
- **参数:** 无
- **返回:** 无

### task_stop()

- **功能:** 停止机械臂并等待停止完成
- **参数:** 无
- **返回:** 无

### get_digital_in(pin_number)

- **功能:** 获取数字输入引脚值
- **参数:** 
    - `pin_number (DI):`输入引脚号
- **返回:**`(int)` 
    - `0`: 无输入
    - `1`: 有输入

### get_digital_out(pin_number)

- **功能:** 获取数字输出引脚值
- **参数:** 
    - `pin_number (DO）:`输出引脚号
- **返回:**`(int)` 
    - `0`: 无输出
    - `1`: 有输出

### set_digital_out(pin_number, pin_value)

- **功能:** 设置数字输出引脚值
- **参数:** 
    - `pin_number (DO)`:输出引脚号
    - `pin_value (int)`: 引脚值 (0 or 1)
      - `0`:关闭输出
      - `1`:打开输出
- **返回:** 无

### get_axis_speed(axis)

- **功能:** 获取对应坐标轴速度
- **参数:** 
    - `axis`:  Axis.X ~ Axis.RZ
- **返回:** 
    - `（float:）`: 坐标轴速度

### get_cmd_pos()

- **功能:** 获取轨迹姿态
- **参数:** 无
- **返回:** 
    - `list[float]`: G-code字符串列表

### get_cmd_joint()

- **功能:** 获取所需要的关节角度
- **参数:** 无
- **返回:** 
    - `list[float]`:  [J1,J2,J3,J4,J5,J6]

### get_current_speed()

- **功能:** 获取获取当前速度
- **参数:** 无
- **返回:** 
    - `（float）`:  当前速度

### get_default_speed()

- **功能:** 获取默认速度
- **参数:** 无
- **返回:** 
    - `（float）`: 默认速度

### get_default_acceleration()

- **功能:** 获取所默认加速度
- **参数:** 无
- **返回:** 
    - `（float）`:  默认加速度

### get_max_speed()

- **功能:** 获取最大速度
- **参数:** 无
- **返回:** 
    - `（float）`:  最大速度

### get_max_acceleration()

- **功能:** 获取最大加速度
- **参数:** 无
- **返回:** 
    - `（float）`:  最大加速度

### get_feedrate()

- **功能:** 获取当前进给速率
- **参数:** 无
- **返回:** 
    - `（float）`:  当前进给速率


### get_motion_enabled()

- **功能:** 获取轨迹规划器启用标志的状态
- **参数:** 无
- **返回:**`(bool)` 
    - `True`:   可以移动
    - `False`:  不可以移动

### coords_to_gcode(coords)

- **功能:** 将输入的坐标转换成G-code字符串
- **参数:** 
    - `coords(list[float | str])`：坐标
- **返回:**`list[str]`  G-code

### angles_to_gcode(angles)

- **功能:** 将输入的角度转换成G-code字符串
- **参数:** 
    - `angles(list[float | str])`：角度
- **返回:**`list[str]`  G-code

### coords_equal(coords_1, coords_2)

- **功能:** 判断输入的坐标是否相等
- **参数:** 
    - `coords_1`：坐标
    - `coords_2`：坐标
- **返回:**`(bool)` 
    - `True`:  相等
    - `False`: 不相等

### cangles_equal(angles_1, angles_2)

- **功能:** 判断输入的角度是否相等
- **参数:** 
    - `angles_1`：角度
    - `angles_2`：角度
- **返回:**`(bool)` 
    - `True`:  相等
    - `False`: 不相等

### tool_get_firmware_version()

- **功能:** 获取Pico固件版本号
- **参数:** 无
- **返回:** 当前固件版本

### tool_set_digital_out(pin_no, pin_value)

- **功能:** 设置数字输出引脚值（末端）
- **参数:** 
    - `pin_number (DO)`:输出引脚号
    - `pin_value (int)`: 引脚值 (0 or 1)
      - `0`:关闭输出
      - `1`:打开输出
- **返回:** 无

### tool_get_digital_in(pin_no)

- **功能:** 获取数字输入引脚值（末端）
- **参数:** 
    - `pin_no (int):`输入引脚号
- **返回:**`(int)` 
    - `0`: 无输入
    - `1`: 有输入

### tool_is_btn_clicked()

- **功能:** 判断机器人ATOM按钮是否被按下
- **参数:** 无
- **返回:**`(bool)` 
    - `True`:  按下
    - `False`: 未按

### tool_set_gripper_mode(mode)

- **功能:** 设置夹爪模式
- **参数:** 
    - `mode:`夹爪模式
        - `0`:485模式 
- **返回:** 无

### tool_set_gripper_enabled(enabled)

- **功能:** 设置夹爪使能
- **参数:** 
    - `enabled:`夹爪模式
        - `0`: 夹爪放松 
        - `1`: 夹爪锁紧
- **返回:** 无

### tool_set_gripper_calibrate()

- **功能:** 设置夹爪校准
- **参数:** 无
- **返回:** 无

### tool_set_gripper_value（value, speed）

- **功能:** 设置夹爪角度
- **参数:** 
    - `value:`夹爪角度
    - `speed:`夹爪速度
- **返回:** 无

### tool_set_gripper_state(state, speed)

- **功能:** 设置夹爪使能
- **参数:** 
    - `state:`夹爪状态
        - `0`: 全开
        - `1`: 全关
    - `speed:`夹爪速度
- **返回:** 无

### clear_all_errors()

- **功能:** 清除所有错误
- **参数:** 无
- **返回:** 无

### recover_robot()

- **功能:** 检测到碰撞或其他错误后恢复
- **参数:** 无
- **返回:** `(bool)` 
    - `True`:  恢复成功
    - `False`: 恢复失败

### enable_manual_brake_control()

- **功能:** 启用或禁用手动制动控制。
- **参数:** 无
- **返回:** 无


### set_joint_torque_limit(joint, torque_limit)

- **功能:** 设置笛卡尔扭矩限制
- **参数:** 
    - `joint:` Axis.X ~ Axis.RZ
    - `torque_limit(float）:`扭矩限制值
- **返回:**无
   
### set_axis_torque_limit(axis, value)

- **功能:** 设置对应关节扭矩限制值
- **参数:** 
    - `axis:`Joint.J1 ~ Joint.J6
    - `torque_limit(float）:`扭矩限制值
- **返回:**无


## 2 运动管理

### get_coords()

- **功能:** 获取所有坐标
- **参数:** 无
- **返回:**`(list)` 
    - `[X,Y,Z,RX,RY,RZ]`


### get_coord(axis)

- **功能:** 获取对应坐标
- **参数:** 
   - `axis`: Axis.X ~ Axis.RZ
- **返回:** 坐标
    
### get_angles()

- **功能:** 获取所有关节角度
- **参数:** 无
- **返回:**`(list)` 
    - `[J1,J2,J3,J4,J5,J6]`

### get_angle(joint)

- **功能:** 获取对应关节角度
- **参数:** 
   - `joint`: Joint.J1 ~ Joint.J6
- **返回:** 关节角度

### set_coords(list, speed)

- **功能:** 控制多坐标运动
- **参数:** 
  - `list`: [X,Y,Z,RX,RY,RZ]
  - `speed`: 0~100
- **返回:** 无

### set_coord(axis, coord, speed)

- **功能:** 控制单坐标运动
- **参数:** 
  - `axis:`: Axis.X ~ Axis.RZ
  - `coord `: 坐标
  - `speed `: 0-100
- **返回:** 无

### set_angles(list, speed)

- **功能:** 控制多关节运动
- **参数:** 
  - `list`: [J1,J2,J3,J4,J5,J6]
  - `speed`: 0~100
- **返回:** 无

### set_angle(joint, angle, speed)

- **功能:** 控制单关节运动
- **参数:** 
  - `joint:`: Joint.J1 ~ Joint.J6
  - `angle `: 角度
  - `speed `: 0-100
- **返回:** 无
  
### is_in_position(coords, is_linear)

- **功能:** 判断机械臂是否运动到对应角度/坐标
- **参数:** 
  - `coords (list[float])`: 坐标/角度
  - `is_linear (bool)`:
    - False (0) - 角度
    - True (1) - 坐标
- **返回:**`(bool)` 
    - `True`:  运动到位
    - `False`: 运动未到位

### is_in_commanded_position()

- **功能:** 判断机械臂是否运动到位
- **参数:** 无
- **返回:**`(bool)` 
    - `True`:  运动到位
    - `False`: 运动未到位

### jog_absolute_coord(axis, coord, speed)

- **功能:** 控制单坐标持续运动
- **参数:** 
  - `axis`: Axis.X ~ Axis.RZ
  - `coord (float)`: 坐标
  - `speed (float)`: 0~100
- **返回:**`(bool)` 
    - `True`:  开始持续运行
    - `False`: 失败

### jog_stop_all()

- **功能:** 停止所有角度/坐标运动
- **参数:** 无
- **返回:**`(bool)` 
    - `True`:  停止成功


    