# mycobot630 and PLC IO interactive control case

## 1 Hardware wiring
### 1.1 Wiring of robot input and PLC output
PLC is Siemens 1200, the output type of PLC is PNP, and the input type of robot is NPN, so an external intermediate relay is required to convert the signal.

First connect 24V to the PLC output
![](../../../resources/1-ProductIntroduction/1.4/PLC/1.jpg)
Then connect the relay coil to the common terminal and Q0.0 of the PLC
![](../../../resources/1-ProductIntroduction/1.4/PLC/3.jpg)
![](../../../resources/1-ProductIntroduction/1.4/PLC/4.jpg)
Then connect the normally open contact wire of the relay to the terminal
![](../../../resources/1-ProductIntroduction/1.4/PLC/5.jpg)
Then connect the terminal to the input of the robot
![](../../../resources/1-ProductIntroduction/1.4/PLC/6.jpg)

### 1.1 Wiring the output of the robot arm and the input of the PLC
PLC is Siemens 1200. The input type of the PLC supports PNP or NPN. The output type of the robot arm is PNP, so the input of the PLC adopts the PNP type connection

First connect 24V to the input end of the PLC
![](../../../resources/1-ProductIntroduction/1.4/PLC/7.jpg)
Then connect the GND and OUT1 of the robot arm to the common end and I0.0 of the PLC
![](../../../resources/1-ProductIntroduction/1.4/PLC/8.jpg)
Then insert the terminal into the output of the robot arm
![](../../../resources/1-ProductIntroduction/1.4/PLC/10.jpg)

## 2 Software Programming
**You need to start the robot system before use**
![](../../../resources/1-ProductIntroduction/1.4/poweron/poweron.png)
![](../../../resources/1-ProductIntroduction/1.4/poweron/poweron2.png)

Confirm the IP address of the robot arm: Enter ifconfig in the terminal to obtain
![](../../../resources/1-ProductIntroduction/1.4/poweron/ip.png)
```python

from pymycobot import ElephantRobot
import time

# Change the ip to the real ip of the P600 Raspberry Pi

elephant_client = ElephantRobot("192.168.10.158", 5001)

# Necessary commands to start the robot
elephant_client.start_client()
time.sleep(1)
elephant_client.set_digital_out(0,1)
time.sleep(1)
while True:

if elephant_client.get_digital_in(0)=='1':
elephant_client.write_angle([0,0,0,0,0,0],1500)
elephant_client.command_wait_done()
break
else:
pass
```
PLC program
![](../../../resources/1-ProductIntroduction/1.4/PLC/plc1.png)