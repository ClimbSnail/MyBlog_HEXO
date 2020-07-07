---
title: 香橙派 OrangePi Zero plus主频1.3Ghz启动失败
date: 2020-07-01 14:35:43
updated: 2020-07-01 14:35:43
tags: 硬件
---

#### 简要介绍
硬件方面OrangePi Zero plus使用的是全志H5芯片。四核A53芯片。

使用的系统是[armbian](https://www.armbian.com/orange-pi-zero-plus/)，刷完系统，开机默认运行最高的频率为1008Mhz。

七七八八装了很多软件以及配置了相关的环境。

由于了解到全志H5芯片是可以工作在1.3Ghz的主频上。所以接着就想调节到更高的性能，调节过程中由于主频不适配硬件，导致启动失败。

<!-- more -->

#### 使用armbian-config命令进行调节主频到1.2Ghz
###### 1. 进入系统设置选项
![进入System选项](https://gitee.com/ClimbSnailQ/Project_Image/raw/master/Note/OrangePi_Zero_Plus_System.jpg)


###### 2. 进入硬件调节选项
使用的是conservative调节器，有关调节器的介绍放在了<a href="#调节器"><font size=2 color=#00f>文末</font></a>。<br>
![进入硬件调节选项](https://gitee.com/ClimbSnailQ/Project_Image/raw/master/Note/OrangePi_ArmbianConfig_HW.png)

###### 3. 光标通过方向键移动到指定的选项，这里选择1.2V，按空格键勾选选项，设置完毕先`Save`，后`Back`。
![选择1.2V主频](https://gitee.com/ClimbSnailQ/Project_Image/raw/master/Note/OrangePi_Zero_Plus_1.2.jpg)
<br>
用armbian-config将主频提高到了1.2Ghz，修改主频将在重启之后生效。

###### 4. 重启后，查询状态
使用armbian-config查看CPU的频率，这时已经可以在1.2Ghz的频率上工作了。

#### 将主频调至1.3Ghz出现问题
后期同样的操作调节主频到1.3Ghz，结果系统没能成功启动。<br>
重要的是，我的环境不就白配了吗？？？<br>
![选择1.3V主频](https://gitee.com/ClimbSnailQ/Project_Image/raw/master/Note/OrangePi_CPU_1.3.png)

###### 以下是TTL的最后的启动日志。
![启动失败日志](https://gitee.com/ClimbSnailQ/Project_Image/raw/master/Note/OrangePi_StartupLog.png)

##### 穿插一段关于联系香橙派售后
1. 先是让帮忙联系技术确定一下板子CPU能不能跑到1.3Ghz，结果客服让等（最后没给任何答复）。
2. 后来查出是硬件缺少Q5后（下文有介绍），再次联系客服，让硬件工程师给个答复:缺少Q5是与不是跑不到1.3Ghz（是与不是的问题），又让我等，最后好几天（当然期间已经自行解决了）过去了还是没给任何答复。<br>

![香橙派售后聊天](https://gitee.com/ClimbSnailQ/Project_Image/raw/master/Note/OrangePi_Service.jpg)


注：个人也觉得这类东西需要自己学习，过多的询问卖家肯定不合理。但是我就只是简单的一个问题，就只是给我一个"是与不是"的答案就够了，压根不花费工程师多少时间。香橙派的服务真是太差了。

#### 好了，开始自己的研究了
经过一番查找后，终于占到了问题所在。

这里是OrangePi Zero plus的原理图 <https://linux-sunxi.org/images/6/67/ORANGE_PI-ZERO-PLUS_V1_0_Schematic.pdf>

可以看到第7页的CPU供电原理图。
![CPU供电原理图](https://gitee.com/ClimbSnailQ/Project_Image/raw/master/Note/OrangePi_ZeroPlus.png)

左上角标注着两种电压，可以看到这个电压逻辑上是由这个Q5这颗nmos管控制的。

![原背板图](https://gitee.com/ClimbSnailQ/Project_Image/raw/master/Note/OrangePi_PCB_1.jpg)
随即查看了手头的这块Zero Plus，发现背板只有一处空余着的焊盘，就在内存卡插槽的上方，而这处恰好是Q5。默认出厂的OrangePi Zero Plus这个Q5是省缺的。

这不，问题找到了，而手头没有BSN20这个贴片(SOT-23封装的N mos)，百度了以下这个BSN20相关参数，从元件盒里找了一片SI2302 (丝印为A2SHB)来代替。
![添加NMos后的背板](https://gitee.com/ClimbSnailQ/Project_Image/raw/master/Note/OrangePi_Zero_Plus_PCB2.jpg)

开机，顺利启动！
armbian-config命令进设置，可以看到主页面的CPU信息成功调节到480Mhz-1296MHz之间了。
![启动成功后的显示](https://gitee.com/ClimbSnailQ/Project_Image/raw/master/Note/OrangePi_ArmbianConfig_Main_After.png)

首先，CPU的散热我是使用可固化的STARS922导热胶粘连20*20*10mm的散热片。
![板子正面图](https://gitee.com/ClimbSnailQ/Project_Image/raw/master/Note/OrangePi_ZeroPlus_P2.jpg)

![板子侧面图](https://gitee.com/ClimbSnailQ/Project_Image/raw/master/Note/OrangePi_ZeroPlus_P1.jpg)


后期，我对其进行压力测试，在只跑满两个核心的情况下，五分钟CPU的温度就上到了85度以上，但到达90以上时，就已经开始降频到1Ghz以下了。所以，在没有足够好的散热情况下，不建议将主频调制1.2/1.3Ghz。


#### <a id="调节器">cpu调节器(governor)</a>
1. performance：将CPU频率固定工作在其支持的最高运行频率上，不动态调节，可以获取到最大的性能。
2. powersave: 将 CPU 频率设置为最低的所谓 “省电” 模式，CPU 会固定工作在其支持的最低运行频率上。因此这两种 governors 都属于静态 governor，即在使用它们时 CPU 的运行频率不会根据系统运行时负载的变化动态作出调整。这两种 governors 对应的是两种极端的应用场景，使用 performance governor 是对系统高性能的最大追求，而使用 powersave governor 则是对系统低功耗的最大追求。
3. Userspace：最早的 cpufreq 子系统通过 userspace governor 为用户提供了这种灵活性。系统将变频策略的决策权交给了用户态应用程序，并提供了相应的接口供用户态应用程序调节 CPU 运行频率使用。
4. ondemand：按需快速动态调整 CPU 频率， 一有 cpu 计算量的任务，就会立即达到最大频率运行，等执行完毕就立即回到最低频率；ondemand：userspace 是内核态的检测，用户态调整，效率低。
5. conservative: 与 ondemand 不同，平滑地调整 CPU 频率，频率的升降是渐变式的, 会自动在频率上下限调整，和 ondemand 的区别在于它会按需分配频率，而不是一味追求最高频率;


### 致谢
感谢帮助最大的讨论: <https://forum.armbian.com/topic/11967-orange-pi-zero-plus-cpu-frequency-problem/>