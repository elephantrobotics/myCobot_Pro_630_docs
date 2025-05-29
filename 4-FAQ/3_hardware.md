# 硬件问题

**Q：600/630连接显示屏无法显示画面怎么办？**

机械臂存在2个HDMI接口，目前只有中间的HDMI接口可以使用，侧方的HDMI接口是无法使用的。

**Q：myCobot Pro 600机械臂工作时的功率是多少呀？**

- A: 240W 48V 5A

**Q: 600/630的基坐标原点在哪里？**

600/630的基坐标原点在②所在的位置（如图所示），而非①所在的位置


![](../resources/3-UserNotes/FAQ/img/hardware_1.png)


**Q: Re-zero calibration in cmd: this is not necessary, （编码器异常问题排查-600）**

- A: 可能是因为之前长时间未使用，导致电机编码器出现错误。现在请拆卸机械手 J2 和 J3 的外壳，检查编码器中是否有红灯，找到编码器的线，按下它，编码器中出现绿灯，就可以正常使用了。


![](../resources/3-UserNotes/FAQ/img/hardware_2.png)

![](../resources/3-UserNotes/FAQ/img/hardware_3.png)


![](../resources/3-UserNotes/FAQ/img/hardware_4.png)


**Q：630主控是什么？原生系统是什么？**

- A：树莓派4B 8G内存   debian系统


**Q:为什么树莓派会造成无法进入操作系统的现象?**

- A:两种可能，第一种是瞬间电流导致TF卡和树莓派系统镜像损坏，也可能是TF卡容量不足造纸系统挂机，因为出厂内存留给客户的并不多大部分都是被mycobot_ros这个文件夹占用，可以让客户在产品还未发生黑屏现象提示内存不足的时候删除除了该型号产品以外的文件夹保留产品使用空间。如果内存数据过多，满了的情况下是无法开机的。

**Q:600/630的充电器DC接口的规格是什么？**

![](../resources/3-UserNotes/FAQ/img/hardware_5.png)

