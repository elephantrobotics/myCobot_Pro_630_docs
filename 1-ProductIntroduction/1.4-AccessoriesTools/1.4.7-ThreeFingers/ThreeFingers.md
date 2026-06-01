# 产品特性
## 1 产品规格参数
| 名称    | myGripper H100 三指灵巧手      |
| :----------- | :-------------------------------------- |
| 握持范围     | 0 - 130mm                                |
| 指尖数   | 3指，分别对应人手的：拇指 食指 无名指                                  |
| 使用寿命     | 10W次及以上                                    |
| 可活动关节     | 6个                                  |
| 电机类型   | 伺服舵机，支持电流、位置、速度控制                             |
| 重量         | 780g                               |
| 额定负载   | 500g                                  |
| 电源参数  | 24V2A                                 |
| 固定方法     | 螺丝固定                                |
| 使用环境要求 | 常温常压                                |
| 控制接口     | RS485控制                        |

**引脚线序说明**

<img src="/resources/2-serialproduct/myCobot%20Pro%20600/Chinese/new485.png" width="50%" >

编号1,5 连接GND与24V，编号2,3 为控制 IO 输入，编号6,7 为 IO 输出，编
号4,8为485 通信，是与灵巧手接收与发送指令

**注意事项**：

为保障灵巧手设备安全运行，请严格根据线标区分线序，如出现线标丢失、脱落、遗忘等情况，请立即通过官方渠道联系技术团队。若因未规范操作导致损坏，我司将依据合同条款承担相应维修费用。

## 2 主控制器规格参数表

| 名称    | ESP32     |
| :----------- | :-------------------------------------- |
| 核心参数     | 240MHz dual core. 600 DMIPS, 520KB SRAM. Wi-Fi, dual mode Bluetooth                               |
| Flash  | 4MB                                  |


## 3 python开发

**USB-485模块接线**：

连接灵巧手端的 24V，GND, 485_A(T/R+,485+) , 485_B(T/R-,485-)共 4 根线，电源为24V直流稳压电源，将模块的 USB 插口插入到电脑的 USB 接口

<img src="../img/new485.png" width="50%" >

485A 接入 485 转 USB 模块 A+;<br>
485B 接入 485 转 USB 模块 B-;<br>
24V 接入 24V 直流稳压电源正极;<br>
GND 接入 24V 直流稳压电源负极<br>

