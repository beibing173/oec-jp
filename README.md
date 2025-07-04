# oec-jp

This is oec to armbian'readme.

zh-cn

这些工具可以帮助你刷机OEC/OECT成为armbian系统
教程：
2024年运营商大战PCDN行业，各大边缘计算业务受到冲击，“矿难”虽无情，但垃圾佬狂喜，网心云OEC成为新一代矿渣神器，外观和玩客云基本一样，还可以刷机成Armbian系统后解锁轻量NAS、OpenWrt旁路由、迅雷下载机等玩法。

🔺 大量的网心云OEC/OEC-turbo流入海鲜市场，仅需70到90元，同配置的轻量级NAS拾光坞N3要380元，仅需一个零头即可拿下，性价比很高

🔺 网心云OEC和OEC-turbo唯一的区别是内存2GB和4GB，建议直接上turbo版，4GB内存上限高很多

处理器是瑞芯微RK3566，由于是A55架构，性能比N1盒子S905D还要高一点，有一个SATA硬盘位和USB3.0接口，可玩性也比N1更高。

网心云OEC刷机
OEC刷机需要进行拆机，然后短接电路板，连接电脑进行刷写固件、整体难度和玩客云一样，并不是很难，耐心一点就行，刷机准备工作：

网心云OEC/OEC-turbo一台
Type-C数据线
曲别针/镊子
Windows电脑＆刷机资料包
网心云OEC拆机
拆机前先介绍一下接口，

🔺 从左到右，12V/2A的DC电源、REST重置按键、千兆网口、USB3.0接口

🔺 底部向上推一下打开盖板

🔺 有一个SATA硬盘位、一个Type-C接口，使用螺丝刀拧下4颗螺丝

🔺 向上推一下外壳、然后取下侧面外壳，拆卸SATA接口，用螺丝刀拧下三颗螺丝，把SATA接口翻转过来，撕下保护排线的黑胶带，SATA排线很薄比较脆弱不能硬扯，取排线有技巧的，左边黑色的卡扣可以向上扣开，这样是解锁了，可以很轻松把SATA排线取出来。

🔺 然后用螺丝刀拧下内壳上面的8颗螺丝，使用一个卡片在左边空隙慢慢撬一下，取出内壳。

🔺 主板上还有4颗螺丝，使用螺丝刀拧下来，然后把反射LED灯光的白色底座取下来，用手指按住网口往里面用点力推动一下，双手左右晃动网心云OEC几次，主板松动了，轻松拿捏取出主板。

🔺 终于看到庐山真面目了，主板正面有我们需要短接的两个焊点，背面是大面积的散热片，下面有RK3566这颗四核的CPU。

然后，TypeC数据线连接电脑，另一头准备连接OEC主板备用。

安装驱动

🔺 双击安装DriverAssitant瑞芯微驱动助手，成功后点击确认

🔺 返回主目录打开刷机软件RKDevTool，注意点击箭头三个小点的位置选择目录里的文件：1、LoaderToDDR 选择 MiniLoaderAll.bin；2、System 选择要刷机的固件包，我这里是oec-jp（Armbian系统）

短接焊点刷机
这一步很关键，先说下整体流程，按步骤操作：先短接焊点、再插入TypeC数据线，软件提示发现一个MASKROM设备，点击执行，等待下载数据烧录即可。

短接点：（GND和1V8）
见： https://pic4.zhimg.com/v2-b01da4cfe26c940065af5c992d6d0665_1440w.jpg

🔺 使用Type-C数据线连接电脑，然后使用曲别针或者镊子等金属短接图上2个点，调整一个合适的姿势，要保证两个点接通稳住，另一个手把Type-C数据线插入网心云

🔺 大概2秒左右，软件会提示：发现一个MASKROM设备，这个时候松开曲别针，在软件上点击执行即可

🔺 等待下载固件和写入网心云eMMC存储，整个刷机过程大概8分钟，看到下载完成，代表刷机完成了，我们可以关掉软件、拔掉OEC的数据线了。

