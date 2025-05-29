# Accessory related questions

**Q: How to use the electric gripper of 630 roboflow:**

A: The electric gripper must be initialized to ensure that the light is blue to use it normally. Flashing red light is abnormal
https://docs.google.com/document/d/1CVKVcCJSCgD87TlGKCsp2q1sG6oHwWit/edit

**Q: How to use the electric gripper of 630&600?**

The first step is to update pymycobot to 3.6.3

```bash
pip3 install pymycobot==3.6.3
```

```python
import time
from pymycobot import Phoenix
#Phoenix and roboflow conflict, so you can only use one. If you use roboflow, you cannot use phoneix, and vice versa

#You need to fill in your own ip address, debug is not a required item
#mg = Pro630("192.168.1.5",115200,debug=True)

mg = Phoenix()
#Power on the robot
mg.start_robot()

time.sleep(0.5)

mg.tool_set_gripper_electric_init()
time.sleep(0.5)

while True:
    mg.tool_set_gripper_electric_open()
    time.sleep(3)
    mg.tool_set_gripper_electric_close()
    time.sleep(3)

```

**Q: Does 600/630 use pro adaptive grippers?**

- A: Before starting the robot arm, you need to manually pull the grippers to the maximum.
After starting the robot arm, click as shown in the figure to test whether the grippers are working properly:
tool_out0: Close the grippers
tool_out1: Open the grippers

![](../resources/3-UserNotes/FAQ/img/acces_1.png)

First, click the test next to tool_out0 to test whether the grippers are open. If the grippers open normally after clicking, it is normal. Click tool_out0 again to close.
Click the test next to tool_out1 to test whether the grippers are closed. If the grippers open normally after clicking, it is normal. Click tool_out1 again to close.

**Q: How to control the grippers when writing programs using RoboFlow?**

As shown in the figure, select Basic Functions-Settings, select End Tool Pin Output, and select Only Once to control the closing/opening of the grippers once.

![](../resources/3-UserNotes/FAQ/img/acces_2.png)

**Q: Can I use transparent mode to control the gripper using RoboFlow?**
- A: No. RoboFlow currently only supports IO mode to control full open and full close. To use transparent mode, you need to use python or serial port assistant to control the robot arm.

**Q; How to use the camera flange on p600?**

A: You can refer to this case: https://blog.csdn.net/qq_29225913/article/details/101077821

**Q: Is there anything to pay attention to between the gripping object and the movement of the robot arm?**

When the load is > 500g, the speed needs to be less than 50%.



