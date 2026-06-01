# 五指灵巧手 (Five-Finger Dexterous Hand)

<img src="./img/five_finger_hand.jpg" alt="五指灵巧手" width="60%" height="60%" />

## 简介
五指灵巧手依靠机械臂末端完成供电与数据通信，上电后自动执行自检动作。通过 Python 接口可精准读写 6 个关节角度，自定义手指姿态，适用于手势演示、科研实验、柔性抓取等场景。

**兼容型号**: myCobot Pro 630

## 规格说明

| 名称 | 五指灵巧手 |
| :--- | :--- |
| **通信方式** | Modbus 通信 |
| **连接线缆** | 85 芯专用线缆 |
| **控制接口** | 机械臂末端接口 |
| **默认设备 ID** | 2 |
| **关节数量** | 6 轴 |
| **供电方式** | 机械臂末端供电 |
| **固定方式** | 法兰直装 |
| **适用设备** | myCobot Pro 630 |

## 工作流程
1. 设备上电后发出提示音；
2. 五指自动完成 **握紧 → 释放** 自检动作；
3. 自检完成后进入待机状态，此时可接收上位机指令控制。

## 关节角度范围

> [!WARNING]
> 设置角度需严格遵循下表范围，超出阈值程序会主动抛出异常！

| 关节编号 | 角度范围 |
| :---: | :--- |
| **J1** | 2.26° ~ 36.76° |
| **J2** | 100.22° ~ 178.37° |
| **J3** | 97.81° ~ 176.06° |
| **J4** | 101.38° ~ 176.54° |
| **J5** | 98.84° ~ 174.86° |
| **J6** | 0° ~ 90° |

## 硬件安装
1. 将五指灵巧手通过法兰盘固定在 myCobot Pro 630 机械臂末端；
2. 使用标配 85 芯线缆，一端连接灵巧手接口，另一端接入机械臂末端对应接口，确保插头插接牢固。

## Python 开发控制 (Pro 630 版本)

### 接口说明
- `get_five_fingers_angles(dev_id)`：获取灵巧手当前 6 轴关节角度，默认设备 ID 为 2。
- `set_five_fingers_angles(dev_id, angles)`：下发角度指令，控制灵巧手运动至指定姿态。

### 代码示例

```python
from pymycobot import ElephantRobot
import time

# 初始化机械臂连接，根据实际设备修改 IP 和端口
er = ElephantRobot("192.168.123.102", 5001)

# 启动客户端连接
er.start_client()

# 定义手指姿态角度
angles = [36.86, 100, 100, 100, 100, 0]
angles_1 = [36.76, 178, 176, 176, 174, 0]

# 控制灵巧手运动
er.set_five_fingers_angles(2, angles)
time.sleep(2)
er.set_five_fingers_angles(2, angles_1)

# 读取当前关节角度
current_angle = er.get_five_fingers_angles(2)
print("当前关节角度：", current_angle)
```
