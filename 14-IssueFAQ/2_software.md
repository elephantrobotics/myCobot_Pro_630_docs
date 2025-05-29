# Software Problems

**Q: How to check the IP address of the robot and connect to VNC?**
WIFI connection:
After connecting to wifi, place the mouse on the wifi icon

![](../resources/3-UserNotes/FAQ/img/sofware_1.png)

Or click the icon in the upper right corner (as shown in the figure) and then check the position pointed by 2

![](../resources/3-UserNotes/FAQ/img/sofware_2.png)

**Q: Is there a formula for converting the Cartesian coordinate system into the 6-DOF angular coordinates of the p600?**

- A: No, but you can use send_coords to move to the target position and then read the current joint angle

**Q: When using a program to control the robot arm, the robot arm angle or coordinates cannot be read. What should I do if I cannot continue to control the movement of the robot arm after executing the first motion instruction?**

- A: It may be because there is no delay or waiting for the completion instruction when writing the program to control the robot arm. When using Python control, you can add command_wait_done() to make the robot complete the previous step before executing the next step

![](../resources/3-UserNotes/FAQ/img/sofware_3.png)

When using RoboFlow, you can add a delay to ensure that the robot completes the movement before executing the next command:

![](../resources/3-UserNotes/FAQ/img/sofware_4.png)

**Why does command_wait_done() return -1 after the robot moves?**

- A: It is because the robot arm moves for too long. If the running time exceeds 1 minute, command_wait_done() will return -1

**Solution**: Replace RoboFlow version: 630. The latest version of roboflow and update tutorial:

A: Close roboflow, then use a USB flash drive to copy the file to the Raspberry Pi and follow the video
Video:
https://drive.google.com/file/d/1KD1VxhzFYXEFF-3paO-ntMfGQMvjjLc2/view?usp=sharing
File:
https://drive.google.com/file/d/1lV2fTM-rNeZbccjJInpbKVhSzSXJGf4c/view?usp=sharing

**Why is there an error when starting the robot arm?**

![](../resources/3-UserNotes/FAQ/img/sofware_5.png)

![](../resources/3-UserNotes/FAQ/img/sofware_6.png)

If the above error occurs:
1. Check whether the emergency stop is in the released state. If not, turn the emergency stop knob clockwise to make it pop up.
2. If the emergency stop is in the released state, check whether the connection between the emergency stop and the robot arm is loose. You can tighten the connection.

![](../resources/3-UserNotes/FAQ/img/sofware_7.png)

If the above error occurs:
Check whether the joint prompted by the system has reached the limit. You need to turn off the power and adjust the joint to zero.
If the 456 joints are out of limit, please press the emergency stop switch, move the 456 joints back to the normal posture and then start the robot.
If the 123 joints are out of limit, you can follow the steps below to adjust the out-of-limit joint posture back:

① Enter the configuration center in roboflow, and click Power on only in the initialization bar
② Click Start Programming, enter the configuration bar, select Safety Configuration, and turn on the brakes of joints 1, 2, and 3 in turn (if only one joint is out of limit, turn on the corresponding out-of-limit joint, and do not need to turn on all 123 brakes).
③ After turning on the brake, the joint can be moved manually. Please manually adjust the joint to the normal posture, and then turn off the brake after the adjustment is completed.
④ Restart the robot in roboflow, and pay attention to the joint posture not exceeding the limit later

![](../resources/3-UserNotes/FAQ/img/sofware_8.png)

![](../resources/3-UserNotes/FAQ/img/sofware_9.png)

![](../resources/3-UserNotes/FAQ/img/sofware_10.png)


If the above error occurs:
Close Roboflow, open the command line and enter elerob -l

![](../resources/3-UserNotes/FAQ/img/sofware_11.png)

Restarting RoboFlow can solve the problem

**Q: When the two joints of 600 move at the same time, the movement speed is very fast. How to deal with it?**