**驱动库安装**
[点击下载驱动库](https://github.com/elephantrobotics/Myhand)

##### 串口依赖库安装
在电脑终端执行下面命令，安装依赖库
```bash
pip install pyserial
```
## API说明

### get_gripper_firmware_version()

- **功能:** 获取夹爪固件主版本号
- **参数:** 无
- **返回:** `(int)`固件主版本号

### get_gripper_modified_version()

- **功能:** 获取夹爪固件次版本号
- **参数:** 无
- **返回:** `(int)`固件次版本号

### get_gripper_gripper_Id()

- **功能:** 获取夹爪ID
- **参数:** 无
- **返回:** `(int)`夹爪ID


### get_gripper_gripper_baud()

- **功能:** 获取夹爪波特率
- **参数:** 无
- **返回:**`(int)` 0-5
    - `0`: 115200
    - `1`: 1000000
    - `2`: 57600
    - `3`: 19200
    - `4`: 9600
    - `5`: 4800

### get_gripper_joint_angle(id)

- **功能:** 获取夹爪的当前位置数据信息
- **参数:** `id`: `(int)` 夹爪关节ID,取值范围 `1-6`  
- **返回:** `(int)`夹爪关节ID的当前位置数据

### get_gripper_status()

- **功能:** 获取夹爪的当前状态
- **参数:** 无
- **返回:**`(int)` 0-3
    - `0`:  正在运动
    - `1`: 停止运动,未检测到夹到物体
    - `2`: 停止运动,检测到夹到了物体
    - `3`: 检测到夹到物体以后,物体掉落

### get_gripper_joint_speed(id)

- **功能:** 获取夹爪关节ID的当前速度
- **参数:** `id`: `(int)` 夹爪关节ID,取值范围 `1-6`  
- **返回:** `(int)`夹爪关节ID的当前速度

### get_gripper_joint_P(id)

- **功能:** 获取夹爪关节ID的PID的P值
- **参数:** `id`: `(int)` 夹爪关节ID,取值范围 `1-6`  
- **返回:** `(int)`夹爪关节ID的PID的P值

### get_gripper_joint_I(id)

- **功能:** 获取夹爪关节ID的PID的I值
- **参数:** `id`: `(int)` 夹爪关节ID,取值范围 `1-6`
- **返回:** `(int)`夹爪关节ID的PID的I值

### get_gripper_joint_D(id)

- **功能:** 获取夹爪关节ID的PID的D值
- **参数:** `id`: `(int)` 夹爪关节ID,取值范围 `1-6`
- **返回:** `(int)`夹爪关节ID的PID的D值

### get_gripper_joint_cw(id)

- **功能:** 获取夹爪关节ID的顺时针可运行误差
- **参数:** `id`: `(int)` 夹爪关节ID,取值范围 `1-6`
- **返回:** `(int)`夹爪关节ID的顺时针可运行误差

### get_gripper_joint_cww(id)

- **功能:** 获取夹爪关节ID的逆时针可运行误差
- **参数:** `id`: `(int)` 夹爪关节ID,取值范围 `1-6`
- **返回:** `(int)`夹爪关节ID的逆时针可运行误差

### get_gripper_joint_mini_pressure(id)

- **功能:** 获取夹爪关节ID的最小启动力
- **参数:** `id`: `(int)` 夹爪关节ID,取值范围 `1-6`
- **返回:** `(int)`夹爪关节ID的最小启动力

### get_gripper_joint_mini_pressure(id)

- **功能:** 获取夹爪关节ID的最小启动力
- **参数:** `id`: `(int)` 夹爪关节ID,取值范围 `1-6`
- **返回:** `(int)`夹爪关节ID的最小启动力

### get_gripper_angles()

- **功能:** 获取夹爪6个关节的角度
- **参数:** `id`: `(int)` 夹爪关节ID,取值范围 `1-6`
- **返回:** `(list)`夹爪6个关节的角度

### set_gripper_Id(value)

- **功能:** 设置夹爪ID号
- **参数:** 
  - `value`: `(int)` 夹爪ID,取值范围 `1-254`
- **返回:**`(int)` 0-1
  - `0`: 失败
  - `1`: 成功

### set_gripper_baud(value)

- **功能:** 设置夹爪波特率
- **参数:** 
  - `value`: `(int)` 夹爪波特率,取值范围 `0-5`
    - `0`: 115200
    - `1`: 1000000
    - `2`: 57600
    - `3`: 19200
    - `4`: 9600
    - `5`: 4800
- **返回:**`(int)` 0-1
  - `0`: 失败
  - `1`: 成功
  
### set_gripper_enable(value)

- **功能:** 设置夹爪使能状态
- **参数:** 
  - `value`: `(int)` 使能状态,取值范围 `0-1`
    - `0`: 掉使能
    - `1`: 上使能
- **返回:**`(int)` 0-1
  - `0`: 失败
  - `1`: 成功

<!-- ### set_gripper_value(value,speed)

- **功能:** 设置夹爪以指定的速度转动到指定的位置
- **参数:** 
  - `value`: `(int)` 位置,取值范围 `0-100`
  - `speed`: `(int)` 速度,取值范围 `1-100` 
- **返回:**`(int)` 0-1
  - `0`: 失败
  - `1`: 成功 -->

### set_gripper_joint_calibration(id)

- **功能:** 设置夹爪关节ID零位校准
- **参数:** `id`: `(int)` 夹爪关节ID,取值范围 `1-6`
- **返回:**`(int)` 0-1
  - `0`: 失败
  - `1`: 成功

### set_gripper_joint_P(id,value)

- **功能:** 设置夹爪关节ID的PID的P值
- **参数:** 
  - `id`: `(int)` 关节ID,取值范围 `1-6`
  - `value`: `(int)` P值,取值范围 `0-254`
- **返回:**`(int)` 0-1
  - `0`: 失败
  - `1`: 成功

### set_gripper_joint_I(id,value)

- **功能:** 设置夹爪关节ID的PID的I值
- **参数:** 
  - `id`: `(int)` 关节ID,取值范围 `1-6`
  - `value`: `(int)` I值,取值范围 `0-254`
- **返回:**`(int)` 0-1
  - `0`: 失败
  - `1`: 成功

### set_gripper_joint_D(id,value)

- **功能:** 设置夹爪关节ID的PID的D值
- **参数:**
  - `id`: `(int)` 关节ID,取值范围 `1-6` 
  - `value`: `(int)` D值,取值范围 `0-254`
- **返回:**`(int)` 0-1
  - `0`: 失败
  - `1`: 成功

### set_gripper_joint_cw(id,value)

- **功能:** 设置夹爪关节ID的顺时针可运行误差
- **参数:**
  - `id`: `(int)` 关节ID,取值范围 `1-6`  
  - `value`: `(int)` 误差,取值范围 `0-16`
- **返回:**`(int)` 0-1
  - `0`: 失败
  - `1`: 成功

### set_gripper_joint_cww(id,value)

- **功能:** 设置夹爪关节ID的逆时针可运行误差
- **参数:**
  - `id`: `(int)` 关节ID,取值范围 `1-6` 
  - `value`: `(int)` 误差,取值范围 `0-16`
- **返回:**`(int)` 0-1
  - `0`: 失败
  - `1`: 成功

### set_gripper_joint_mini_pressure(id,value)

- **功能:** 设置夹爪关节ID的最小启动力
- **参数:**
  - `id`: `(int)` 关节ID,取值范围 `1-6` 
  - `value`: `(int)` 最小启动力,取值范围 `0-254`
- **返回:**`(int)` 0-1
  - `0`: 失败
  - `1`: 成功

### set_gripper_joint_torque(id,value)

- **功能:** 设置夹爪关节ID的扭矩
- **参数:**
  - `id`: `(int)` 关节ID,取值范围 `1-6` 
  - `value`: `(int)` 扭矩,取值范围 `0-100`
- **返回:**`(int)` 0-1
  - `0`: 失败
  - `1`: 成功


### set_gripper_joint_speed(id,speed)

- **功能:** 设置夹爪关节ID的速度
- **参数:**
  - `id`: `(int)` 关节ID,取值范围 `1-6` 
  - `speed`: `(int)` 速度,取值范围 `1-100`
- **返回:**`(int)` 0-1
  - `0`: 失败
  - `1`: 成功

### set_gripper_angles(angles,speed)

- **功能:** 设置夹爪全关节角度
- **参数:** 
  - `angles`: `(list)` 6个关节角度,每个关节角度取值范围 `0-100`
  - `speed`: `(int)` 速度,取值范围 `1-100`
- **返回:**`(int)` 0-1
  - `0`: 失败
  - `1`: 成功


### set_gripper_action(value)

- **功能:** 设置夹爪捏合动作
- **参数:** 
  - `value`: `(int)` 动作,取值范围 `0-3`
    - `0`：食指与拇指捏合
    - `1`: 中指于拇指捏合
    - `2`: 三指握住
    - `3`: 双指夹持
- **返回:**`(int)` 0-1
  - `0`: 失败
  - `1`: 成功

### set_gripper_pose(pose,value,flag)

- **功能:** 设置夹爪捏合动作及开合程度
- **参数:** 
  - `pose`: `(int)` 动作,取值范围 `0-4`
    - `0`：全关节回零
    - `1`：食指与拇指捏合
    - `2`: 中指与拇指捏合
    - `3`: 中指与食指捏合
    - `4`: 三指捏合
  - `value`: `(int)` 开合程度,取值范围 `0-15`,合拢程度,等级越高越合拢
  - `flag`: `(int)` 空闲标志,标志1时,空闲手指可自由操控
    
- **返回:**`(int)` 0-1
  - `0`: 失败
  - `1`: 成功

#### 测试程序


```python
from MyHand import MyGripper_H100
import time
if __name__=="__main__":
    hand=MyGripper_H100("COM8")
    hand.set_gripper_pose(0,0)
    time.sleep(2)
    hand.set_gripper_pose(1,5)
    time.sleep(5)
    hand.set_gripper_pose(2,5)
    time.sleep(5)
    hand.set_gripper_pose(3,5)
    time.sleep(5)
    hand.set_gripper_pose(4,15)
    time.sleep(5)
    hand.set_gripper_pose(0,0)
    time.sleep(2)
```
