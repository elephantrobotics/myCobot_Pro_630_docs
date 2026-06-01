#630+五指灵巧手使用手册：

#1.五指灵巧手python接口：
获取灵巧手的关节角度get_five_fingers_angles(2)
发送灵巧手的关节角度 set_five_fingers_angles(2,ID)

#2.使用说明：将五指灵巧手85线接入到机械臂的接口上，正常通电情况下，灵巧手会响应一声，响应过后五个手指会进行握紧再释放

#3.Python代码示例:
from pymycobot import ElephantRobot
import time
er=ElephantRobot("192.168.123.102", 5001)
er.start_client()
angles = [36.86,100,100,100,100,0]
angles_1 = [36.76,178,176,176,174,0]
er.set_five_fingers_angles(2,angles)