A: Regarding the problem you mentioned that the J4 movement speed is inconsistent when the joint 1 is 0 and 0.0001, please refer to the explanation below
First of all, this phenomenon is normal
In the two sets of angle values ​​you set, the change of J1 is very small, while the movement range of J4 is relatively large. When this set of instructions is issued, the motor inside the robot arm has a synchronous execution mechanism, which means that between the two points, the time for J1 to move forward and backward is the same as the time for J4 to move forward and backward. Since the angle change of J1 is too small, the running time is naturally relatively short. This leads to the fact that in the case of synchronous execution, the J4 joint needs to complete a relatively large angle change in the same relatively short movement time, which results in a faster speed of J4
In order to adjust the running speed of the machine to a slower state, we recommend that you use the API to control a single joint when you only need to control one joint: write_angle
If you want to control multiple joints to move at the same time, please use write_angles to minimize the angle difference between different joints. For example, the difference between J1's 0 and 0.00001 is 0, while the difference between J4's -150 and -100 is 40. This difference is too big. If you change J1's change to 0 to 100, the movement speed is basically normal and not too fast. You can test it.

**Q: The latest version and update tutorial of roboflow for 630:**

- A: Close roboflow, then use a USB flash drive to copy the file to the Raspberry Pi, and follow the video
Video:
https://drive.google.com/file/d/1N_lDCe4H-Oyy0yGGVttszHlmmVVN-K94/view?usp=sharing
File (2024.10.10):
https://drive.google.com/file/d/1h6UIe9G9Mum_dutInfaqH_oVjJHSrqn6/view?usp=sharing

**Q: After pressing the emergency stop, the P600 cannot continue to be controlled using python. How to deal with this?**

- A: Under normal circumstances, python can still be used to control after pressing the emergency stop. The reason for the failure to control is that power_off() is not used to completely power off the P600. Add power_off() before starting the robot.

**Q: How to deal with the situation where the robot arm reports an error and cannot continue to move after the 600 runs beyond the limit?**

- A: If the 456 joints are out of limit, please press the emergency stop switch, move the 456 joints back to the normal posture and then start the robot

If the 123 joints are out of limit, you can adjust the out-of-limit joint posture according to the following steps

① Enter the configuration center in roboflow, and click Power on only in the Initialization column

② Click Start Programming, enter the configuration column, select Safety Configuration, and turn on the brakes of joints 1, 2, and 3 in turn (if only one joint is out of limit, turn on the corresponding out-of-limit joint, and do not need to turn on all 123 brakes).

③ After turning on the brake, the joint can be moved manually. Please manually adjust the joint to the normal posture and turn off the brake after the adjustment is completed

④ Restart the robot in roboflow, and pay attention to the joint posture not to exceed the limit later

![](../resources/3-UserNotes/FAQ/img/sofware_8.png)

**Q: Does 630 have a collision detection function? If so, can the collision detection threshold be adjusted?**

- A: Our machine has a collision detection design. When a large collision is received, the machine will automatically stop moving. If you want to detect a smaller force and generate a collision detection, you can try to adjust the following collision detection parameters. The recommended single adjustment range is 0.01

![](../resources/3-UserNotes/FAQ/img/sofware_12.png)

**Q: How to solve wait_command_done:-1 when the coordinate control of 630&600 cannot be used?**

Check if the robot arm is in the following posture

![](../resources/3-UserNotes/FAQ/img/sofware_13.png)

Then use the two APIs get_angles and get_coords to obtain the coordinates and angles

![](../resources/3-UserNotes/FAQ/img/sofware_14.png)

After obtaining the coordinates and angles, modify the angles and coordinates of write_angles and write_coords

![](../resources/3-UserNotes/FAQ/img/sofware_15.png)

```python
from pymycobot import ElephantRobot
import time

# This code is not powered on, you must make sure you have powered on.
if __name__=='__main__':

# "Change the ip to the real-time ip of the P600 Raspberry Pi" 
elephant_client = ElephantRobot("192.168.1.153", 5001,debug=True) 

elephant_client.start_client() 

print(elephant_client.get_angles()) 
time.sleep(1) 
print(elephant_client.get_coords()) 
time.sleep(1) 

elephant_client.write_angles([0.0, -144.884, 138.455, -89.648, -89.824, 0.0], 1000) 
elephant_client.command_wait_done() 



elephant_client.write_coords([80.014, 156.939, 316.656, 174.274, -0.0, 110.002], 3000)
elephant_client.command_wait_done()

```

**Q: What are forward kinematics and inverse kinematics?**

- A: Forward kinematics refers to solving the position and posture of the robot's end effector (such as the gripper of the robot arm) in Cartesian space when the angles (or displacements) of each joint of the robot are known. It is implemented in the get_coords() API, but the specific algorithm is not public.
Inverse kinematics is the opposite of forward kinematics. It refers to solving the angles (or displacements) of each joint of the robot when the position and posture of the robot's end effector in Cartesian space are known. write_coords(), send_coords()