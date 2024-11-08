# Phoenix API use case

**Note**: Phoenix API can only run on the robot's main control, not on the customer's computer. If you want to use Phoenix API, you need to manually shut down Roboflow, otherwise an error will be reported

## 1 Robot enable control
```Python
from pymycobot.mycobotpro630 import *
import time
p = Phoenix()
#Check if the robot is enabled. If not, enable the robot
while p.state_check()==False:
    p.start_robot()#Power on and enable the robot
    time.sleep(0.02)
time.sleep(2)
p._state_off()#Turn off the robot
p._power_off()#Power off the robot

```
## 2 Robot joint angle acquisition and control
```Python
from pymycobot.mycobotpro630 import *
import time
p = Phoenix()
#Check if the robot is enabled, if not, enable the robot
while p.state_check()==False:
    p.start_robot()
    time.sleep(0.02)
#Get the robot joint angle
print("angles=",p.get_angles())
#Wait for the robot motion command to execute before executing subsequent commands
def wait_done():
    while p.is_in_commanded_position()==False:
        time.sleep(0.1)

p.set_angles([0,-90,0,-90,0,0],20)#Joint moves to the specified joint angle
wait_done()#Wait for the motion command to complete
p.set_angles([00,-90,0,0,0,0],20)#Joint moves to the specified joint angle
wait_done()#Wait for the motion command to complete
```

## 3 Robot coordinate position acquisition and control
```Python
from pymycobot.mycobotpro630 import *
import time
p = Phoenix()
#Check if the robot is enabled, if not, enable the robot
while p.state_check()==False:
    p.start_robot()
    time.sleep(0.02)

#Get the robot coordinates and posture
print("coords=",p.get_coords())

#Wait for the robot motion command to execute before executing subsequent commands
def wait_done():
    while p.is_in_commanded_position()==False:
        time.sleep(0.1)

p.set_angles([0,-90,90,-91,-90,0],20)#Joint moves to the initial posture
wait_done()#Wait for the motion command to complete
p.set_coords([369.002, 46.685, 321.705, 175.578, 0.01, 83.526],20)#Coordinate movement to the specified position
wait_done()#Wait for the motion command to complete
p.set_coords([369.002, 46.685, 421.705, 175.578, 0.01, 83.526],20)#Coordinate movement to the specified position
wait_done()#Wait for the motion command to complete
```

## 4 Robot IO acquisition and control
```Python
from pymycobot.mycobotpro630 import *
import time
p = Phoenix()
#Check if the robot is enabled, if not, enable the robot
while p.state_check()==False:
    p.start_robot()
    time.sleep(0.02)

#DI.PIN_0 ~ DI.PIN_5 corresponds to robot IN1~IN6 input. If it returns 1, it means there is input, and if it returns 0, it means there is no input
print("IN1=",p.get_digital_in(DI.PIN_0))

#DO.PIN_0 ~ DO.PIN_5 corresponds to robot OUT1~OUT6 output
p.set_digital_out(DO.PIN_0,1)#OUT1 turns on output
time.sleep(2)
p.set_digital_out(DO.PIN_0,0)#OUT1 turns off output

```

## 5 Adaptive gripper control
```Python
from pymycobot.mycobotpro630 import *
from pymycobot import ElephantRobot
ElephantRobot.set_gripper_state()
import time
p = Phoenix()
#Check if the robot is enabled. If not, enable the robot
while p.state_check()==False:
    p.start_robot()
    time.sleep(0.02)

p.tool_set_gripper_mode(0)#Set the gripper to transparent mode
p.tool_set_gripper_value(0,100)#Set the gripper to be completely closed
time.sleep(1)
p.tool_set_gripper_value(100,100)#Set the gripper to be completely closed
time.sleep(1)

```