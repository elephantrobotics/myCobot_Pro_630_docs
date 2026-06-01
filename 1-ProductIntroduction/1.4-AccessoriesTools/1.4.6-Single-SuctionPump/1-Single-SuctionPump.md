# Single head suction pump

> **Compatible models:** myCobot 320, myCobot Pro 600, myCobot Pro 630


## Product Pictures

<img src="./resources/2-serialproduct/myCobot_Pro_600/English/0.jpg" alt="" width="60%" height="60%" />



**Specifications**

| Name | Single head suction pump |
|---------------------|------------------------------------------------|
|Suction pump box size|150mmX150mmX108mm|
|Suction pump length|106mm|
|Suction cup diameter|25mm|
|Tracheal length|1m|
|Operating voltage|24V|
|Rated current|1A|
|Own weight|2kg|
| Rated load | 1kg |
|Flow rate| 10-15L/min|
|Negative pressure| -85Kpa|
| Fixing method | Screw fixing |
| Usage environment requirements | Normal temperature and pressure
| Control interface | IO control | |
| Applicable equipment | myCobot 320, myCobot Pro 600, myCobot Pro 630 |
<!-- | Service life | One year | -->

**Single head suction pump**: used to absorb objects

**Introduction**

- The suction cup suction pump connects the suction port to the object to be adsorbed through suction cups, pipes and other components, and evacuates the suction cup, causing the internal air pressure to change from normal pressure to negative pressure. The pressure difference between the external atmospheric pressure and this negative pressure is used to achieve the purpose of adsorbing the object.


**How it works**

- Start the suction of the vacuum equipment to generate negative air pressure in the suction cup, thereby sucking the object to be lifted firmly, and then start transporting the object to be lifted.
- When the object to be lifted is transported to the destination, inflate the vacuum suction cup smoothly, so that the negative air pressure in the vacuum suction cup changes to zero air pressure or slightly positive air pressure. The vacuum suction cup will separate from the object to be lifted, thus completing the task of lifting and transporting heavy objects.

**Applicable objects** Applicable to flat objects

## Hardware installation
First install the suction pump on the end of the robotic arm
![](./img/4.jpg)

Then connect the line of the suction pump control box to the base IO of the robotic arm.
![](./img/5.png)

# python development

## python control

**Pro 630 version**
```python
from pymycobot import ElephantRobot,utils
import time
elephant_client = ElephantRobot("192.168.10.158", 5001)
arm=ElephantRobot(utils.get_port_list()[0])
for i in range(1): 
arm.set_basic_output(1,0)#Open the suction pump 
time.sleep(2) 
arm.set_basic_output(1,1)#Close the suction pump 
time.sleep(2)
```
