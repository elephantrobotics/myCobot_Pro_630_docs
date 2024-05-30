# **Developed based on Python API**
&ensp;&ensp;Elephant provides Python API to remotely control the robot. We use TCP protocol to communicate between the client and the robot, so before using our API, you need to follow the documentation and operate the following.

## **1 Environment setup**
### 1.1 Install Python


* **Python official download address: https://www.python.org/downloads/**
* **It is recommended to install version 3.7 and above**
* **Click the `Downloads` option to start downloading Python, click `Add Python 3.10 to PATH`, click `Install Now` to start installing Python**

<img src="../../resources/7-ApplicationBasePython/pythondownload1.jpg" style="zoom: 33%;" />

<img src="../../resources/7-ApplicationBasePython/pythondownload2.jpg" style="zoom: 50%;" />

<img src="../../resources/7-ApplicationBasePython/pythondownload3.jpg" style="zoom: 50%;" />



* **The prompt "Setup was successful" appears, indicating that the installation is complete**

<img src="../../resources/7-ApplicationBasePython/pythondownload4.jpg" style="zoom: 50%;" />




### 1.2 pymycobot installation
* pymycobot installation. Open a console terminal (shortcut key Win+R, enter cmd to enter the terminal), enter the following command and press the Enter key on the keyboard to install:

```python
pip install pymycobot --upgrade
```

<img src="../../resources/7-ApplicationBasePython/pymycobot安装.jpg" style="zoom: 67%;" />


## 2 **Enable TCP server function**


### **2.1 Log in to RoboFlow operating system**

&ensp;&ensp;After the robot is powered on, use VNC Viewer to enter the Raspberry Pi and log in to the RoboFlow operating system.
<div align=center><img src="../../resources/2-serialproduct/myCobot Pro 600/Chinese/p0.png"></div>

### **2.2 Start the robot**
&ensp;&ensp;Enter the configuration center and click the Start Robot button
<div align=center><img src="../../resources/2-serialproduct/myCobot Pro 600/Chinese/p1.png"></div>
<br>
<div align=center><img src="../../resources/2-serialproduct/myCobot Pro 600/Chinese/p2.png"></div>
<br>
<div align=center><img src="../../resources/2-serialproduct/myCobot Pro 600/Chinese/p3.png"></div>

### **2.3 Check whether the TCP server is open**
&ensp;&ensp;Return to the main menu, click Write Program, and then click the blank program. After entering the program editing interface, click the Configuration button, click the Network/Serial Port option, and check whether the TCP server is turned on. Normally, **TCP server is the default If it is turned on**, if it is not turned on, it needs to be turned on manually.

<div align=center><img src="../../resources/2-serialproduct/myCobot Pro 600/Chinese/p4.png"></div>
<br>
<div align=center><img src="../../resources/2-serialproduct/myCobot Pro 600/Chinese/p5.png"></div>
<br>
<div align=center><img src="../../resources/2-serialproduct/myCobot Pro 600/Chinese/p6.png"></div>
<br>
<div align=center><img src="../../resources/2-serialproduct/myCobot Pro 600/Chinese/p7.png"></div>

## 3 **Python API interface description**
### 3.1 ElephantRobot class instantiation
```
"Import ElephantRobot class from pymycobot library"
from pymycobot import ElephantRobot

"Connect to robot server"
elephant_client = ElephantRobot("192.168.137.182", 5001)

"Start TCP communication"
elephant_client.start_client()
```
**Using the Python API, you must first instance the ElephantRobot class before calling the functional functions of mycobot pro600**
- **Required parameters**:
&ensp;&ensp; **Parameter 1**: Actual IP address of the robot
&ensp;&ensp; **Parameter 2**: Robot port (**API function port is fixed at 5001**)
### 3.2 Function introduction
**def start_client()**:
- **Function**: Open TCP connection (**If you want to use Python API to control the robot, you must call this API**)
- **Parameters**: None
  
**def stop_client()**:
- **Function**: Close TCP connection
- **Parameters**: None

**def send_command(command)**:
- **Function**: Send instructions to the server
- **Parameter**: instruction (string type)

**def string_to_coords(data)**:
- **Function**: Convert string type data to list type data
- **Parameter**: String type data

**def string_to_double(data)**:
- **Function**: Convert string type data to double precision floating point data
- **Parameter**: String type data

