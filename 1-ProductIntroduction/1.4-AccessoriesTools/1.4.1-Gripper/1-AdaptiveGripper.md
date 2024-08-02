# **myCobotPro Adaptive Gripper**

> **Compatible models:** myCobot 320, myCobot Pro 630,myCobot Pro 600

## Product Image

<img src="../../../resources/1-ProductIntroduction/1.4/1.4.1-Gripper/1-AdaptiveGripper/1.4.1自适应夹爪1.png" alt="img-1" width="800" height="auto" />


## Specifications

| **Name** | **myCobotPro Adaptive Gripper Black and White** |
| :----------- | :-------------------------------------- |
| Material | Photosensitive resin + nylon |
| Process technology | 3D printing |
| Gripping range | 0-90 mm |
| Clamping force | 1000 grams |
| Drive mode | Electric drive |
| Gearbox mode | Gear + connecting rod |
| Dimensions | 158x105x55mm |
| Weight | 350 grams |
| Fixing method | Screw fixing |
| Environment requirements | Normal temperature and pressure |
| Control interface | Serial port/IO control |
| Applicable devices | myCobot 320 series, myCobot Pro 630, myCobot Pro 600 |
<!-- | Repeatability accuracy | 0.5 mm |
| Service life | 1 year | -->
## Used for grabbing objects

### Introduction

- A manipulator is a robot component that works like a human hand. It has the advantages of complex structure, firm gripping of objects, not easy to fall, and easy operation.

- The gripper kit includes gripper connection wires and flanges. The end effector of the manipulator is controlled by a programmable system to realize functions such as grabbing objects and multi-point positioning. The gripper can be used in all development environments, such as ROS, Arduino, Roboflow, etc.

### Working principle

- Driven by the motor, the finger surface of the manipulator makes linear reciprocating motion to achieve opening or closing actions. The acceleration and deceleration of the electric manipulator are controllable, the impact on the workpiece is minimal, the positioning point is controllable, and the clamping is controllable.

### Applicable objects

- Small cubes

- Small balls

- Long objects

<!-- Purchase link:

