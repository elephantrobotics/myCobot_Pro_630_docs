# Five-Finger Dexterous Hand
## Introduction
The five-fingered dexterous hand relies on the end of the robotic arm to complete power supply and data communication, and automatically performs self-checking actions after powering on. Through the Python interface, you can accurately read and write 6 joint angles and customize finger postures, which is suitable for gesture demonstrations, scientific research experiments, flexible grasping and other scenarios.

**Compatible models**: myCobot Pro 630

## Specifications

| Name | Five-Finger Dexterous Hand |
| :--- | :--- |
| **Communication method** | Modbus communication |
| **Connection cable** | 85-core special cable |
| **Control interface** | Robotic arm end interface |
| **Default Device ID** | 2 |
| **Number of joints** | 6 axes |
| **Power supply method** | Power supply at the end of the robotic arm |
| **Fixation method** | Flange direct mounting |
| **Applicable devices** | myCobot Pro 630 |

## Workflow
1. The device emits a beep after it is powered on;
2. Five fingers automatically complete the **grip → release** self-check action;
3. After the self-test is completed, it enters the standby state. At this time, it can receive instructions from the host computer for control.

## Joint angle range

> [!WARNING]
> The setting angle must strictly follow the range in the table below. If the threshold is exceeded, the program will actively throw an exception!

| Joint number | Angle range |
| :---: | :--- |
| **J1** | 2.26° ~ 36.76° |
| **J2** | 100.22° ~ 178.37° |
| **J3** | 97.81° ~ 176.06° |
| **J4** | 101.38° ~ 176.54° |
| **J5** | 98.84° ~ 174.86° |
| **J6** | 0° ~ 90° |

## Hardware installation
1. Fix the five-fingered dexterous hand to the end of the myCobot Pro 630 robotic arm through the flange;
2. Use the standard 85-core cable, connect one end to the smart hand interface, and the other end to the corresponding interface at the end of the robotic arm, ensuring that the plug is firmly connected.

## Python Development Control (Pro 630 version)

### Interface description
- `get_five_fingers_angles(dev_id)`: Get the current 6-axis joint angles of the dexterous hand, the default device ID is 2.
- `set_five_fingers_angles(dev_id, angles)`: Issue angle commands to control the movement of dexterous hands to the specified posture.

### Code Example

```python
from pymycobot import ElephantRobot
import time

# Initialize the robot arm connection and modify the IP and port according to the actual device
er = ElephantRobot("192.168.123.102", 5001)

# Start client connection
er.start_client()

# Define finger posture angle
angles = [36.86, 100, 100, 100, 100, 0]
angles_1 = [36.76, 178, 176, 176, 174, 0]

#Control dexterous hand movements
er.set_five_fingers_angles(2, angles)
time.sleep(2)
er.set_five_fingers_angles(2, angles_1)

# Read the current joint angle
current_angle = er.get_five_fingers_angles(2)
print("Current joint angle:", current_angle)
```