**def string_to_int(data)**:
- **Function**: Convert string type data to integer type data
- **Parameter**: String type data
  
**def invalid_coords()**:
- **Function**: Return an invalid Cartesian coordinate to the server
- **Parameters**: None

**def get_angles()**:
- **Function**: Request the current joint angle information from the server
- **Parameters**: None

**def get_coords()**:
- **Function**: Request the current Cartesian pose information from the server
- **Parameters**: None
  
**def get_speed()**:
- **Function**: Request the robot movement rate from the server
- **Parameters**: None

**def power_on()**:
- **Function**: Power on the robot
- **Parameters**: None

**def power_off()**:
- **Function**: Power off the robot
- **Parameters**: None

**def check_running()**:
- **FEATURE**: Check if the bot is running
- **Parameters**: None

**def state_check()**:
- **Function**: Get robot status
- **Parameters**: None

**def read_next_error(data)**:
- **FEATURE**: Robot error detection
- **Parameters**: None
  
**def write_coords(coords,speed)**:
- **Function**: Send the overall coordinates and attitude to move the robot arm head from the original point to the designated point
- **Parameters**: Robot Cartesian pose (list type), robot arm movement speed: [0-6000]

**def write_coord(axis, value, speed)**:
- **Function**: Send a single coordinate value to the robot arm for movement
- **Parameters**: Cartesian position of the robot [0 represents x, 1 represents y, 2 represents z, 3 represents rx, 4 represents ry, 5 represents rz], the coordinate value to be reached, the speed of the robot arm movement: [ 0-6000]

**def write_angles(angles,speed)**:
- **Function**: Send all angles to all joints of the robotic arm
- **Parameters**: joint angle (list type), speed of robot arm movement: [0-1999]
  
**def write_angle(joint, value, speed)**:
- **Function**: Send the specified single joint motion to the specified angle
- **Parameters**: Specify the joint [0 represents j1, 1 represents j2, 2 represents j3, 3 represents j4, 4 represents j5, 5 represents j6], joint angle, and the speed of the robot arm movement: [0-1999]

**def set_speed(percentage)**:
- **FEATURE**: Set speed
- **Parameter**: target speed

**def set_carte_torque_limit(axis_str, value)**:
- **Function**: Set the torque limit of the robot
- **Parameters**: x/y/z/rx /ry/rz, torque
  
**def set_payload(payload)**:
- **FEATURE**: Set the robot's payload
- **Parameter**: Range 0.0 ~ 2.0

**def state_on()**:
- **Function**: Start the system
- **Parameters**: None

**def state_off()**:
- **Function**: Shut down the system
- **Parameters**: None

**def task_stop()**:
- **Function**: Task Pause
- **Parameters**: None

**def jog_angle(joint_str, direction, speed)**:
- **Function**: Control the robot to continuously move at a specified angle
- **Parameter**: The joint of the robot arm [J1/J2/J3/J4/J5/J6], mainly controls the direction of movement of the robot arm [-1=negative direction, 0=stop, 1=positive direction], robot speed of movement

**def jog_coord(axis_str, direction, speed)**:
- **Function**: Control the robot to continuously move in the specified coordinate axis direction
- **Parameter**: Cartesian direction [x/y/z/rx/ry/rz], mainly controls the direction of movement of the robot arm [-1=negative direction, 0=stop, 1=positive direction], robot speed of movement
  
**def get_digital_in(pin_number)**:
- **Function**: Get input pin signal
- **Parameter**: Pin number

**def get_digital_out(pin_number)**:
- **Function**: Get output pin signal
- **Parameter**: Pin number

**def set_digital_out(pin_number, pin_signal)**:
- **Function**: Set output pin signal
- **Parameters**: pin number, pin status [0=low level, 1=high level]
  
**def get_acceleration()**:
- **Function**: Get the acceleration of the robot
- **Parameters**: None

**def set_acceleration(acceleration)**:
- **Function**: Set the acceleration of the robot
- **Parameter**: Acceleration

**def command_wait_done()**:
- **Function**: Wait until the last motion command is completed (**This API function must be added after all motion API functions**)
- **Parameters**: None

**def wait(seconds)**:
- **Function**: Waiting time (in seconds)
- **Parameters**: None
  
**def assign_variable(var_name, var_value)**:
- **Function**: Assign values to defined variables
- **Parameters**: variable name (string type), target value