- [Taobao](https://shop504055678.taobao.com)

- [shopify](https://shop.elephantrobotics.com/) -->

### Installation and use

- Gripper installation:

- Structural installation:

1. Align the gasket with the hole at the end of the robot arm and tighten it with screws:
![](../../../resources/1-ProductIntroduction/1.4/1.4.1-Gripper/1-AdaptiveGripper/j3.jpg)

2. Align the screw holes of the gripper with the holes around the gasket and tighten them with thin screws:
![](../../../resources/1-ProductIntroduction/1.4/1.4.1-Gripper/1-AdaptiveGripper/j2.jpg)

![](../../../resources/1-ProductIntroduction/1.4/1.4.1-Gripper/1-AdaptiveGripper/j1.jpg)

- Electrical connection:

![](../../../resources/3-UserNotes/jigao.png)

> **Note that the robot arm should be powered off, that is, the green light at the end should not be on when plugging and unplugging. If hot-plugging is performed with power on, there is a risk of damaging the gripper. **

1. Align the m8 cable with the interface of the robot arm. Note that there is a notch at the interface and a corresponding protrusion on the connecting cable. After confirming the direction, insert it and tighten it:
![](../../../resources/1-ProductIntroduction/1.4/1.4.1-Gripper/1-AdaptiveGripper/电气连接1.png)
2. Insert the gripper control interface, and also pay attention to the direction of the notch:
![](../../../resources/1-ProductIntroduction/1.4/1.4.1-Gripper/1-AdaptiveGripper/电气连接2.png)

<br>

## Python programming control
You need to use roboflow to enable the robot first, then run the following python script to test whether the gripper is normal
![](../../../resources/1-ProductIntroduction/1.4/1.4.1-Gripper/1-AdaptiveGripper/on.png)
![](../../../resources/1-ProductIntroduction/1.4/1.4.1-Gripper/1-AdaptiveGripper/state.png)

Confirm the IP address of the robot: Enter ifconfig in the terminal to obtain
![](../../../resources/1-ProductIntroduction/1.4/poweron/ip.png)

## Python programming control
You need to use roboflow to enable the robot first, then run the following python script to test whether the gripper is normal
![](../../../resources/1-ProductIntroduction/1.4/1.4.1-Gripper/1-AdaptiveGripper/on.png)
![](../../../resources/1-ProductIntroduction/1.4/1.4.1-Gripper/1-AdaptiveGripper/state.png)

Confirm the IP address of the robot: Enter ifconfig in the terminal to obtain
![](../../../resources/1-ProductIntroduction/1.4/poweron/ip.png)

### IO control mode
```python
from pymycobot import ElephantRobot
import time

# Change the ip to the real-time ip of the P600 Raspberry Pi

elephant_client = ElephantRobot("192.168.10.158", 5001)

# Necessary commands to start the robot
elephant_client.start_client()
time.sleep(1)
elephant_client.set_cag_gripper_mode(1)
time.sleep(1)
#elephant_client.power_off()#When changing the IO mode from gripper to gripper, you need to shut down the machine and restart the robot. If you only use gripper to gripper mode, you do not need to shut down the robot
elephant_client.power_off()
time.sleep(3)
elephant_client.state_off()
time.sleep(3)
elephant_client.power_on()
time.sleep(3)
elephant_client.state_on()
time.sleep(3)
elephant_client.set_digital_out(16, 0) # IO restores low level
time.sleep(1)
elephant_client.set_digital_out(17, 0) # IO restores low level
time.sleep(1)

# IO mode
# Gripper full open and full closed control code. Note that when the gripper is transparently switched to IO mode, you need to shut down the machine and restart the robot once before switching back to the gripper IO mode
for i in range(3):

    elephant_client.set_digital_out(16, 1) # Close the gripper
    time.sleep(1)
    elephant_client.set_digital_out(17, 0) # IO restores low level
    time.sleep(1)
    elephant_client.set_digital_out(16, 0) #IO restores low level
    time.sleep(1)
    elephant_client.set_digital_out(17, 1) # Open the gripper
    time.sleep(1)
    
    elephant_client.set_digital_out(16, 0) # IO restores low level
    time.sleep(1)
    elephant_client.set_digital_out(17, 0) # IO returns to low level
    time.sleep(1)

```

### Transparent transmission mode
```python
from pymycobot import ElephantRobot
import time

# Change the IP address to the real IP address of the P600 Raspberry Pi

elephant_client = ElephantRobot("192.168.10.158", 5001)

# Necessary commands to start the robot
elephant_client.start_client()
time.sleep(1)
elephant_client.set_cag_gripper_mode(0)
time.sleep(1)
# elephant_client.power_off()#When changing the IO mode of the gripper through transmission, you need to shut down the machine and restart the robot once. If you only use the gripper through transmission mode, you do not need to shut down the robot
elephant_client.state_off()
time.sleep(3)
elephant_client.power_on()
time.sleep(3)
elephant_client.state_on()
time.sleep(3)

#Transparent transmission mode

for i in range(3):
    elephant_client.set_cag_gripper_value(26,20)
    time.sleep(1)
    elephant_client.set_cag_gripper_value(86,20)
    time.sleep(1)
    
```
## Gripper zero position calibration
**The gripper has been zero-calibrated before leaving the factory. If the gripper's stroke is incorrect, you can calibrate it according to the following steps**

First turn off the robot in roboflow, and manually open the gripper to the maximum
![](../../../resources/1-ProductIntroduction/1.4/1.4.1-Gripper/1-AdaptiveGripper/off.png)

![](../../../resources/1-ProductIntroduction/1.4/1.4.1-Gripper/1-AdaptiveGripper/zero.jpg)

Then start the robot
![](../../../resources/1-ProductIntroduction/1.4/1.4.1-Gripper/1-AdaptiveGripper/on.png)

Then execute the following script

```python
from pymycobot import ElephantRobot
import time

# Change the IP address to the real IP address of the P600 Raspberry Pi

elephant_client = ElephantRobot("192.168.10.158", 5001)

# Necessary commands to start the robot
elephant_client.start_client()
time.sleep(1)
elephant_client.set_cag_gripper_mode(0)
time.sleep(1)
elephant_client.set_gripper_calibrate()
time.sleep(1)

```


---

[← Previous page](../README.md) | [Next page →](./2-ElectricGripper.md)