从短接金属焊点到插入数据线，然后软件提示发现设备，到拿开曲别针总共是几秒钟左右，如果你操作了没有成功、没反应，拔掉数据线重新来过（不需要接入DC电源，TypeC数据线能供电）。

初见Armbian系统
网心云OEC刷机完成，赶快进入Armbian系统确认下，![v2-b01da4cfe26c940065af5c992d6d0665_1440w](https://github.com/user-attachments/assets/ae60d68d-d525-402b-8cb1-57ed9d20650f)


🔺 网心云先不着急装机，使用12V/2A的电源接入主板，然后把OEC接入家里的路由器

🔺 打开路由器后台查看设备，正常情况会有一个名称为armbian的设备，证明刷机armbian系统成功了，记录一下这个IP地址，后面SSH连接需要用到。

🔺 使用SSH软件连接OCE上的armbian系统，输入上面的IP地址，默认用户：root，密码：1234

第一次进来armbian系统后，会让你更改密码：我们输入两次密码，回车，之后会让你选择shell模式，一般选bash模式，最后会让你创建一个普通用户，不需要创建，可以Ctrl+C退出。

🔺 这颗RK3566处理器是跑在1.8GHz频率，那性能有保证呀，开机内存占用不到200MB，真不错啊，剩余空间随便折腾

网心云OEC重新装好外壳、恢复原状，插入一个SATA硬盘，测试一下功耗：

🔺 不会吧？！待机功耗2.2W，不过没有跑Docker之类的服务，ARM功耗真香~

总结
OK，经过上面一番猛如虎的操作，网心云OEC刷机至此结束，不到100元即可拥有一台轻量级NAS家用服务器，可以说是矿渣神器、适合喜欢折腾的玩家。

你可以跑轻NAS系统、安装Docker、迅雷下载、挂载alsit网盘等可玩性非常高，如果对你有帮助，欢迎star一下。
en
These tools can help you flash OEC/OECT to armbian system
Tutorial:
In 2024, operators will fight against the PCDN industry, and major edge computing businesses will be impacted. Although the "mining disaster" is ruthless, the garbage man is ecstatic. NetCenter OEC has become a new generation of mining artifact. The appearance is basically the same as Wanke Cloud. It can also be flashed to Armbian system to unlock lightweight NAS, OpenWrt bypass router, Thunder download machine and other gameplay.

🔺 A large number of NetCenter OEC/OEC-turbo have flowed into the seafood market, only 70 to 90 yuan, and the lightweight NAS Shiguangwu N3 with the same configuration costs 380 yuan, which is only a fraction of the price, and the cost performance is very high

🔺 The only difference between NetCenter OEC and OEC-turbo is the memory 2GB and 4GB. It is recommended to go directly to the turbo version, and the 4GB memory limit is much higher

The processor is Rockchip RK3566. Due to the A55 architecture, the performance is a little higher than the N1 box S905D. There is a SATA hard disk slot and USB3.0 interface, and the playability is also higher than N1.

NetCenter OEC Flashing
OEC flashing requires disassembly, then short-circuiting the circuit board, connecting to the computer to flash the firmware. The overall difficulty is the same as Wanke Cloud. It is not very difficult. Just be patient. Flashing preparation:

One NetCenter OEC/OEC-turbo
Type-C data cable
Paper clip/tweezers
Windows computer & flashing data package
NetCenter OEC disassembly
Before disassembling, let’s introduce the interface.

🔺 From left to right, 12V/2A DC power supply, REST reset button, Gigabit network port, USB3.0 interface

🔺 Push the bottom up to open the cover

🔺 There is a SATA hard disk slot and a Type-C interface. Use a screwdriver to unscrew 4 screws

🔺 Push the outer shell upwards, then remove the side outer shell, disassemble the SATA interface, unscrew the three screws with a screwdriver, turn the SATA interface over, and tear off the black tape protecting the cable. The SATA cable is very thin and fragile and cannot be pulled hard. There are skills to take out the cable. The black buckle on the left can be buckled upwards. This is unlocked, and the SATA cable can be easily taken out.

🔺 Then use a screwdriver to unscrew the 8 screws on the inner shell, use a card to slowly pry the gap on the left, and take out the inner shell.

🔺 There are 4 more screws on the motherboard. Use a screwdriver to unscrew them, then remove the white base that reflects the LED light, press the network port with your fingers and push it inward with a little force, shake the Net Heart Cloud OEC left and right with both hands a few times, the motherboard is loose, and it is easy to grasp and take out the motherboard.

🔺 Finally saw the true face of Mount Lu. There are two solder joints on the front of the motherboard that we need to short-circuit, and there is a large area of ​​heat sink on the back, and there is a quad-core CPU RK3566 below.

Then, connect the TypeC data cable to the computer, and prepare to connect the other end to the OEC motherboard for standby.

Install the driver

🔺 Double-click to install DriverAssitant, and click Confirm after success

🔺 Return to the main directory to open the flashing software RKDevTool. Note that you click the three small dots on the arrow to select the file in the directory: 1. LoaderToDDR Select MiniLoaderAll.bin; 2. System Select the firmware package to be flashed, here is oec-jp (Armbian system)

Short-circuit solder joints to flash
This step is very critical. Let me first talk about the overall process. Follow the steps: first short-circuit the solder joints, then insert the TypeC data cable. The software prompts that a MASKROM device has been found. Click Execute and wait for the downloaded data to be burned.

🔺 Use the Type-C data cable to connect the computer, and then use a paper clip or tweezers to short-circuit the two points on the diagram. Adjust a suitable posture to ensure that the two points are connected and stable. Use the other hand to insert the Type-C data cable into the Net Heart Cloud

🔺 After about 2 seconds, the software will prompt: A MASKROM device is found. At this time, release the paper clip and click Execute on the software

🔺 Wait for the firmware to be downloaded and written to the Net Heart Cloud eMMC storage. The entire flashing process takes about 8 minutes. When you see the download is complete, it means that the flashing is completed. We can turn off the software and unplug the OEC data cable.

From short-circuiting the metal solder joint to inserting the data cable, then the software prompts to find the device, to removing the paper clip, it takes a total of about a few seconds. If you fail to operate and there is no response, unplug the data cable and start again (no need to connect to a DC power supply, the Type C data cable can be powered).

First look at the Armbian system
NetCenter OEC flashing is complete, quickly enter the Armbian system to confirm,

🔺 Don't rush to install NetCenter, use a 12V/2A power supply to connect to the motherboard, and then connect OEC to the router at home

🔺 Open the router backend to check the device. Normally, there will be a device named armbian, which proves that the flashing of the armbian system is successful. Record this IP address, which will be used for SSH connection later.

🔺 Use SSH software to connect to the armbian system on OCE, enter the above IP address, default user: root, password: 1234

After entering the armbian system for the first time, you will be asked to change the password: we enter the password twice, press Enter, and then you will be asked to select shell mode, generally bash mode, and finally you will be asked to create a normal user. You don't need to create one, you can exit by pressing Ctrl+C.

🔺 This RK3566 processor runs at 1.8GHz, so the performance is guaranteed. The boot memory occupies less than 200MB, which is really good. You can do whatever you want with the remaining space.

Reinstall the shell of NetCenter OEC, restore it to its original state, insert a SATA hard drive, and test the power consumption:

🔺 No way? ! The standby power consumption is 2.2W, but there is no service like Docker running. The ARM power consumption is really good~

Summary
OK, after the above fierce operation, the NetCenter OEC flashing is over. You can own a lightweight NAS home server for less than 100 yuan. It can be said to be a slag artifact and suitable for players who like to toss.

You can run a light NAS system, install Docker, Thunder download, mount alsit network disk, etc. It is very playable. In the next issue,  If it helps you, welcome to star.