**def get_variable(var_name)**:
- **Function**: Get the value of a variable
- **Parameter**: variable name (string type)

## 4 **Python API use case**
### 4.1 **Joint Control**
&ensp;&ensp;After using VNC Viewer to enter the RoboFlow system, under the fast movement interface, you can use joint control to control the robot to reach the target position and record the angles of the six joints of the robot displayed on the operation panel.
<div align=center><img src="../../resources/2-serialproduct/myCobot Pro 600/Chinese/p9.png"></div>

#### 4.1.1 **Multi-joint control**
```
from pymycobot import ElephantRobot

if __name__=='__main__':
     "Connect to robot server"
     elephant_client = ElephantRobot("192.168.137.182", 5001)

     "Enable TCP communication"
     elephant_client.start_client()

     "Fill in the recorded 6 joint angles in the list, and the last parameter is the movement speed"
     elephant_client.write_angles([94.828,-143.513,135.283,-82.969,-87.257,-44.033],1000)

     "Wait for the robot to move to the target position before executing subsequent instructions"
     elephant_client.command_wait_done()

```
#### 4.1.2 **Single joint control**
```
from pymycobot import ElephantRobot

if __name__=='__main__':
     "Connect to robot server"
     elephant_client = ElephantRobot("192.168.137.182", 5001)

     "Enable TCP communication"
     elephant_client.start_client()

     "Fill in the angle of a single joint to be controlled, the first parameter 0 is the first axis, and so on; the second parameter represents the joint angle; the third parameter represents the movement speed"
     elephant_client.write_angle(0,94.828,1000)

     "Wait for the robot to move to the target position before executing subsequent instructions"
     elephant_client.command_wait_done()

```
#### 4.1.3 **Joint angle acquisition**
```
from pymycobot import ElephantRobot

if __name__=='__main__':
     "Connect to robot server"
     elephant_client = ElephantRobot("192.168.137.182", 5001)

     "Enable TCP communication"
     elephant_client.start_client()

     "Print the current 6 joint angle information of the robot"
     elephant_client.get_angles()

     "Wait for the robot to move to the target position before executing subsequent instructions"
     elephant_client.command_wait_done()

```

### 4.2 **Coordinate Control**
&ensp;&ensp;It is mainly used to realize intelligent planning of routes to get the robotic arm from one location to another designated location. Divided into [x, y, z, rx, ry, rz], where [x, y, z] represents the position of the end of the robotic arm in space (the coordinate system is a rectangular coordinate system), [rx, ry, rz] represents the attitude of the end of the robotic arm at this point (the coordinate system is Euler coordinates)
&ensp;&ensp;After using VNC Viewer to enter the RoboFlow system, under the fast movement interface, you can use Cartesian coordinate control to control the robot to reach the target position and record the 6 coordinate values of the robot displayed on the operation panel.
<div align=center><img src="../../resources/2-serialproduct/myCobot Pro 600/Chinese/p10.png"></div>

#### 4.2.1 **Multi-parameter coordinate control**
```
from pymycobot import ElephantRobot

if __name__=='__main__':
     "Connect to robot server"
     elephant_client = ElephantRobot("192.168.137.182", 5001)

     "Enable TCP communication"
     elephant_client.start_client()

     "Fill in the recorded 6 coordinate values in the list, the last parameter is the movement speed"
     elephant_client.write_coords([-130.824,256.262,321.533,176.891,-0.774,-128.700], 3000)

     "Wait for the robot to move to the target position before executing subsequent instructions"
     elephant_client.command_wait_done()

```
#### 4.2.2 **Single parameter coordinate control**
```
from pymycobot import ElephantRobot

if __name__=='__main__':
     "Connect to robot server"
     elephant_client = ElephantRobot("192.168.137.182", 5001)

     "Enable TCP communication"
     elephant_client.start_client()

     "Fill in the parameters, the 2 in the first parameter represents the Z-axis direction, and so on; the second parameter represents the relevant coordinate value; the third parameter represents the movement speed"
     elephant_client.write_coord(2,94.828,3000)

     "Wait for the robot to move to the target position before executing subsequent instructions"
     elephant_client.command_wait_done()

```
#### 4.2.3 **Get Cartesian space coordinates**
```
from pymycobot import ElephantRobot

if __name__=='__main__':
     "Connect to robot server"
     elephant_client = ElephantRobot("192.168.137.182", 5001)

     "Enable TCP communication"
     elephant_client.start_client()

     "Print out the current Cartesian space coordinate information of the robot"
     elephant_client.get_coords()

     "Wait for the robot to move to the target position before executing subsequent instructions"
     elephant_client.command_wait_done()

```
### 4.3 **IO Control**

#### 4.3.1 **Set IO pin output status**
```
from pymycobot import ElephantRobot

if __name__=='__main__':
     "Connect to robot server"
     elephant_client = ElephantRobot("192.168.137.182", 5001)

     "Enable TCP communication"
     elephant_client.start_client()

     "Control the robot OUT1 output to high level"
     elephant_client.set_digital_out(0,1)

     "The robot delays for 3 seconds before executing the following program"
     elephant_client.wait(3)

     "Control the robot OUT1 output to low level"
     elephant_client.set_digital_out(0,0)

     "The robot delays for 3 seconds before executing the following program"
     elephant_client.wait(3)

```
#### 4.3.1 **Get IO pin output status**
```
from pymycobot import ElephantRobot

if __name__=='__main__':
     "Connect to robot server"
     elephant_client = ElephantRobot("192.168.137.182", 5001)

     "Enable TCP communication"
     elephant_client.start_client()

     "Get the robot OUT1 output status"
     elephant_client.get_digital_out(0)

     "The robot delays for 0.5 seconds before executing the following program"
     elephant_client.wait(0.5)

```
#### 4.3.1 **Get IO pin input status**
```
from pymycobot import ElephantRobot

if __name__=='__main__':
     "Connect to robot server"
     elephant_client = ElephantRobot("192.168.137.182", 5001)

     "Enable TCP communication"
     elephant_client.start_client()

     "Get the robot IN1 input status"
     elephant_client.get_digital_in(0)

     "The robot delays for 0.5 seconds before executing the following program"
     elephant_client.wait(0.5)

```
## 5 **Python API application scenario case**
### 5.1 **Transportation and Palletizing**
```
from pymycobot import ElephantRobot

if __name__=='__main__':
     "Connect to robot server"
     elephant_client = ElephantRobot("192.168.137.182", 5001)
     "Enable TCP communication"
     elephant_client.start_client()
     for i in range (1):
         "Robot joints move to a safe point"
         elephant_client.write_angles([94.828,-143.513,135.283,-82.969,-87.257,-44.033],1000)
         "Wait for the robot to move to the target position before executing subsequent instructions"
         elephant_client.command_wait_done()
        
         "Transition point from robot Cartesian motion to palletizing and grabbing"
         elephant_client.write_coords([-130.824,256.262,321.533,176.891,-0.774,-128.700], 3000)
         elephant_client.command_wait_done()

         "Control the robot to move Cartesianly in the Z-axis direction to the palletizing grab point"
         elephant_client.write_coord(2,241.533,3000)
         elephant_client.command_wait_done()
        
         "Control the robot OUT1 output to high level"
         elephant_client.set_digital_out(0,1)
         "Control the robot to wait for 1 second before taking action"
         elephant_client.wait(1)

         "Control the robot to move Cartesianly in the Z-axis direction to the palletizing and grabbing transition point"
         elephant_client.write_coord(2,321.533,3000)
         elephant_client.command_wait_done()

         "Control robot movement to placement transition point"
         elephant_client.write_coords([86.687,255.542,320.867,177.065,-1.333,-128.721], 3000)
         elephant_client.command_wait_done()

         "Control the robot to move Cartesianly in the Z-axis direction to the palletizing point"
         elephant_client.write_coord(2,241.533,3000)
         elephant_client.command_wait_done()
        
         "Control the robot OUT1 output to low level"
         elephant_client.set_digital_out(0,0)
         elephant_client.wait(1)

         "Control the robot to move Cartesianly in the Z-axis direction to the palletizing transition point"
         elephant_client.write_coord(2,321.533,3000)
         elephant_client.command_wait_done()

         "Robot joints move to a safe point"
         elephant_client.write_angles([94.828,-143.513,135.283,-82.969,-87.257,-44.033],1000)
         elephant_client.command_wait_done()

   
```

---
[← Previous page](../6-SDKDevelopment.md) | [Next page → ](../../11-ApplicationBaseROS/11.1-ROS1/README.md)